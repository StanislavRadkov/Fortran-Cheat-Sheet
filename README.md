Fortran Cheat Sheet
===================
This is work in progress. Feel free to contribute :)

## Table of Contents

* [Hello World](#hello-world)
* [Terminology](#terminology)
* [Special Characters](#special-characters)
* [Data types](#data-types)
* [Type Declaration Statements](#type-declaration-statements)
* [User Defined Types](#user-defined-types)
* [Operators](#operators)
* [Arrays](#arrays)
* [Loops](#loops)
* [Control flow](#control-flow)
* [Functions](#functions)
* [Subroutines](#subroutines)
* [Modules](#modules)
* [File I/O](#file-io)
* [Command line arguments](#command-line-arguments)


#### Hello World
``` fortran
program hello
    write(*,*) 'Hello World!'
end
```
#### Terminology
* **Statement** - An instruction which is either executabe or
nonexecutable.
* **Construct** - A sequence of statements ending with a
construct terminal statement.
* **Function** - A procedure that returns the value of a single
variable.
* **Procedure** - Either a function or subroutine. Intrinsic
procedure, external procedure, module procedure, internal
procedure, dummy procedure or statement function.
* **Subroutine** - A procedure that is invoked by a CALL
statement or defined assignment statement. It can return more
than one argument.

#### Special Characters

* **’** (Apostrophe) Editing, declaring a string
* **"** (Quotation Marks) Declaring a string
* **\*** (Asterisk) Comment lines.
* **:** (Colon) Editing.
* **::** (Double Colon) Separator.
* **!** (Exclamation) inline comment.
* **/** (Slash) Skip a line in a fmt statment?
* **;** (Semicolon) Separates Statement on single source line. Except when it is in a character context.
* **&** (Ampersand) Line continuation charachter.

#### Data types
* integer 
* real 
* character
* logical
* complex 

#### Type Declaration Statements

> TODO - expand and add examples

* non_overridable - Declares a bound procedure cannot be overridden in a subclass of this class.
* allocatable - Declares an array is allocatable.
* dimension - Declares the rank and and shape of an array.
* external - Declares that a name is a function external to a pro-gram unit.
* intent - Specifies the intended use of a dummy argument.
* intrinsic - Declares that a name is a specific intrinsic function
* nopass - Declares a bound procedure cannot be overridden in a subclass of this class.
* optional - Declares that a dummey argument is optional.
* parameter - Defines named constant.
* pointer - Declares that a variable is a pointer.
* private - Declares that an object is private to a module.
* protected = Declares that an object in a module is protected, meaning that it can be used but not modified outside the module in which it is defined.
* public - Declares that an object is private to a module.
* save - Declares that an object is private to a module.
* target - Declares that an object is private to a module.
* volatile - Declares that a value of a variable might be changed at any time by some source external to the program.

#### User Defined Types
Definition of a new data type called 'personType':

``` fortran
type :: personType
        character(len=100) :: name
        integer :: age
        real :: weight
end type personType
```

Declare an instance of person type:

``` fortran
type (personType) :: p
```

Access properties:

``` fortran
p%name = 'John Doe'
p%age = 45
p%weight = 70
```

#### Operators
* Arithmetic Operators:

| Priority | Operation | Symbol | FORTRAN Expression | 
| :---: | :---: | :---: | :---: |
| inside to outside | Parentheses | ( ) | A*(A+B) | 
| right to left | Exponentiation | ** | A**B |
| left to right | Multiplication | * | A*B |
| left to right | Division | / | A/B |
| left to right | Addition | + | A+B |
| left to right | Subtraction | - | A-B |
| left to right | Unary Minus | - | -A |
 
#### Arrays
> TODO - Add content

#### Loops
> TODO - Add content

#### Control flow
> TODO - Add content

#### Functions
> TODO - Add content

#### Subroutines
> TODO - Add content

#### Modules
> TODO - Add content

#### File I/O
> TODO - Add content

#### Command line arguments
> TODO - Add content