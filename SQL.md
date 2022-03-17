# SQL Commands

## User-Defined Variables
- User-defined variables can be declared with `@*var_name*`.
- They are session-specific and are not case sensitive.
- Way to declare user-defined variables is through `SET`.
```
SET @var_name = expr [, @var_name = expr] ...
```
- Assignment operators: `=` or `:=`.

### = and := Operators
- In `SET`, both are assignment operators. 
- In other context, = is a comparison operator.
