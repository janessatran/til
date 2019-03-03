# Rspec

### Setup
To set up your project to use rspec:
```ruby
rspec --init
```

Navigate to the spec directory and create a new file with '_spec' appended to the file you're testing. 

Create some tests in your spec file:
```ruby
require ('./hello_world.rb')

describe '#greet' do

  it 'greets with hello world' do
    expect(greet).to eq('hello, world!')
  end
  
end
```

### Test Expectations
```ruby
result.should eq 0
result.should_not eq 0
expect(result).to eq 0
expect(result).not_to eq 0
```
#### Numeric
```ruby
expect(result).to be > 10
expect(result).to == 10

value = 15
expect(result).to equal value

expect(result).to be_between(0,5)
expect(result).to be_within(0.1).of value
```

#### Objects
```ruby
expect(obj).to be_a Class
expect(obj).to be_a_kind_of Class
```

#### Comparisons
```ruby
expect(x). to be 10
expect(x).to satisfy {|x| x < 10 }
expect(x).to match /regexp/
```


