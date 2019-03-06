# Blocks, Procs, and Lambdas

## Blocks
A Ruby block is a bit of code that can be executed. Block syntax uses either `do..end` or curly braces `{}`.
```ruby
[1,2,3].each do |num|
  puts num
end
# ==> prints 1,2,3 on separate lines
```
Blocks can be combined with methods like `.each` and `.times` to execute an instruction for each item in the collection (like Hash or Array).
Note: blocks are not objects so they can't be saved to variables.

#### Yield
Methods that accept blocks can transfer control form calling the method to the block. This is done with the `yield` keyword. 
```ruby
def testing_yield
  puts "We're inside the method!!"
  puts "Yielding to the block..."
  yield
  puts "We're back in the method!"
end

testing_yield { puts "HELLO THERE!" }
```
You can also pass parameters to `yield`. 
```ruby
def double(p)
	yield(4)
end

double(p) {|p| puts p*2}
# ==> 8
```

## Procs
A saved/named block. Good for keeping code DRY (Don't Repeat Yourself) 
```ruby
multiples_of_3 = Proc.new do |n|
  n % 3 == 0
end

print (1..100).to_a.select(&multiples_of_3)
```
#### Proc Syntax
- call `Proc.new` and pass in the block you want to save
- use `&` to conver the proc into a block (since some methods take a block)
```ruby
cube = Proc.new { |x| x ** 3 }
[1, 2, 3].collect!(&cube)
# ==> [1, 8, 27]
[4, 5, 6].map!(&cube)
# ==> [64, 125, 216]

```
You can also use `.call` to call a block
```ruby
hi = Proc.new {puts "Hello!"}
hi.call
# ==> prints to console Hello!
```

To convert symbols to procs, use `&`. The following code maps `&:to_i` over every element of `strings` and turns each string into an integer.
```ruby
strings = ["1", "2", "3"]
nums = strings.map(&:to_i)
# ==> [1, 2, 3]
```

## Lambda
Lambdas are objects and they are functionally similar to procs. They are defined using the following syntax:
```ruby
lambda { |param| block }
```
Differences between a lambda and proc: 
- lambda checks number of arguments passed to it, proc does not
  - lambda will throw an error if you pass the wrong number of arguments
  - proc will ignore unexpected arguments and assign nil to any that are missing
- when a lambda returns, it passes control back to the calling method
  - when a proc returns, it does so immeidatley without going back to the calling method
