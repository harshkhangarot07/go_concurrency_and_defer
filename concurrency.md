# 1 to stop main function to exist before completion of go routine we use time.sleep() and weight group

# we use go keyword for running go routine

# example below using time.Sleep()
 <!-- package main
 import (
    "fmt"
    "time"
 )

 func main(){
    go helloworld()
    go goodbye()
 }


 func helloworld(){
    fmt.println("hellow")
 }

 func goodbye(){
    fmt.println("goodbye")
 } -->

# If we run the above program, it doesn't print anything. This is because the main function got terminated as soon as those two goroutines started executing. So, we can use Sleep which pauses the execution of the main function. It looks like this:
<!-- 
package main

import (
	"fmt"
	"time"
)

func main() {
	go helloworld()
	go goodbye()
	time.Sleep(2 * time.Second)
}

func helloworld() {
	fmt.Println("Hello World!")
}

func goodbye() {
	fmt.Println("Good Bye!")
} -->

# Here's the output:
<!-- $ go run HelloWorld.go 
Good Bye!
Hello World! -->

# the order is not defined ,In the provided Go program, the output of "Hello World!" and "Good Bye!" can appear in any order due to the concurrent execution of the goroutines. The Go runtime scheduler determines the order in which goroutines are executed, and this order is not guaranteed to be the same every time you run the program.

# using sync.WaitGroup
<!-- 
package main 
import (
    "fmt"
    "sync"
)

func main(){
  var wg sync.WaitGroup

  wg.Add(2)
  go helloworld(&wg)
  go goodye(&wg)
  wg.Wait()
}

func helloworld(wg *sync.WaitGroup){
    defer wg.Done()
    fmt.Println("hello world")
}

func goodbye(wg *sync.WaitGroup){
  defer wg.Done()
  fmt.Println("goodbye")
}
 -->


# differ in go lang
The defer statement in Go is a powerful tool for ensuring that cleanup operations are performed, especially in the context of resource management.

Deferred functions are executed in LIFO order just before the surrounding function returns.

The arguments to a deferred function are evaluated at the time the defer statement is executed, not when the deferred function is called.

defer is particularly useful for operations like closing files, unlocking mutexes, and other cleanup tasks that must be performed to avoid resource leaks and ensure proper program behavior.