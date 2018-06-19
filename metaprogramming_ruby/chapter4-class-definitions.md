Class in Ruby is actually regular code that runs.

## Inside Class

You can write any code inside class definition.

```ruby
class MyClass
  puts 'Hello!"
end

# => Hello!
```

## Current Class

Wherever you are in a Ruby program, you always have a current object `self`

```ruby
class MyClass
  # the current class is now MyClass
  def my_methode
    # ... so this is an instance method of MyClass
  end
end
```

```ruby
class MyClass
  def method_one
    def method_two: 'Hello!'; end
  end
end

obj = MyClass.new
obj.method_one 
obj.meethod_two # => 'Hello!'

```
Which class does method_two() belongs to?
The role of the current class is taken by the class of self: MyClass

The Ruby interpreter always keeps a reference to the current class(or moduel). 
All methods defined with def become instance methods of the current class.
When there is no class defined, the `self` is Object.


## class_eval() (alternate, module_eval())

`Module#class_eval()` evaluates a block in the context of an existing class.

```ruby
def add_method_to(a_class)
  a_class.class_eval do
    def m; 'Hello!'; end
  end
end

add_method_to String
"abc".m # => "Hello!"
```
## Class Instance Variables

Class instance variables is defined with obj with `self`, so it's an instance variable of the obj object.
Change the class instance variables in one instance does not affect others instance of the class.


```ruby
class MyClass
  @my_val = 1
  def self.read; @my_var; end
  def write; @my_var = 2; end
  def read; @my_var; end
end

obj = MyClass.new
obj.write
obj.read        # => 2
MyClass.read    # => 1
```

## Class Instance

```ruby
class C
  @@v = 1
end

class D < C
 def my_method; @@v; end 
end

D.new.my_method  # => 1
```
Class instance can be accessed by subclasses and regular instance methods.

**But**, there is a bad habit of surprising you.


```ruby
@@v = 1
class MyClass
  @@v = 2
end

@@v # => 2
```

`@@v` belongs to top level class Object. MyClass inherited from Object, and therefore can access the variable.
Because of unwelcome surprises like the one shown above, most Rubyist nowadays shun **Class Variables** in favor of **Class Instance Variables**

## Singleton Method

Ruby allows you to add a method to a single object.

```ruby
```
