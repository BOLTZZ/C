# C Basics:
* Datatypes (really similar to Java):
  1. ```int``` - Used for variables that'll store integers. Since they're limited to 4 bytes (32 bits) of information the integer range is between -2<sup>31</sup> and 2<sup>31</sup> - 1.
  2. ```unsigned int``` - unsigned is a <em>qualifier</em> that can be applied to certain types (like int) used to double the range of positive values while disallowing negative values (0 to 2<sup>32</sup> - 1).
  3. ```char``` - Used for variables that store single characters, they can store 1 byte (8 bits) of memory which ranges from -128 to 127. Thanks to ASCII characters (like A, B, C, ...) are mapped to numeric values in the positive range.
  4. ```float``` - Used to store floating point numbers (real numbers) and are limited to 4 bytest (32 bits) of memory. It has 32 bits of precision, limiting its precision.
  5. ```double``` - Similar to floats but uses double precision, 8 bytes (64 bits) of memory, being much more precise.
  6. ```void``` - A type, not data type, functions can have a void type which means they don't return anything and the parameter list (inputs) can be void which means they don't take in an input.
* Like Java, finish a line of code with a semicolon: ```printf("Hello World\n");```. Also, the convention for C files is .c .
* The process of running code is taking in *source code* (Python, Java, C, and more), compiling it using a compiler, and then running it as *machine code* (binary). Clang is a software to convert source code to machine code.
* Strings can be concatenated as so:
```c
#include <cs50.h>
// Above, allows the user of string datatypes since C doesn't have strings.
#include <stdio.h>
// Above, used for the below code:
int main(void){
    // Asks user for name:
    string name = get_string("What's your name?\n");
    // Prints out a greeting to the user using his/her name:
    printf("Hello, %s\n", name);
}
// When compiling the source code make sure to link with cs50 so you can access the get_string() function:
//clang -o personalized hello.c -lcs50
// Above, clang is used to compile source code (hello.c) into machine code (file name = personalized) and link it (-l). Another way to compile:
// make file_name
```
* The place holders, like the one used up above to input the user's name (string), ```printf("Hello, %s\n", name);``` uses %s to input a string. A few other place holders:
  * %c - char
  * %f - float, long
  * %i - int
  * %li - long
  * %s - string
* A neat trick of kind of tricking C into running a function even before its declared is by pasting the function name before the main function (where the below function will be ran):
```c
#include <stdio.h>
//Tricking C into believing it's seen cough() before:
void cough(int n);

//Main function:
int main(void){
  // Calling cough function, 3 times:
  cough(3);
}

//Cough function:
void cought(int n){
  for (i = 0; i <= n; i ++){
    printf("Cough\n");
  }
}
```
# C Syntax:
* If/Else statement:
```c
if (conditional) 
{
  // code
}
else if (conditional) 
{
  // code
} 
else 
{
  // code
}
```
* While loop:
```c
while (conditional)
{
  //code
}
// With increment:
int i = 0;
while (i < 50)
{
  printf("Spaghet");
  i ++;
}
```
* For loop:
```c
for (int i = 0; i < 50, i ++)
{
  printf("Spaghet");
}
```
