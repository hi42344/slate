# Dynamic Libraries #

### Table of Contents

| Section | Description |
| :--- | :--- |
| [Writing a plugin](#writing-a-plugin) | Required exports and the plugin entry point |
| [Helper Macros](#helper-macros) | Less boilerplate |
| [The Value API](#the-value-api) | Constructing, inspecting, and freeing `SlateValue`s |
| [Registering functions](#registering-functions) | `slate_bind` |
| [Ownership](#ownership-rules) | Ownership Responsibly |
| [Full example](#full-example) | A complete plugin demonstrating every type |

- **All slate_api.h's are inside releases**

# Writing a plugin #

```cpp
#include "slate_api.h"

static const SlateAPI* g_api;

extern "C" __declspec(dllexport) int slate_api_version(void) {
    return SLATE_API_VERSION;
}

extern "C" __declspec(dllexport) void slate_plugin_init(SlateEnv env, const SlateAPI* api) {
    g_api = api;
    // register your functions here with g_api->bind
}
```

- Slate calls `slate_api_version()` automatically when loading your plugin and refuses to load it if the version doesn't match, so a plugin built against an older/newer Slate fails with a warning instead of crashing or behaving unpredictably. `slate_plugin_init` receives the `SlateAPI` function-pointer table, store it (`g_api` above) so every other function in your plugin can reach it.

- On non-Windows builds, `__declspec(dllexport)` isn't needed, `extern "C"` alone is sufficient, since ELF/Mach-O don't require an explicit export attribute the way Windows `.dll`s do. (The `SLATE_EXPORT` macro below handles this automatically)

**Compiling a plugin** (MinGW example):
```
g++ -shared -o myplugin.dll myplugin.cpp -I "slate_api_path.h"
```

# Registering functions #

- ```bind(env, name, fn, userdata)``` // Registers a C function under `name` (dotted names build a namespace the same way `data.write` etc. do). `fn` has the signature `SlateValue fn(SlateValue* args, int argc, void* userdata)`. `userdata` is passed through unchanged on every call , use it to give a function access to state (like `env` itself) without global variables

# Helper Macros #

- Note that there are some other tiny helper things

**Macros:**
```cpp
#ifndef SLATE_EXPORT
#ifdef __cplusplus
#define SLATE_EXTERN_C extern "C"
#else
#define SLATE_EXTERN_C
#endif

#if defined(_WIN32) || defined(__CYGWIN__)
#if defined(__GNUC__) || defined(__clang__)
#define SLATE_EXPORT SLATE_EXTERN_C __attribute__((dllexport))
#else
#define SLATE_EXPORT SLATE_EXTERN_C __declspec(dllexport)
#endif
#else
#if (defined(__GNUC__) && __GNUC__ >= 4) || defined(__clang__)
#define SLATE_EXPORT SLATE_EXTERN_C __attribute__((visibility("default")))
#else
#define SLATE_EXPORT SLATE_EXTERN_C
#endif
#endif
#endif

static const SlateAPI* g_api = nullptr;

#ifndef SLATE_FN
#define SLATE_FN(name, min_args) \
        SLATE_EXPORT SlateValue name(SlateValue* args, int argc, void* userdata) { \
            if (argc < (min_args)) { \
                return g_api->make_null(); \
            }

#define SLATE_END }
#endif

#ifndef SLATE_PLUGIN_INIT
#define SLATE_PLUGIN_INIT() \
        SLATE_EXPORT int slate_api_version(void) { return SLATE_API_VERSION; } \
        SLATE_EXPORT void slate_plugin_init_internal(SlateEnv env, const SlateAPI* api); \
        SLATE_EXPORT void slate_plugin_init(SlateEnv env, const SlateAPI* api) { \
            g_api = api; \
            slate_plugin_init_internal(env, api); \
        } \
        void slate_plugin_init_internal(SlateEnv env, const SlateAPI* api)
#endif
```

- ```SLATE_EXPORT``` // Expands to the correct `extern "C"` + export-visibility attribute for whichever platform you're compiling on
- ```SLATE_FN(name, min_args)``` // Opens a plugin function named `name`, with the standard `(SlateValue* args, int argc, void* userdata)` signature already declared, and an automatic `argc < min_args` guard that returns `null` if there aren't enough arguments. Must be closed
- ```SLATE_END``` // Closes a function opened with `SLATE_FN` (Not really needed tbh, a regular `}` is the same exact thing, may make organization easier though)
- ```SLATE_PLUGIN_INIT()``` // Declares `g_api`, and defines both required exports (`slate_api_version` and `slate_plugin_init`) in one line, write your registration code in the block that follows it, exactly like a normal function body

Using some, a plugin function shrinks to:

```cpp
#include "slate_api.h"

SLATE_FN(my_add, 2)
    long long a = g_api->to_int(args[0]);
    long long b = g_api->to_int(args[1]);
    return g_api->make_int(a + b);
SLATE_END

SLATE_PLUGIN_INIT() {
    g_api->bind(env, "myplugin.add", my_add, nullptr);
}
```

Compared to:

```cpp
#include "slate_api.h"

static const SlateAPI* g_api;

extern "C" __declspec(dllexport) SlateValue my_add(SlateValue* args, int argc, void* userdata) {
    if (argc < 2) return g_api->make_null();
    long long a = g_api->to_int(args[0]);
    long long b = g_api->to_int(args[1]);
    return g_api->make_int(a + b);
}

extern "C" __declspec(dllexport) int slate_api_version(void) { return SLATE_API_VERSION; }

extern "C" __declspec(dllexport) void slate_plugin_init(SlateEnv env, const SlateAPI* api) {
    g_api = api;
    g_api->bind(env, "myplugin.add", my_add, nullptr);
}
```

# The Value API #

Every value that crosses the plugin boundary is an opaque `SlateValue` (`void*`). All of these are accessed through the `SlateAPI` table passed to `slate_plugin_init` (`g_api->` in every example on this page).

- ```throw_error(message)``` // Throws a runtime error with the specified message

**Primitives**
- ```make_int(v)``` // Returns a new `SlateValue` holding a 64-bit integer
- ```make_double(v)``` // Returns a new `SlateValue` holding a double
- ```make_string(s, len)``` // Returns a new `SlateValue` holding a string of `len` bytes starting at `s`
- ```make_bool(v)``` // Returns a new `SlateValue` holding a bool (`0` = false, nonzero = true)
- ```make_null()``` // Returns a new `SlateValue` representing Slate's `null`

- ```is_int(v)``` / ```is_double(v)``` / ```is_string(v)``` / ```is_bool(v)``` / ```is_null(v)``` // Type checks, return `0` or `1`

- ```to_int(v)``` // Returns the int value, or `0` if `v` isn't actually an int
- ```to_double(v)``` // Returns the double value, or `0.0` if `v` isn't actually a double
- ```to_bool(v)``` // Returns the bool value as `0`/`1`, or `0` if `v` isn't actually a bool
- ```to_string(v, out_len)``` // Returns a `const char*` to the string's bytes and writes its length to `*out_len`, or an empty string if `v` isn't actually a string. **The returned pointer is only valid until `v` is released**, copy it out immediately if you need to keep it

**Arrays**
- ```array_new()``` // Returns a new, empty array
- ```is_array(v)``` // Returns `1` if `v` is an array, otherwise `0`
- ```array_length(v)``` // Returns the number of elements, or `0` if `v` isn't an array
- ```array_get(v, index)``` // Returns a **new owned copy** of the element at `index`, or `null` if out of range
- ```array_push(v, item)``` // Copies `item`'s value into the array, does **not** take ownership of `item`, you still own and must separately release it
- ```array_set(v, index, item)``` // Copies `item`'s value into the array at `index`, if in range

**Structs**
- ```struct_new(type_name)``` // Returns a new, empty struct tagged with `type_name`
- ```is_struct(v)``` // Returns `1` if `v` is a struct, otherwise `0`
- ```struct_get(v, field)``` // Returns a **new owned copy** of `field`'s value, or `null` if the field doesn't exist
- ```struct_set(v, field, val)``` // Copies `val`'s value into `field`, does **not** take ownership of `val`

**Pointers**
- ```is_pointer(v)``` // Returns `1` if `v` is a non-null pointer, otherwise `0`
- ```pointer_null()``` // Returns a new `SlateValue` representing a null pointer (equivalent to `make_null()`)
- ```deref(v)``` // Returns a **new owned copy** of the value `v` points to, or `null` if `v` isn't a valid pointer or its target has since been deleted from the Slate side
- ```deref_write(v, new_val)``` // Writes `new_val`'s value through the pointer, if `v` is still valid, silently does nothing otherwise
- ```new_ptr(env, val)``` // Allocates a new heap slot holding a copy of `val` and returns a pointer to it, same shape as Slate's own `make()` expression

**Coroutines**
- ```coroutine_create(fn_val)``` // Wraps a `SlateValue` function closure into a new `SlateCoroutine` handle (returns `nullptr` if the value is not a valid closure)
- ```coroutine_resume(co)``` // Resumes the coroutine, running it until its next yield or completion, and returns the yielded or returned `SlateValue`
- ```coroutine_status(co)``` // Returns a string status: `"suspended"`, `"running"`, or `"dead"`
- ```coroutine_is_done(co)``` // Returns `1` if the coroutine has finished or is invalid, otherwise `0`
- ```coroutine_free(co)``` // Frees a dead coroutine's memory. Returns `1` on success, or `0` if attempted on a non-dead coroutine

**Callbacks**
- ```is_callable(v)``` // Returns `1` if `v` is a function or closure, otherwise `0`
- ```call(env, fn_val, args, argc)``` // Invokes a Slate function/closure with an array of `SlateValue` arguments, returning a new owned `SlateValue` result

**Lifetime**
- ```release(v)``` // Frees a `SlateValue`. Every value you construct or extract must eventually be released , see [Ownership rules](#ownership-rules)

# Ownership rules #

- **Constructors** (`make_int`, `array_new`, `struct_new`, `new_ptr`, ...) return an **owned** value, you're responsible for eventually calling `release` on it.
- **Extracting getters** (`array_get`, `struct_get`, `deref`) return a **new owned copy**, not a view, releasing it never affects the container/pointer it came from, and it needs its own `release` too.
- **Setters** (`array_push`, `array_set`, `struct_set`, `deref_write`) **copy the value in**, they never consume or release what you pass them, so you still own it afterward.
- `args` passed into a bound function (`SlateValue* args` in your function) are owned by the caller for the duration of the call, don't release them yourself, and don't hold onto them past the call returning.
- The `SlateValue` your function **returns** is consumed by Slate, don't release it yourself after returning it.

# Full example #

- **Note that you should have more safety checks, this is just a demo showing unrealistic parameters (demo_add would fail with unexpected types and produce weird behavior,** *eg: a struct + struct or class + string, etc*) **passed in with no error checking** 
- **Honestly if you're a plugin dev you should probably make a wrapper on these types, so you dont have to manually release and do alot of the boilerplate**

```cpp
#include "slate_api.h"

/*Macros*/

SLATE_FN(demo_add, 2)
    double result = (double)g_api->to_int(args[0]) + (double)g_api->to_int(args[1]);
    return g_api->make_double(result);
SLATE_END

SLATE_FN(demo_make_array, 0)
    SlateValue arr = g_api->array_new();

    SlateValue a = g_api->make_int(1);
    g_api->array_push(arr, a);
    g_api->release(a);

    SlateValue b = g_api->make_int(2);
    g_api->array_push(arr, b);
    g_api->release(b);

    SlateValue c = g_api->make_int(3);
    g_api->array_push(arr, c);
    g_api->release(c);

    if (argc >= 1 && g_api->is_string(args[0])) {
        SlateValue name = g_api->make_string("plugin says hi", 14);
        g_api->array_push(arr, name);
        g_api->release(name);
    }
    return arr;
SLATE_END

SLATE_FN(demo_make_point, 0)
    SlateValue s = g_api->struct_new("Point");

    SlateValue x = g_api->make_int(10);
    g_api->struct_set(s, "x", x);
    g_api->release(x);

    SlateValue y = g_api->make_int(20);
    g_api->struct_set(s, "y", y);
    g_api->release(y);

    if (argc >= 1 && g_api->is_string(args[0])) {
        g_api->struct_set(s, "label", args[0]);
    }
    return s;
SLATE_END

SLATE_FN(demo_pointer_roundtrip, 1)
    SlateEnv env = (SlateEnv)userdata;

    SlateValue initial = g_api->make_int(42);
    SlateValue ptr = g_api->new_ptr(env, initial);
    g_api->release(initial);

    if (g_api->is_pointer(ptr)) {
        SlateValue doubled = g_api->make_int(g_api->to_int(args[0]) * 2);
        g_api->deref_write(ptr, doubled);
        g_api->release(doubled);
    }

    SlateValue result = g_api->deref(ptr);
    g_api->release(ptr);
    return result;
SLATE_END

SLATE_FN(demo_apply_callback, 2)
    SlateEnv env = (SlateEnv)userdata;
    SlateValue fn_val = args[0];

    if (!g_api->is_callable(fn_val)) {
        g_api->throw_error("First argument must be callable!");
        return g_api->make_null();
    }

    SlateValue cb_args[1] = { args[1] };
    SlateValue result = g_api->call(env, fn_val, cb_args, 1);

    return result;
SLATE_END

SLATE_FN(demo_run_coroutine, 1)
    SlateValue fn_val = args[0];
    if (!g_api->is_callable(fn_val)) {
        g_api->throw_error("Expected a generator function!");
        return g_api->make_null();
    }

    SlateCoroutine co = g_api->coroutine_create(fn_val);
    SlateValue last_result = g_api->make_null();

    while (!g_api->coroutine_is_done(co)) {
        g_api->release(last_result);
        last_result = g_api->coroutine_resume(co);
    }

    g_api->coroutine_free(co);
    return last_result;
SLATE_END

SLATE_PLUGIN_INIT() {
    g_api->bind(env, "demo.add", demo_add, nullptr);
    g_api->bind(env, "demo.make_array", demo_make_array, nullptr);
    g_api->bind(env, "demo.make_point", demo_make_point, nullptr);
    g_api->bind(env, "demo.pointer_roundtrip", demo_pointer_roundtrip, (void*)env);
    g_api->bind(env, "demo.apply_callback", demo_apply_callback, (void*)env);
    g_api->bind(env, "demo.run_coroutine", demo_run_coroutine, nullptr);
}
```

```slate
os.load_plugin("myplugin.dll");

print(demo.add(2, 3));                               // 5
print(demo.make_array("hi"));                        // [1, 2, 3, plugin says hi]

print(demo.make_point("origin"));                    // Point{x: 10, y: 20, label: origin}
print(demo.pointer_roundtrip(21));                   // 42

var double_fn = fn(x) { 
    return x * 2; 
};
print(demo.apply_callback(double_fn, 21));          // 42

var task = fn() {
    yield 100;
    yield 200;
    return 300;
};
print(demo.run_coroutine(task));                     // 300
```
