# differ in go lang
The defer statement in Go is a powerful tool for ensuring that cleanup operations are performed, especially in the context of resource management.

Deferred functions are executed in LIFO order just before the surrounding function returns.

The arguments to a deferred function are evaluated at the time the defer statement is executed, not when the deferred function is called.

defer is particularly useful for operations like closing files, unlocking mutexes, and other cleanup tasks that must be performed to avoid resource leaks and ensure proper program behavior.


# example
<!-- package main

import "fmt"

func main() {
    fmt.Println("Start")
    defer fmt.Println("Deferred 1")
    defer fmt.Println("Deferred 2")
    fmt.Println("End")
}


output 
Start
End
Deferred 2
Deferred 1 -->


# using differ for cleanup
<!-- package main

import (
    "fmt"
    "os"
) 
func main() {
    file, err := os.Open("example.txt")
    if err != nil {
        fmt.Println("Error opening file:", err)
        return
    }
    defer file.Close() // Ensure the file is closed when the function returns

    // Perform file operations
    // ...

    fmt.Println("File operations completed")
}-->
# output 

# The file is opened, and if an error occurs, the function returns immediately.
## The defer file.Close() statement ensures that the file will be closed when the function returns, regardless of how it returns.





