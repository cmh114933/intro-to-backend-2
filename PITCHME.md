# Intro to Backend Pt2
---
### How do we execute the same block of code multiple times?
---
### Example
+++
Defining a method to calculate a number to the power of n
```ruby
def power(base, n)
  i = 1
  result = base
  while i < n do
    result *= base
    i += 1
  end
  return result
end
```
---
# Recursion
The alternative to loops
+++
### What is it?
Recursion is the way of writing a method that calls itself repeatedly until it reaches a termination condition to solve a problem.

```ruby
def recursive_emthod(arg)
  return if termination condition met
  recursive_method(mutated_arg)
end
```
+++
### Points of note
- A recursive method must have a terminate condition, else it will run indefinitely
- When the method is called within itself, the arguments passed must have changed
---
# What happens?
```ruby
i = 0
while i < 2 do
  p i
end
```
+++
### In iteration, we get infinite loops if the terminate clause can never be met
- The code will run indefinitely, until you manually stop it

How bout in recursion?
+++
### Stack Level Too Deep
+++
### Understanding Stack
+++
```ruby
def power_recursive(base, n, acc)
  return acc if n == 0
  power_recursive(base, n - 1, acc * base)
end

def power(base, n)
  power_recursive(base, n ,1)
end

power(3,3) # => 27
```
+++
```ruby 
  power_recursive(3,3,1) # Stack 1 -> First time run
```
+++
```ruby
  power_recursive(3,2,3) # Stack 2
```
```ruby 
  power_recursive(3,3,1) # Stack 1
```
+++
```ruby
  power_recursive(3,1,9) # Stack 3
```
```ruby
  power_recursive(3,2,3) # Stack 2
```
```ruby
  power_recursive(3,3,1) # Stack 1
```
+++
```ruby
  power_recursive(3,0,27) # Stack 4 -> Last function
```
```ruby
  power_recursive(3,1,9) # Stack 3
```
```ruby
  power_recursive(3,2,3) # Stack 2
```
```ruby
  power_recursive(3,3,1) # Stack 1
```
+++
### Stacks run in a LIFO method
- LIFO (Last In, First Out)
- The lower stacks are waiting for the upper stack to finish execution
- Will only continue to execute when upper stack finishes
+++
```ruby
  power_recursive(3,1,9) # Stack 3 -> Stack 4 returns value to stack  3
```
```ruby
  power_recursive(3,2,3) # Stack 2
```
```ruby
  power_recursive(3,3,1) # Stack 1
```
+++
```ruby
power_recursive(3,3,1)
    power_recursive(3,2,1 * 3) # => acc = 3
        power_recursive(3,1, 3 * 3 ) # => acc = 9
            power_recursive(3,0, 3 * 3 * 3) # => acc = 27
              27
```
+++
### So why stack level too deep?
```ruby
def power_recursive(base, n, acc)
  # return acc if n == 0
  power_recursive(base, n - 1, acc * base)
end

def power(base, n)
  power_recursive(base, n ,1)
end

power(3,3) # => 27
```
+++
### .
### .
### .
```ruby
  power_recursive(3,-1,81) # Stack 5 -> Depth 5
```
```ruby
  power_recursive(3,0,27) # Stack 4 -> Depth 4
```
```ruby
  power_recursive(3,1,9) # Stack 3 -> Depth 3
```
```ruby
  power_recursive(3,2,3) # Stack 2 -> Depth 2
```
```ruby
  power_recursive(3,3,1) # Stack 1 -> Depth 1
```
+++
### Your computer can only maintain a certain number of stacks
### Hence the error: Stack Level Too Deep
---
# Regex
+++
### Ever worked with 
- Credit cards  
-> ```1111 1111 1111 1111```
- Emails 
-> ```test1234@gmail.com```
- Web Sites 
-> ```http://google.com```
- Social Security number 
-> ```111-11-1111```
+++
### Let's break them into patterns
+++
### Breakdown
- Credit cards 
```4 fields of 4 digits with space in between```
- Emails 
```x number of characters + @ symbol + y number of characters + . symbol + z number of characters```
- Websites 
```http:// + any number of characters```
- Social Security Number 
```3 digits + '-' symbol 2 digits + '-' symbol 4 digits```
+++
### What is Regex?
- It means Regular Expression
- It is a pattern describing text that the computer can use to identify and match strings
+++
Example Usage:
1. Use regex to determine whether the provided input is a valid credit card/ email
2. Use regex to capture all credit card numbers in a large text file.
3. Use regex to match portions of credit card I wish to hide (e.g hide first 3 credit card fields)
etc...
+++
### Let's try it out