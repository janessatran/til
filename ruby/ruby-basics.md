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
