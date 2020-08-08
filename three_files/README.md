# battle_c
## NamDohyeon - Team 3
Personal Project #2

# C compile and Execution
Preprocessing, Compile, Link (with library), Loader
# C preprocessor(CPP)

1. CPP can include files.

    - I can use `""` and `<>` for this. <> can be used for standard library.

2. CPP can Define Macro

    -Use `#define` for this. But this is very critical. So I need some practice for this.<br>
    Order Expansion and stringification. Special Macro can be used for searching bug and errorline.

3. CPP can do Conditional Compliation

    -I can compile section by section with `#ifdef` and `#endif`, etc.

4. Line Control

# gcc Compile option(major 6)


1. -c : generate .o file.
    -This is for fast compile.<br>
    If I has very long code but nothing change, I can use this option and compile more faster by  making this code .o file


2. -E : preprocessor.
    -If I include `math.h` in `file.c`, and make `gcc -E file.c` command, <br>
    `math.h` included and `math.h` preprocessing result will be out by stdout.


3. -g : debugging option


4. -O : Optimization. It should be used with optimize level.
    -It cannot be used with -g. If you done this, -O will be turn off.


5. -D : macro define


6. -o : Can send compile result to other file.


Other options, -std, -infile can be used.
Also, with -dM, `#define` can be defined with gcc compile.

Let's see one example. On this shot, printf is wrong on main.c. You can fix func(100) as fun1(100)

# In this file, how I can read func.c on main.c?

![image](/uploads/699f8d16b801fea24a9e467f35ba482b/image.png)



Answer: On C Compile process, there are link process, third chapter.
func1(100) needs link cause its extern int.
So the answer is, we can read this on link process.

If you want compile this, type `gcc main.c func.c` on prompt.

One of the bad habit of new beginner's is write down `#include<stdio.h>` everywhere.
In this code, only main.c needs <stdio.h> cause this code only have standard output.

# three files explanation

MY professor gave me a workout for practice this concept.

![image](/uploads/f4aa3590a685735fc8aeaaeb58aea462/image.png)

## func.h

in header file, I just declare function on here.<br>
Perfectly candid, I don't have to make func.h on here<br> 
if I put `extern int func_name_or_id()` on `func.c`.
But I made this for HW description

<pre>
<code>
//func.h
extern int func_name_or_id();
</code>
</pre>

## func.c

I defined function on here. <br>
And I will use `PRINT_ID` macro for conditional. For this, #ifdef and #endif will work by pair.<br>
If PRINT_ID already defined, print ID. If not, print name.<br>
If I print name, return 1. And for ID, I return 0.

<pre>
<code>
//func.c
#include "func.h"
#include <stdio.h>

int func_name_or_id()
{
    #ifdef PRINT_ID
	printf("ID : 201620921\n");
	return 0;
    #endif
	printf("Name : Nam Do Hyeon\n");
	return 1;
}
</code>
</pre>

## main.c

Nothing special on here. this is for compile. 

<pre>
</code>
//main.c
#include "func.h"
#include <stdio.h>

int main()
{
    func_name_or_id();
}
</code>
</pre>

## Compile 1
1. Type `gcc main.c func.c` on the git bash. 
2. Type `ls` 
    ![image](/uploads/e4e747409d8075480e46ef9298ae133f/image.png)
3. Type `./a.exe`

Result
    ![image](/uploads/6460bb521b618515b330d4b1350a18f7/image.png)

## Compile 2
All things are same, but try `gcc -DPRINT_ID main.c func.c` at first process.

Result
    ![image](/uploads/1a35eb3c417204d252453200648790bc/image.png)

## Why this happen?

What is `-D` option?<br> 
`gcc -DPRINT_ID` means define macro PRINT_ID. By define PRINT_ID macro, ID comes out instead of name.