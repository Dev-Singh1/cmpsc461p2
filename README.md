# Custom Language Parser with Scope and Type Checking

A parser implementation for a custom programming language that implements variable scoping rules and type checking. This project includes a lexical analyzer (lexer) and a parser that enforces variable declaration rules, type compatibility, and block scoping.

## Features

### Type System
- Supports two basic types: `int` and `float`
- Enforces strict type checking between numeric types
- Validates type compatibility in expressions and assignments

### Scoping Rules
- Implements block-level scoping
- Variables must be declared before use
- Prevents variable redeclaration within the same scope
- Allows variable shadowing in nested scopes

### Control Structures
- If-else statements with block scoping
- While loops with block scoping
- Function calls with argument parsing

### Error Detection
- Type mismatch detection
- Undeclared variable usage
- Variable redeclaration in same scope
- Out-of-scope variable access

## Grammar

The parser implements the following grammar:

```
statement ::= assign_stmt | if_stmt | while_stmt | expr_stmt | function_call | decl_stmt
decl_stmt ::= type IDENTIFIER '=' expression
type ::= 'int' | 'float'
if_stmt ::= 'if' boolean_expression '{' block '}' ('else' '{' block '}')?
while_stmt ::= 'while' boolean_expression '{' block '}'
factor ::= NUMBER | FNUMBER | IDENTIFIER | '(' expression ')'
```

## Usage Example

```python
from Parser import Lexer, Parser

# Sample code
code = """
int x = 5
if x > 3 {
    float y = 2.5
    x = 10
}
"""

# Create lexer and tokenize input
lexer = Lexer(code)
tokens = lexer.tokenize()

# Create parser and parse tokens
parser = Parser(tokens)
ast = parser.parse()

# Check parser messages for any errors
for message in parser.messages:
    print(message)
```

## Error Examples

1. Type Mismatch:
```python
int a = 10.2  # Error: Type Mismatch between int and float
```

2. Undeclared Variable:
```python
int a = 10
b = 5  # Error: Variable b has not been declared in the current or any enclosing scopes
```

3. Variable Redeclaration:
```python
int a = 10
int a = 5  # Error: Variable a has already been declared in the current scope
```

4. Scope Violation:
```python
if true {
    int x = 10
}
x = 5  # Error: Variable x has not been declared in the current or any enclosing scopes
```

## Implementation Details

The implementation consists of two main classes:

1. `Lexer`: Handles tokenization of input code
   - Recognizes keywords, operators, identifiers, and literals
   - Distinguishes between integer and floating-point numbers
   - Handles whitespace and basic error detection

2. `Parser`: Implements the parsing logic
   - Maintains symbol table for variable tracking
   - Implements scope management
   - Performs type checking
   - Generates error messages for violations

## Dependencies

- Python 3.x
- No external dependencies required

## Academic Integrity

This project is subject to academic integrity policies. Please ensure you understand and follow your institution's academic integrity guidelines when using or referencing this code.
