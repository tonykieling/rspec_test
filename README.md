# RSpec test 
This is a step by step project, based on the link-source bellow, which provided my practice and documentation based on that.
ps. some issues caused by character-format stuff, but, in the end, everything's working. :D

*source: https://semaphoreci.com/community/tutorials/getting-started-with-rspec*


1- create a project's directory
```
  mkdir calculator
  cd calculator
```


2- create the Gemfile with the following content inside it
```ruby
  source 'https://rubygems.org'
  gem 'rspec'
```


3- run the command bellow in order to install the latest version of RSpec and all related dependencies
```
bundle install --path .bundle
```


4- create a dir to wirte tests 
By convention, tests written with RSpec are called “specs” (short for “specifications”) and are stored in the project’s spec directory.
Create that directory in your project too:
```
mkdir spec
```


5- create the file 'spec/string_calculator_spec.rb', content:
```ruby
describe StringCalculator do
end
```


6- To run the specs:
`bundle exec rspec`
It will outup an error due to the uninitialized constant StringCalculator (NameError) error. That’s expected, as we haven’t created that class yet.


7- create a new directory to host our project's classes
```
mkdir lib
```


8- create the file 'lib/string_calculator.rb':
```ruby
class StringCalculator
end
```


9- we should require the file above in our file 'spec/string_calculator_spec.rb':
```ruby
require “string_calculator”

describe StringCalculator do
end
```


10- now the test will pass, but no too much content. It means we are ready to add code.
`bundle exec rspec`


11- 'spec/string_calculator_spec.rb' is suppose to have the code:
```ruby
require_relative '../lib/string_calculator'

describe StringCalculator do
  describe ".add" do
    context "given an empty string" do
      it "returns zero" do
        expect(StringCalculator.add("")).to eql(0)
      end
    end
  end
end
```


12- if we run `bundle exec rspec` we will have an error because the class StringCalculator hasn't have the metho add yet.


13- The simplest thing to do right now is define a the requested method with a simple return, 0.
At lib/string_calculator.rb:
```ruby
class StringCalculator
  def self.add(input)
    0
  end
end
```


14- we can add more examples in our test file 'spec/string_calculator_spec.rb':
```ruby
    context "given 4" do
      it "returns 4" do
        expect(StringCalculator.add("4")).to eql(4)
      end
    end

    context "given 10" do
      it "returns 10" do
        expect(StringCalculator.add("10")).to eql(10)
      end
    end
```


15- In order to fix the code above's errors, we should change the code in our add method, class StringCalculator:
```ruby
def self.add(input)
    if input.empty?
      0
    else
      input.to_i
    end
  end
```


16- to add real add operations, add to the test file ('/spec/string_calculator_spec.rb):
```ruby
...
    context "given 2 and 4" do
      it "returns 6" do
        expect(StringCalculator.add("2,4")).to eql(6)
      end
    end

    context "given 17 and 100" do
      it "returns 117" do
        expect(StringCalculator.add("17,100")).to eql(117)
      end
    end
```


17- and also, change the class file '/lib/string_calculator.rb':
```ruby
def self.add(input)
  if input.empty?
    0
  else
    numbers = input.split(",").map { |num| num.to_i }
    numbers.inject(0) { |sum, number| sum + number }
  end
end
```


18- RSpec has more than one way to display its output. A very popular alternative to the default dot format is the “documentation” format:
`bundle exec rspec --format documentation`

