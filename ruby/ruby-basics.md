## Ruby Basics

### Conversions
- to get string version of object, write `.to_s` 

The following results in `25`:
```ruby
var1 = 2
var2 = '5'
puts var1.to_s + var2
```

- to get integer version of object, write `.to_i`
- to get float version of object, write `.to_f`

### puts, gets, chomp
- `puts` is used to write an output
  - it uses to `.to_s` method to convert all output into strings
- `gets` is used to get an input from the keyboard
- `chomp` takes off any Enter's hanging out the end of the string input

```ruby
puts 'Hello there, what\'s your name?'
name = gets.chomp
puts 'Your name is ' + name + '? What a lovely name!'
puts 'Pleased to meet you, ' + name + '. :)'
```
Will have the following result:
```ruby
Hello there, and what's your name?
Chris
Your name is Chris? What a lovely name!
Pleased to meet you, Chris. :) 
```

Whereas, using only `gets` will result in: 
```ruby
Hello there, and what's your name?
Chris
Your name is Chris
? What a lovely name!
Pleased to meet you, Chris
. :) 
```

### String Methods
- `reverse`: gives backwards version of a string
- `length`: gives number of characters (including spaces) in the string
- `upcase`: changes every lowercase letter to uppercase
- `downcase`: changes every uppercase letter to lowercase
- `swapcase`: switches the case of every letter in the string
- `capitalize`: switches the first character to uppercase (if it is a letter)
- `center`: adds spaces to the beginning and end of the string to make it look centered; it can take a parameter for lineWidth
- `ljust`: left justify the string
- `rjust`: right justify the string

### Arrays
Declared like `names = ['A', 'B', 'C']
- zero indexed 
- can use the string methods on arrays, but they operate on the elements and not characters
- can call the `each` method on an array object for iteration through each element in array
Example:
```ruby
languages = ['English', 'German', 'Ruby']
languages.each do |lang|
  puts 'I love ' + lang + '!'
  puts 'Don\'t you?'
end
```
Results in:
```ruby
I love English!
Don't you?
I love German!
Don't you?
I love Ruby!
Don't you?
```

- `last` to get last element
- `join` to add string between array's objects
Example:
```ruby
foods = ['cheese', 'donut', 'apple']
puts foods.join(', ')
```
Results in:
```
cheese, donut, apple
```

- `push` to add element to end of array
- `pop` to remove last element of array 


### Some general things
#### Branching
Using the `if` is `true` run code, `if` is `false` do nothing. 

Example:
```ruby
puts 'Hello, what's your name?'
name = gets.chomp
puts 'Hello, ' + name + '.'
if name == 'Belle'
  puts 'What a lovely name!'
end
```
#### Comments
Use a `#` to comment out code

#### Loops
Start with `for` `while`, etc, indent code and end block with `end`
Example:
```ruby
while i < 10
  puts i
  i = i + 1
end
```

#### Methods
- declare a method in between `def` and `end` block
