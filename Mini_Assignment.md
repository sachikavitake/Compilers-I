## Common Options in GCC and LLVM

```
-c
```

This option compiles the source file to object file without linking.

```
-time
```

This option gives the time of individual commands.

```
-glevel 
```

This option specifies the debug level to generate debug information

```
-Olevel
```

This option specifies how much optimization has to be performed ranging from O0, O1, O2, O3, Os, Oz(llvm).

```
-g
```

This options generates the source level debug information

```
-gdrawf<version>
```

This option generates debug information with the specified dwarf version

```
-w
```

This option disables all warning messages

```
-save-temps
```

This options stores the output of all stages of compilation, therefore saves all intermediate results.

## Frontend Support

GCC  has frontends hat supports C, C++, Objective-C, Fortran, Ada, D and Go programming language.

LLVM has frontends that support C, C++, Objective-C, Fortran, Ada, D, Delphi, Haskell, Julia, Rust, and Swift.

## Backend Support

The backend of compiler is responsible for CPU architecture specific optimizations.

On executing the binary for x-86_64,the required output is observed.

For example:

```
#include<stdio.h>
int main()
{
        printf("Backend check\n");
        return 0;
}
```

For the source file, back.c 

```
vi back.c
gcc back.c -o back-x86
./back-x86
```

On executing the above commands, the result is

```
Backend check
```

But on compiling for other architecture, ARM, there is an error;

```
cannot execute binary file: Exec format error
```

This is because the build machine is x86_64 which is why 'Backend check' was printed for that architecture not for others.

## Optimization Level

```
main (void)
{
 int f=0,f0=0,f1=1;
  int i;
  for (i = 1; i <= 1000000; i++)
    {
      f = f0+f1;
      f0=f1;
      f1=f;
    }

  printf ("sum = %d\n", f);
  return 0;
}
```

On running this code for various optimization level:

```
gcc -O<level> main.c
time ./a.out
```

```
clang -O<level> main.c
time ./a.out
```

We get the result that the compilation time taken by O0 is the maximum. At O1 level, the time is is reduced and at level O2 the time decreases even further. At level O3, the time does not reduces much for this code, but for code with much more input values, there is a decrease in time for O3 level.

```
#include <stdio.h>

double powerr(double x, int n)
{
  double r = 1.0;

  for (int j = 1; j <= n; j++)
    r *= x;

  return r;
}

int main ()
{
  double s = 0.0;
  int i;
  
  for (i = 1; i <= 1000000000; i++)
      s += powerr (i, i%10);
    

  printf ("result is %g\n", s);
  return 0;
}
```

On trying different optimizing level on the above code, we see similar result time required for 

O0 > O1 > O2 > O3.

GCC compiler has a optimization level Os for reducing the code size, not focusing on reducing time. Therefore, the time needed for Os level is not significantly reduced but is definitely less than O0 and O1.

LLVM compiler has Os and Oz level, both these levels are used for reducing the code size where Oz is more optimized for reducing size as compared to Os.

Therefore, optimization levels O0,O1,O2,O3 are used for optimizing the time required to compile the code and the optimization levels Os and Oz are used for optimizing the code size.