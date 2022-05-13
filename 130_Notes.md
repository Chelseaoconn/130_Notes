**Blocks** 

<u>Words to know:</u>

1) yield if block_given?  (Kernal#block_given)

2) {|var| } -> var is a block parameter/ a type of local variable scoped to the block
3) Arity- The rule regarding the number of arguments that you must pass to a block, proc, or lambda
   1) Lenient Arity- blocks and procs (you can pass too many or too few arguments to a block)
   2) Strict Arity- lambdas (must pass the exact number of arguments to a block)

​		**Methods enforce the argument count, blocks do not* 

4. Explicit Block- Gets treated as a named object, it gets assigned to a method parameter so that it can be managed like any other object. (Syntax = def method(&block)) #& converts the block argument to a 'simple' Proc object. 

   1. ```ruby 
      def test(&block)
        puts "What's &block? #{block}" #drop & symbol inside the block 
      end
      ```

      

5) #block.call(optional)

   ```ruby 
   def display(block)
     block.call(">>>") # Passing the prefix argument to the block
   end
   
   def test(&block)
     puts "1"
     display(block)
     puts "2"
   end
   
   test { |prefix| puts prefix + "xyz" }
   # => 1
   # => >>>xyz
   # => 2
   ```

6. Proc - Ruby converts blocks passed in as explicit blocks into simple proc object- why we call #call to invoke the Proc object 
7. Closure- chunk of code that you can pass around and execute at some later time 
8. Binding - Surrounding environment/ context - A closure must keep track of its binding   



<u>Testing</u> 

1. Minitest- Rubys default testing library and is part of Ruby's standard library. A bundled gem- shipped with Ruby installation but outside Ruby core library. Another one is called RSpec
2. DSL- Domain Specific Language/ RSpec/ Minitest can also use DSL but also just Ruby 
3. Test Suite- This is the entire set of tests that accompanies your program or application.  You can think of this as all the tests for a specific project. 
4. Test- This describes a situation or context in which tests are run. For example, this test is about making sure you get an error message after trying to log in with the wrong password.  A test can contain multiple assertions. 
5. Assertion- This is the actual verification step to confirm that the data returned by your program or app is what is expected.  You make one or more assertions within a test. 

How to use minitest



1. Assertion/ Assert-style syntax

2. `assert_equal` (testing for value equality and not object equality `==`) therefor we have to have a custom `==` method if we are using `assert_equal`on a custom class

3. `assert_same` (testing for object equality)

   

- In a separate file 

- ```ruby
  require 'minitest/autorun' #loads all files from minitest gem
  
  require_relative 'car' #'car' is the name of the file we're testing 
  
  class CarTest < MiniTest::Test #our test class will inherit all methods from superclass
    def test_wheels #begin instance method with test_
    	car = Car.new 
    	assert_equal(4, car.wheels) #make assertions to verify/ parameters - (expected value, actual value) 
    end
  end
  ```

- When the test is run: 

- ```ruby 
  Run options: --seed 62238
  
  # Running:
  
  CarTest .  #This period means it passed/ "S" means you skipped it/ "F" means failure 
  
  Finished in 0.001097s, 911.3428 runs/s, 911.3428 assertions/s.
  
  1 runs, 1 assertions, 0 failures, 0 errors, 0 skips
  
  ```

- To use colors in Minitest:

- ```ruby 
  require "minitest/reporters"
  Minitest::Reporters.use!
  ```

- To skip a test :

- ```ruby 
    def test_bad_wheels
      skip #use skip keyword optional argument for message
      car = Car.new
      assert_equal(3, car.wheels)
    end
  ```



2. Expection/ Spec-Style syntax/ DSL



- Tests are grouped into describe blocks, and induvidual tests are written with the 'it' method/ no assertions, instead expectation matchers 



- ```ruby 
  require 'minitest/autorun'
  
  require_relative 'car'
  
  describe 'Car#wheels' do
    it 'has 4 wheels' do
      car = Car.new
      _(car.wheels).must_equal 4           # this is the expectation
    end
  end
  ```



<u>Four Steps to Writing a Test</u>



1) Set up the necessary objects

2) Execute the code against the object we're testing

3) Assert the results of the execution

4) Tear down and clean up any lingering artifacts

   

- Use `#setup` to help with redundancy 

- ```ruby 
  def setup 
    @car = Car.new #reference this instance instead of instantiating in every test
  end 
  ```



<u>Code Coverage</u> 



- How much of our actual program ims tested by a test suite. Public/private- only means we have some tests in place for every method 

- in irb `gem install simplecov` 

- ```ruby 
  require 'simplecov'
  SimpleCov.start
  ```




<u>&</u>

- & when applied to an argument object, converts the object to a proc and then a block
- & when applied to a parameter converts the object to a proc (explicit block)
