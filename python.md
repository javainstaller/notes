## Python Lambda Functions
- Lambda functions are simple anonymous functions, which composes of 
  - the keyword `lambda`
  - a bound variable 
  - a body
- Instead of writing a function 
```
def identity(x):
  return x+1 
```
The function above can be written with `lambda`
```
lambda x:x+1
```
To run the lambda function, use `( )`
```
(lambda x:x+1)(2)
> 3
```
- Lambda functions can be named with no parenthesis
```
add_one = lambda x:x+1
add_one(2)
> 3
```
- Lambda functions can take on multiple variables 
```
full_name = lambda first, last : f'Full name: {first.title()} {last.title()}'
full_name = ('guido', 'van rossum')
> 'Full name: Guido Van Rossum
```
