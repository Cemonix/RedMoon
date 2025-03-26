# RedMoon Grammar Specification

In this document, grammar rules for the RedMoon programming language are defined. The grammar is written in Extended Backus-Naur Form ([EBNF](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) with some modifications such as regular expressions.
 
## Grammar Rules

```ebnf
// Top-level program structure
program = statement* EOF;
statement = declaration | expression ;
declaration = ... ;

// Expressions
expression = assignment ;
assignment = identifier '=' assignment | logical_or ;
logical_or = logical_and (logical_or_op logical_and)* ;
logical_and = equality (logical_and_op equality)* ;
equality = relational (equality_op relational)* ;
relational = additive (relational_op additive)* ;
additive = shift (additive_op shift)* ;
shift = multiplicative (shift_op multiplicative)* ;
multiplicative = unary_expr (multiplicative_op unary_expr)* ;
unary_expr = unary_op* primary ;
primary = identifier | literal | grouping ;
grouping = '(' expression ')' ;

// Operators
shift_op = '<<' | '>>' ;
logical_or_op = '||' ;
logical_and_op = '&&' ;
equality_op = '==' | '!=' ;
relational_op = '<' | '>' | '<=' | '>=' ;
additive_op = '+' | '-' ;
multiplicative_op = '*' | '/' | '%' ;
unary_op = '-' | '!' | '~' '|' | '&' ;

// Basic tokens
literal = integer | float | string | boolean ;
identifier = (letter | '_') (letter | digit | '_')* ;
integer = digit+ ;
float = digit+ '.' digit+ ([eE] [+-]? digit+)? ;
string = '"' [^"]* '"' ;
boolean = 'true' | 'false' ;

// Fundamental elements
letter = [a-zA-Z] ;
digit = [0-9] ;
whitespace = ' ' | '\t' | '\n' | '\r' ;

// Comments (ignored in parsing)
comment = line_comment | block_comment ;
line_comment = '//' [^\n]* '\n' ;
block_comment = '/*' ([^*] | '*' [^/])* '*/' ;
```

This grammar defines all rules in dependency order, from basic elements up to complete expressions. Each section builds upon previously defined rules.

## Operators

| Operator | Description |
|----------|-------------|
| `+`      | Addition    |
| `-`      | Subtraction |
// Add more operators