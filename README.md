Fortran Cheat Sheet
===================
This is work in progress. Feel free to contribute :)

* [TODO](https://github.com/StanislavRadkov/Fortran-Cheat-Sheet/blob/master/TODO.md "TODO")
* [How to contribute](https://github.com/StanislavRadkov/Fortran-Cheat-Sheet/blob/master/Contribute.md "How to contribute")

## Table of Contents

* [Hello World](#hello-world)
* [Terminology](#terminology)
* [Special Characters](#special-characters)
* [Data types](#data-types)
* [Type Declaration Statements](#type-declaration-statements)
* [User Defined Types](#user-defined-types)
* [Operators](#operators)
* [Arrays](#arrays)
* [Array Operations](#array-operations)
* [Implicit variable declaration](#implicit-variable-declaration) 
* [Goto Statements](#goto-statements)
* [Loops](#loops)
* [Control flow](#control-flow)
* [Functions](#functions)
* [Subroutines](#subroutines)
* [Modules](#modules)
* [File I/O](#file-io)
* [Command line arguments](#command-line-arguments)


## Hello World
``` fortran
program hello
    write(*,*) 'Hello World!'
end
```

> Please keep in mind that the language is not case sensitive outside of character literals.

## Terminology
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

## Special Characters

* **’** (Apostrophe) Editing, declaring a string
* **"** (Quotation Marks) Declaring a string
* **\*** (Asterisk) Comment lines.
* **:** (Colon) Editing.
* **::** (Double Colon) Separator.
* **!** (Exclamation) inline comment.
* **/** (Slash) Skip a line in a fmt statment?
* **;** (Semicolon) Separates Statement on single source line. Except when it is in a character context.
* **&** (Ampersand) Line continuation charachter.

## Data types
* integer 
* real 
* character
* logical
* complex 

## Type Declaration Statements

* dimension - Specifies the dimensions (start and end index) of an array.
* common - Common storage area for variables that are in several program units.
* data - Puts initial values into variables.
* non_overridable - Declares a bound procedure cannot be overridden in a subclass of this class.
* parameter - Makes a variable into a constant with a certain value.
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
* protected - Declares that an object in a module is protected, meaning that it can be used but not modified outside the module in which it is defined.
* public - Declares that an object is private to a module.
* save - Declares that an object is private to a module.
* target - Declares that an object is private to a module.
* volatile - Declares that a value of a variable might be changed at any time by some source external to the program.

## User Defined Types
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

## Operators
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
 
* Character Operators:

	* Concatenation	- you can do it by using the '//' operator. 
		```fortran
		write(*,*) 'Concate'//'nation'
		```
	* Substring - string(startingIndex:endIndex)
		```fortran
		character(len=20) :: c = 'substring'
		write(*,*) c(1:3)
		```

* Logical Operators (**in order of precedence**):

| Operator |
| :----: |
| .not. |
| .and. |
| .or. | 

* Relational Operators
	
| Operator | Alternative| Meaning |
| :----: | :----: | :----: |
| .eq. | == | equal to |
| .ne. | /= | not equal to |
| .lt. | < | less than |
| .le. | <= | less than or equal |
| .gt. | > | greater than |
| .ge. | >= | greater than or equal |
| .eqv. |  | equivalent to (for boolean) |
| .neqv. |  | not equivalent to (for boolean) |

## Arrays

Arrays can be up to seven dimensions. They are stored in column major format. This is not
the same as C which is stored in row major format. ([Row-major order](http://en.wikipedia.org/wiki/Row-major_order "Row-major order")). **By default the first index in an array is 1.**

Define an array with starting index -3 and end index 3 using the dimension statement:

```fortran
integer, dimension(-3:3) :: arr
data arr/1,2,3,4,5,5,5/
```

You can use the following syntax for repeated values **count\*repeatedValue**:

```fortran
data arr/1,2,3,4,3*5/
```

Access element:

```fortran
rite(*,*) arr(-2) ! Output: 2
```

Array subset:

```fortran
rite(*,*) arr(-2:2) ! Output: 2 3 4 5 5
```

Define a multidimensional array:

```fortran
integer, dimension(1:3, 1:3) :: arr2
data arr2/1,2,3,4,5,6,7,8,9/

write(*,*) arr2(1,1:3) ! Output: 1 4 7   
write(*,*) arr2(1:3,1) ! Output: 1 2 3
write(*,*) arr2(1:3,1:3) ! Output:  1 2 3 4 5 6 7 8 9
```

## Array Operations

If we want to add two arrays a and b and put the result in c. We may have something like the following piece of code:

```fortran
do i=1,n
  do j=1,n
    c(j,i) = a(j,i) + b(j,i)
  enddo
enddo
```
However in Fortran we can also do the following:
```fortran
c = a + b
```

Most of the intrinsic functions operate component-wise on arrays. m = sin(k) is equivalent to:

```fortran
do i=1,n
  m(i) = sin(k(i))
enddo
```
> Note: c = a*b multplies corresponding elements in A and B. It does NOT do matrix multiplication. There are some intrinic functions for matrix multiplication (matmul) and dot products (dot_product). 

Another example operations on a vector and a scalar:

```fortran
real, dimension(3) :: m
data m/1.0, 2.0, 3.0/

write(*,*) m + 1   ! Output: 2.0 3.0 4.0    
write(*,*) m * 2   ! Output: 2.0 4.0 6.0    
write(*,*) m/2     ! Output: 0.5 1.0 1.5   
write(*,*) sqrt(m) ! Output: 1.00 1.41 1.73
```

## Implicit variable declaration

Back in the 1950s, when Fortran was first developed, memory was very expensive, and because of this, a typical computer might have only a few KB of main memory. So, programmers wanted their Fortran programs to be as short as possible.
Because of this they made variable declaration implicit. A consequence of this is [type inference](http://en.wikipedia.org/wiki/Type_inference "type inference"), this refers to the compiler's ability to deduce the type of the used variable if it has not been declared beforehand.

**This means that when you mistype a character of a variable name the compiler will declare a new variable instead of an error!**

For example:
```fortran
real :: variable = 0
vaIRable = 3 + 5 ! wrong name
write(*,*) variable ! output is 0
```

**You can force explicit variable declaration by either using the "implicit none" statement or by passing a specific parameter to the compiler.**

If you put the "implicit none" statement at the top of this piece of code:

```fortran
implicit none
real :: variable = 0
vaIRable = 3 + 5 !! 
write(*,*) variable
```

You will get a compile time error similar to this:

```fortran
    vaIRable = 3 + 5 ! wrong name
            1
Error: Symbol 'vairable' at (1) has no IMPLICIT type
```

>According to the Fortran language standard unless specified otherwise, all variables starting with letters I, J, K, L, M and N are of type integer. All other are by default of type real. Other data types must be explicitly declared. Those defaults can be overridden by 'implicit TypeName (CharacterRange)' statements. However it is considered a good practice to always use the 'implicit none' statement and explicitly declare all variables! 

## Goto Statements

Goto statements performs a one-way transfer of control to another line of code. A function call normally returns control. Goto statements should be avoided as they can lead to [spaghetti code](http://en.wikipedia.org/wiki/Spaghetti_code 'spaghetti code').

Simple example:

```fortran
n = 2
if(n.eq.2) then
	goto 100
endif

write(*,*) 'This line will not be printed!'

100 write(*,*) 'Hi!'
```

Goto statements can have multiple parameters. 
```fortran
goto (s[, s])e
```
Where 's' is label of an executable statement and 'e' is an expression of type integer which points which label should be used by index. 

Example:

```fortran
n = 3
goto (10, 20, 30, 40), n
 
10 write(*,*) 10
20 write(*,*) 20
30 write(*,*) 30
40 write(*,*) 40
```

Output:
```fortran
30
40
```

## Loops

A loop can be defined using the following syntax:

```fortran
do  variable = startValue, StopValue [, StepValue]       
	one or more statments
end do
```
StepValue is optional. Default value is 1.

Example, where an iteration is skipped:
```fortran
do i = 1, 10, 2
	if (i.eq.5) then
    	cycle ! Skip iteration
    endif

	write(*,*) "i = ", i
end do
```

Output:
```fortran
 i = 1
 i = 3
 i = 7
 i = 9
```

Implied DO loops are DO loops in the sense that they control the execution of some iterative procedure, but are different than DO loops because they do not use the do statement to control the execution. Basically, these loops are a shorthand that was introduced in FORTRAN to provide a method for array initialization and to cut back on the number of lines of code that where required in the program. Example:

```fortran
write (*,*) (i, i=1, 5) ! Output:  1 2 3 4 5
```

## Control flow
If/else statement:

```fortran
if(n.eq.2) then
	write(*,*) 'N is equal to 2'
else
	write(*,*) 'N is not equal to 2'
endif
```

Switch case statement:

```fortran
character(len=1) :: c
c = 'C'

select case (c)
   case ('A')
      write(*,*) 'A'
   case ('B')
      write(*,*) 'B'
   case ('C')
      write(*,*) 'C'
   case ('D')
      write(*,*) 'D'
   case default
      write(*,*) 'Other'
end select
```

## Functions

Defining and calling a function:

```fortran
program functions
  implicit none

  real :: k = 4.5, z = 1.5

  write (*,*) sumNumbers(k,z)
  
  contains
      function sumNumbers(a, b)
          real :: sumNumbers  ! The variable with the same name as the function is the returned value
          real, intent(in) :: a,b ! a and b cannot be modified
          
          sumNumbers = a + b                
      end function sumNumbers
      
end program functions
```

## Subroutines
Subroutines in Fortran do not return a value. Instead they can modify some of their arguments. They must be invoked with the 'call' keyword. The 'intent' statement defines the type of the argument. Input arguments cannot be changed inside the subroutine.


```fortran
real :: k
call sumNumbers(k, 1.0, 3.0)
write (*,*) k ! Output is 4.0

contains
    subroutine sumNumbers(k, z, y)
        real, intent(out) :: k ! Output variable
        real, intent(in) :: z,y ! Input variable
        
        k = z + y
    end subroutine sumNumbers
```

## Modules

Define a module:

```fortran
module vector
    implicit none
    private ! private statement causes all data and subprograms to be hidden
    
    type, public :: vectorType
        integer :: n = 3
        real :: a(3) ! vector component, array
        real :: magnitude
    end type vectorType
    
    interface assignment(=)
        module procedure assignVector
    end interface
    
    public :: magnitude
    
    contains
        subroutine assignVector (left, right)
            type(vectorType), intent(in) :: right
            type(vectorType), intent(inout) :: left
            
            integer :: i
            
            left%n = right%n
            left%magnitude = right%magnitude
            
            do i = 1, right%n
                left%a(i) = right%a(i)
            enddo
            
        end subroutine assignVector
    
        subroutine magnitude (x)
            type(vectorType), intent(inout) :: x
            integer :: i
            
            x%magnitude = 0.0
            do i= 1, x%n ! increment is omitted
                x%magnitude = x%magnitude + x%a(i) * x%a(i)
            enddo 
            
            x%magnitude = sqrt(x%magnitude)
            
        end subroutine magnitude 
    
end module vector
```

Use the module:
```fortran
program modules
    use vector
    implicit none           
    type(vectorType) :: v1,v2
        
    write(*,*) 'Program using modules'
    v1%a(1) = 1.0
    v1%a(2) = 1.0
    v1%a(3) = 0.0
   
    write (*,*) 'Vector magnitude', v1%magnitude

    v2 = v1
    write(*,*) 'Second vector', v2%a
end program modules
```

## File I/O

Write Pi to a file and open the file to check if the content is written as expected.

```fortran
program fileIO
implicit none

    integer :: istat
    real :: a,b
    a = 3.142

    ! open a file
    open(101, file = "out.txt", status = "unknown", action="write", form="formatted", IOSTAT=istat)

    ! check the file
    if( istat /= 0) then
        write (*,*) 'Error opening file'
        return
    endif

    write(101, '(f0.3)') a

    close(101)

    ! open for reading
    open(102, file = "out.txt", status = "old", action="read", form="formatted", IOSTAT=istat)

    ! check the file
    if( istat /= 0) then
        write (*,*) 'Error opening file'
        return
    endif

    read(102, '(f5.3)') b
    write(*, '(f5.3)') b

    close(102)

    write(*,*) 'A is equal to B: ', a.eq.b

end program fileIO
```

## Command line arguments
A simple program to read the passed arguments and print them:

```fortran
program argumentsTest  
     real(8)    :: A,B
     integer :: num_args, ix
     character(len=12), dimension(:), allocatable :: args

     num_args = command_argument_count()
     allocate(args(num_args))  ! Checking the return status of the allocation is omitted
     
     if(.not.allocated(args)) then
        return
     endif

     do ix = 1, num_args
         call get_command_argument(ix,args(ix))
         ! now parse the argument as you wish
     end do
   
     print*, args
end program argumentsTest
```