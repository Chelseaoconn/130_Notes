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

Use the keyword `yield` to yield to block... if no block given then will get `LocalJumpError`. 

Use `Kernal#block_given?` to remedy this. 



Let's look at some lingo: 

```ruby 
# method implementation
def say(words)
  yield if block_given? # block is an implicit parameter and not part of meth. def. 
  puts "> " + words
end

# method invocation
say("hi there") do
  system 'clear'
end                                                # clears screen first, then outputs "> hi there"

#1. Execution starts at method invocation, on line 8.  The say method is invoked with two arguments:N a string and a block(the block is an impicit parameter and not part of the method definition)
#2. Execution goes to line 2, where the method local variable words is assigned the string "hi there". The block is passed in implicitly, without being assigned to a variable.
#3. Execution continues into the first line of the method implementation, line 3, which immediately yields to the block.
#4. The block, line 9, is now executed, which clears the screen.
#5. After the block is done executing, execution continues in the method implementation on line 4. Executing line 4 results in output being displayed.
#6. The method ends, which means the last expression's value is returned by this method. The last expression in the method invokes the puts method, so the return value for the method is nil.
```



*Block parameters/ Block local variable* 

```ruby 
3.times do |num| #block parameter // Within the block `num` is a block local variable scoped to the block
  puts num
end 
```





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

