# Object-oriented programming

## Classes and Methods
**What is an implicit return?**
When the return value of a method is the value return byt he last statement.
```ruby
def implicit_return
  if true
    22
  else
    0
  end
end

# => returns 22
```

**What is a class?**
A blueprint from which objects are created. 

**When should you use a class?**
When your task requires instantiation or keeping track of states (data, knowledge)

**How do you create a class in your script file?**
```ruby
class MyClass
  def initialize; end
end
```
**What is an instance of a class?**
An object.

**What is the difference between the Pascal Case and snake_case styles of naming?**
Pascal Case should be used when naming classes: `MyClass` while snake_case should be used for naming methods `my_method`.

**How do you instantiate a class?**
```ruby
obj = MyClass.new
```
**How do you set the state of your new instance?**
You can pass parameter values if the initialize method accepts them:
```ruby
class Dog
  def initialize(name, breed)
    @name = name
    @breed = breed
  end
end

kody = Dog.new("Kody", "Chihuahua")

```
**What should be done in the #initialize method?**
Setting up initial values for the object.

**What is a class method?**
A method that belongs to the entire class and not just an instance of it. 

**How is a class method different from an instance method?**
It doesn't require craetion of a class instance to by used. 

**How are methods you already know like #count or #sort etc instance methods?**
They are instances of the Array class. 

**What’s the difference between how you declare a class method vs an instance method?**
There are three ways you can define a class method, which I will show below:
```ruby
# First way
class MyClass
  def self.name
    puts 'class method'
  end
end

# Second way 
class MyClass
  class << self
    def name
      puts 'class method'
    end
  end
end

# Third way
class MyClass
  def MyClass.name
    puts 'class method'
  end
end

```
An instance method is declared normally like:
```ruby
class MyClass
  def instance_method
    puts 'i am an instance method!'
  end
end
```
**What’s the difference between how you call a class method vs an instance method?**
You need to instantiate an object before calling an instance method, whereas you don't need an object to call a class method.
```ruby
MyClass.new.instance_method # calls instance_method
MyClass.name # calls the class method
```
**What is an instance variable?**
A variable that belongs to the object of the class.

**What’s the difference between an instance variable and a ‘regular’ variable?**
An instance variable is declared with an `@` before it's name. They also differ in scope.

**What are “getter” and “setter” methods used for?**
They are used to set values of instance variables. 

**What is the difference between a “getter” and a “setter” method?**
getter: sets the value of the instance variable.
setter: gets the value of the instance variable.

**How do you make instance variables readable outside your class? Writeable? Both at the same time?**
You can use `Accessors` in Ruby:
- `attr_reader`: automatically generates a getter method for each given attribute
- `attr_writer`: automatically generates a setter method for each given attribute
- `attr_accessor`: automatically generates a getter/setter method for each given attribute

Example:
```ruby
class Dog
  attr_reader :name, :breed
  
  def initialize(name, breed)
    @name = name
    @breed = breed
  end
end

dog = Dog.new("Kody", "Chihuahua")
puts dog.name # => Kody
puts dog.breed # => Chihuahua
```

**Can a class call its own class methods?**
Yes

**What’s the difference between when you would use a class variable and when you would use a constant?**
You use a class variable when the value may change (like the number of objects instantiated). You use a constant when it doesn't. 

**What’s the difference between a class and a module?**
╔═══════════════╦═══════════════════════════╦═════════════════════════════════╗
║               ║ class                     ║ module                          ║
╠═══════════════╬═══════════════════════════╬═════════════════════════════════╣
║ instantiation ║ can be instantiated       ║ can *not* be instantiated       ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ usage         ║ object creation           ║ mixin facility. provide         ║
║               ║                           ║   a namespace.                  ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ superclass    ║ module                    ║ object                          ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ methods       ║ class methods and         ║ module methods and              ║
║               ║   instance methods        ║   instance methods              ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ inheritance   ║ inherits behaviour and can║ No inheritance                  ║
║               ║   be base for inheritance ║                                 ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ inclusion     ║ cannot be included        ║ can be included in classes and  ║
║               ║                           ║   modules by using the include  ║
║               ║                           ║   command (includes all         ║
║               ║                           ║   instance methods as instance  ║
║               ║                           ║   methods in a class/module)    ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ extension     ║ can not extend with       ║ module can extend instance by   ║
║               ║   extend command          ║   using extend command (extends ║
║               ║   (only with inheritance) ║   given instance with singleton ║
║               ║                           ║   methods from module)          ║
╚═══════════════╩═══════════════════════════╩═════════════════════════════════╝
[source](https://stackoverflow.com/questions/151505/difference-between-a-class-and-a-module)

**When would you use a class but not a module?**
When you need the functionality of state (since you can instantiate different objects) and duplicating that functionality. 

**How does inheritance work?**
Inheritance is when a class inherits behaviors from another class. In Ruby, there is only single inheritance, but there are mixins (using modules in classes)

**Why is inheritance really useful?**
It allows us to extract common behaviors from the parent class, but add new behaviors to the child class. 

**How do you extend a class? What does that mean?**
- extend: mixes in specified module methods as class methods in the target class
```ruby
class Dog
  extend AnimalModule
end
```
**What does #super do? Why use it?**
It calls a parent method of the same name, with the same arguments. If `super()` is called instead of `super`, it passes no arguments. 
