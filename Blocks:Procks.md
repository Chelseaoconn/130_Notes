<u>What is a closure?</u> 

Concept that allows you to save a 'chunk of code' for a later time. It binds to surrounding artifacts(variables and names) and builds an enclosure to be referenced at a later time. Closures are implemented through Proc objects, lambdas or blocks. 



<u>Blocks</u>

`do ... end` / `{....}` 

The block is the argument to the method call. Every method can take an optional impicit block. 

```ruby 
def hi 
  puts 'hello'
end 

hi{puts 'hi'} #hello 
```

Use the keyword `yield` to yield to block. 

<u>Proc</u>

A proc object is an encapsulation of a block of code, which can be stored in a local variable, passed to a method or another Proc, and can be called.  They are closures so they can use the entire context in which they were created. Bind to surrounding artifacts.  

Syntax: 

```ruby 
square = Proc.new {|x| x**2} #using Proc class
square.call(3)
square.(3)
square[3]
```

```ruby 
proc2 = proc {|x| x**2 #using Kernal#proc}
```

```ruby 
def make_proc(&block) #converting to a proc with &
  block 
end 

proc3 = make_proc {|x| x**2}
```

