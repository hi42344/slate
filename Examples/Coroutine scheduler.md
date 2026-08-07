```cpp
// Non optimized, you'd use a priority queue or min-heap for better performance 
class coroutine_scheduler {
    private:
        //making the array of coroutines
        var coroutines = [];
        
        fn delete_all() {
            for(var i = 0; i < this.coroutines.length; i += 1) {
                // if the coroutine is done we can free it
                if(coroutine.is_done(this.coroutines[i].co)) {
                    coroutine.free(this.coroutines[i].co);
                }
                // else we will wait until it finishes and free it
                else {
                    while(!coroutine.is_done(this.coroutines[i].co)) {
                        coroutine.resume(this.coroutines[i].co);
                    }
                    coroutine.free(this.coroutines[i].co);
                }
                delete this.coroutines[i];
            }
            delete this;
        }
    public:
        //Destructor  
        !coroutine_scheduler() {
            this.delete_all();
        }
        
        fn sleep(seconds) {
        //wake time is the current time + amount of seconds
            var wake_at = os.time() + seconds;
            yield wake_at; 
        }
        
        fn new(function) {
        //creating a coroutine
            struct task { var co = null; var wake_at = 0; }
            var coroutine_ = coroutine.create(function);
            var t = task(coroutine_, 0);
        //pushing it into the coroutines array
            this.coroutines.push(t);
        }

        fn run(seconds) {
            if(this.coroutines.length <= 0) { return false; }
            var stop_at = os.time() + seconds;

            while (os.time() < stop_at) {
                var current_time = os.time();
                //looping over all the coroutines
                for(var i = 0; i < this.coroutines.length; i += 1) {
                    var task_ = this.coroutines[i];

                    //resuming if the coroutine is not done
                    if(!coroutine.is_done(task_.co)) {
                        //making sure the sleep is done
                        if (current_time >= task_.wake_at) {
                            //resuming and getting the new wake time
                            var yield_val = coroutine.resume(task_.co);
                            //setting the task's wake_at to the new wake time
                            task_.wake_at = yield_val;
                        }
                    }
                    //else we free the coroutine and delete the task and remove it from the array
                    else {
                        coroutine.free(task_.co);
                        delete task_;
                        this.coroutines.remove(i);
                    }
                }
                if(this.coroutines.length <= 0) { return false; }
            }
            return true;
        }
        //same thing as run(seconds) but just runs the whole time
        fn run_until_done() {
            if(this.coroutines.length <= 0) { return false; }
            
            while(this.coroutines.length > 0) {
                var current_time = os.time();
                
                for(var i = 0; i < this.coroutines.length; i += 1) {
                    var task_ = this.coroutines[i];
                    
                    if(!coroutine.is_done(task_.co)) {
                        if (current_time >= task_.wake_at) {
                            var yield_val = coroutine.resume(task_.co);
                            task_.wake_at = yield_val;
                        }
                    }
                    else {
                        coroutine.free(task_.co);
                        delete task_;
                        this.coroutines.remove(i);
                    }
                }
            }
            return true;
        }
}

//Using this:
//making the scheduler
var coroutines = coroutine_scheduler();
//adding functions:
coroutines.new(fn() {
    while(!input.is_key_down("escape")) {
        print("hello coroutine 1");
        //if a coroutine ever has a infinite while loop with no sleep or yield then it will just run forever (coroutines are single threaded)
        yield 0;
    }
});

coroutines.new(fn() {
    while(!input.is_key_down("escape")) {
        print("hello coroutine 2");
        yield 0;
    }
});
//running them
coroutines.run_until_done();
```
