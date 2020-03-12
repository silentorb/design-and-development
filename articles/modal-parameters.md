
## Modal Parameters

A parameter falls within a spectrum of aribitrary to modal.  A parameter is arbitrary when a function will follow the same code path regardless of the value of the parameter.  A parameter is modal when a function will branch into different code paths depending on the value of the parameter.  The more significant the branching, the more the parameter becomes a modal parameter.

### Example: A function with an arbitrary parameter

```
foo(value) {
    return value + 1
}
```

Note that under the hood the underlying assembly and CPU operations could involve significant branching on similar looking addition operations.
 
### Example: A function with an arbitrary and a modal parameter 

```
foo(value, mode) {
    if (mode == 'AlwaysZero')
        return 0
    else
        return value + 1
}
```

Consider the following pseudo code.

```
foo(arg, toggle) {
    if (toggle == 1) {
        // Do A
    }
    else {
        // Do B
    }

    // Do more stuff
}
```

Here we have a function that is essentially three functions crammed into one.  The ```toggle``` parameter configures how the function operates.  That might not look like much of a problem, but
it breaks separation of concern, in that ```block A``` and ```block B``` are tightly coupled to each other and the ```toggle``` parameter.

The problem becomes accentuated when additional functionality is needed:

 ```
 foo(arg, toggle, second_toggle) {
     if (which == 1) {
         // Do A
     }
     else {
        if (second_toggle) {
            // Do B
        }
        else {
            // Do C
        }
     }

     // Do more stuff
 }
 ```

Now things are starting to get cramped.  This reliance on modal configuration does not scale.
```
foo(arg) {
    // Do A
    more_stuff(arg)
}

foo2(arg) {
    // Do B
    more_stuff(arg)
}

more_stuff(arg) {
  // Do more stuff
}
```

The second version is better.  Why?  Because it is more composable, has better separation of concerns, and can scale infinitely.
