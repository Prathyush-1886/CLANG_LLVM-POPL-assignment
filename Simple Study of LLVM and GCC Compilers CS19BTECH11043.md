# Simple Study of LLVM and GCC Compilers

**Repository:** https://github.com/Prathyush-1886/CLANG_LLVM-POPL-assignment

## Options for GCC and LLVM

Taking a common code ( test.c ) to explain the respective options where ever required.

```c
#include<stdio.h>  
int main()
{
	int i;
	for(i=0;i<5;i++)
	{
		printf("%d ",i);
	}
	return 0;
}
```

## Options of GCC

- **-o  choice  :**

    This command is know as output file option. It compiles the input program file and generates the output(executable) file with the name given as input (choice), this output(executable) file can now be executed with the command ./choice .

    ```jsx
    gcc test.c -o test    //to generate the output(executable) file
    ./test                //used to run the code
    ```

    ```c
    Output:
    0 1 2 3 4 
    ```

- **-x    language  :**

    This command allows us to specify the language of the following files so that the compiler need not choose a default based on the file name suffix. This language persists till the next call of 

    -x language or -x none.

    Where language can be C, C++, assembler, ada etc.

- **-x none  :**

    This commands ends the specification that had been mentioned previously while operating the command line and the files are handled according to their respective suffixes. This helps to end the call to any previous -x language

- **-Wall  :**

    This is  a very interesting option that helps to check for any errors within the program but also generates warning in the case of any unused variables.

    If we slightly modify the test.c code.

    ```c
    #include<stdio.h>  
    int main()
    {
  	int m;
  	int i;
  	for(i=0;i<5;i++)
  	{
  		printf("%d ",i);
  	}
  	return 0;
    }
    ```

    upon compiling this program using 

    ```c
    gcc -Wall test.c -o test

    Output:

    test.c: In function ‘main’:
    test.c:4:7: warning: unused variable ‘m’ [-Wunused-variable]
       int m;
    ```

    This compilation procedure generates an error as we had declared a variable m in the main function but hadn't used it anywhere.

    This command just generates a warning for the user and doesn't stop the program from compiling , the usage of -Wall during compilation is considered to be a good practice.

- **-l  and -lm  :**

    The -l option in the command line is used for linking a specific library during a program's compilation so that functions from that library can be used in the program, while on the other hand -lm option is a more specific one that links the math.h library.

    ```c
    gcc test.c -o test -lm
    ```

- -c

    This option compiles the given program and generates its object file as an output, this object file can later be used to make libraries.

    ```c
    gcc -c test.c

    result:
    generates the file test.o (object file) in the same directory
    ```

## Options of LLVM

- lli command

    This command directly executes the programs in the LLVM bitcode format , it take the program given in LLVM bitcode format and runs it using a JIT( just in time)  compiler or an interpreter.

    Few  of the options under ' lli ' are :

    - -time-passes

        This options records the time that was taken for each code generation pass  and prints this value in the standard error output.

        ```c
        lli -time-passes filename.dc
        ```

    - -version

        This option just prints the version of the ' lli ' and exits without doing anything else.

        ```c
        lli -version
        ```

- -o choice :

    This command is know as output file option. It compiles the input program file and generates the output(executable) file with the name given as input (choice), this output(executable) file can now be executed with the command ./choice .

    ```jsx
    clang test.c -o test    //to generate the output(executable) file
    ./test                //used to run the code
    ```

    ```c
    Output:
    0 1 2 3 4 
    ```

- -Wall :

    This is  a very interesting option that helps to check for any errors within the program but also generates warning in the case of any unused variables.

    If we slightly modify the test.c code.

    ```c
    #include<stdio.h>  
    int main()
    {
    	int m;
    	int i;
    	for(i=0;i<5;i++)
    	{
    		printf("%d ",i);
    	}
    	return 0;
    }
    ```

    upon compiling this program using 

    ```c
    clang -Wall test.c -o test

    Output:

    test.c:4:7: warning: unused variable 'm' [-Wunused-variable]
                    int m;
                        ^
    1 warning generated.
    ```

    This compilation procedure generates an error as we had declared a variable m in the main function but hadn't used it anywhere.

    This command just generates a warning for the user and doesn't stop the program from compiling , the usage of -Wall during compilation is considered to be a good practice.

- -c :

    This option compiles the given program and generates its object file as an output, this object file can later be used to make libraries.

    ```c
    clang -c test.c

    result:
    generates the file test.o (object file) in the same directory
    ```

- -v :

    this option prints the commands that had been executed during the stages of compilation in the standard error output . This option also prints the versions of the compiler driver program as well as the  preprocessor.

    ```c
    clang test.c -o test -v

    output:
    clang version 7.0.0 (git@github.com:apple/swift-clang.git 5c9d04dc0697297a47b5edb0c1a581b306a42bdb) (git@github.com:apple/swift-llvm.git 34250a6eef79ee8a83c5cfb4deb1583176dcbb63)
    Target: x86_64-unknown-linux-gnu
    Thread model: posix
    InstalledDir: /usr/bin
    Found candidate GCC installation: /usr/bin/../lib/gcc/x86_64-linux-gnu/7
    Found candidate GCC installation: /usr/bin/../lib/gcc/x86_64-linux-gnu/7.5.0
    Found candidate GCC installation: /usr/bin/../lib/gcc/x86_64-linux-gnu/8
    Found candidate GCC installation: /usr/lib/gcc/x86_64-linux-gnu/7
    Found candidate GCC installation: /usr/lib/gcc/x86_64-linux-gnu/7.5.0
    Found candidate GCC installation: /usr/lib/gcc/x86_64-linux-gnu/8
    Selected GCC installation: /usr/bin/../lib/gcc/x86_64-linux-gnu/8
    Candidate multilib: .;@m64
    Selected multilib: .;@m64
     "/usr/bin/clang-7" -cc1 -triple x86_64-unknown-linux-gnu -emit-obj -mrelax-all -disable-free -main-file-name test.c -mrelocation-model static -mthread-model posix -mdisable-fp-elim -fmath-errno -masm-verbose -mconstructor-aliases -munwind-tables -fuse-init-array -target-cpu x86-64 -dwarf-column-info -debugger-tuning=gdb -v -resource-dir /usr/lib/clang/7.0.0 -I/home/runner/.apt/usr/include -I/home/runner/.apt/usr/include/x86_64-linux-gnu -internal-isystem /usr/local/include -internal-isystem /usr/lib/clang/7.0.0/include -internal-externc-isystem /usr/include/x86_64-linux-gnu -internal-externc-isystem /include -internal-externc-isystem /usr/include -fdebug-compilation-dir /home/runner/Checks -ferror-limit 19 -fmessage-length 72 -fobjc-runtime=gcc -fdiagnostics-show-option -fcolor-diagnostics -o /tmp/test-45147b.o -x c test.c -faddrsig
    clang -cc1 version 7.0.0 based upon LLVM 7.0.0svn default target x86_64-unknown-linux-gnu
    ignoring nonexistent directory "/home/runner/.apt/usr/include"
    ignoring nonexistent directory "/home/runner/.apt/usr/include/x86_64-linux-gnu"
    ignoring nonexistent directory "/include"
    #include "..." search starts here:
    #include <...> search starts here:
     /usr/local/include
     /usr/lib/clang/7.0.0/include
     /usr/include/x86_64-linux-gnu
     /usr/include
    End of search list.
    "/usr/bin/ld" -z relro --hash-style=gnu --eh-frame-hdr -m elf_x86_64 -dynamic-linker /lib64/ld-linux-x86-64.so.2 -o a.out /usr/bin/../lib/gcc/x86_64-linux-gnu/8/../../../x86_64-linux-gnu/crt1.o /usr/bin/../lib/gcc/x86_64-linux-gnu/8/../../../x86_64-linux-gnu/crti.o /usr/bin/../lib/gcc/x86_64-linux-gnu/8/crtbegin.o -L/usr/bin/../lib/gcc/x86_64-linux-gnu/8 -L/usr/bin/../lib/gcc/x86_64-linux-gnu/8/../../../x86_64-linux-gnu -L/usr/bin/../lib/x86_64-linux-gnu -L/lib/x86_64-linux-gnu -L/lib/../lib64 -L/usr/lib/x86_64-linux-gnu -L/usr/bin/../lib/gcc/x86_64-linux-gnu/8/../../.. -L/usr/bin/../lib -L/lib -L/usr/lib /tmp/test-502d29.o -L/home/runner/.apt/usr/lib/x86_64-linux-gnu -L/home/runner/.apt/usr/lib/i386-linux-gnu -L/usr/local/lib -L/home/runner/.apt/usr/lib -lstdc++ -lm -lgcc_s -lgcc -lc -lgcc_s -lgcc /usr/bin/../lib/gcc/x86_64-linux-gnu/8/crtend.o /usr/bin/../lib/gcc/x86_64-linux-gnu/8/../../../x86_64-linux-gnu/crtn.o
    ```

- -Werror

    This option is used to compile the given program and shows a warning if there are any errors present in the program , here -W stands for warnings.

    ```c
    clang -Werror test.c -o test 
    ```

- -ftime-report

    This option is used to print the time summary of each stage during the compilation process in the standard error output.

    ```c
    clang -ftime-report test.c -o test

    output:

    ===-------------------------------------------------------------------------===
                             Miscellaneous Ungrouped Timers
    ===-------------------------------------------------------------------------===

       ---User Time---   --System Time--   --User+System--   ---Wall Time---  --- Name ---
       0.0016 ( 27.7%)   0.0000 (  0.0%)   0.0016 ( 25.8%)   0.0115 ( 69.0%)  LLVM IR Generation Time
       0.0042 ( 72.3%)   0.0004 (100.0%)   0.0047 ( 74.2%)   0.0052 ( 31.0%)  Code Generation Time
       0.0058 (100.0%)   0.0004 (100.0%)   0.0063 (100.0%)   0.0167 (100.0%)  Total

    ===-------------------------------------------------------------------------===
                              Clang front-end time report
    ===-------------------------------------------------------------------------===
      Total Execution Time: 0.0152 seconds (0.0258 wall clock)

       ---User Time---   --System Time--   --User+System--   ---Wall Time---  --- Name ---
       0.0148 (100.0%)   0.0004 (100.0%)   0.0152 (100.0%)   0.0258 (100.0%)  Clang front-end timer
       0.0148 (100.0%)   0.0004 (100.0%)   0.0152 (100.0%)   0.0258 (100.0%)  Total
    ```

With respect to the sets of options available for the warning messages both LLVM and GCC have highly disjoint sets of these options.

The LLVM compilers share a majority of their optimization flags with their GCC counterparts for the languages C and C++.

The command functions and their syntax are as follows :

- The module avail <compiler> command lists all the available version of the respective compiler

```jsx
module avail gcc          //command for GCC
module avail llvm        //command for LLVM
```

- The module load <compiler>/version loads a specific version of the compiler

```jsx
module load gcc/10.2.0      //command to load GCC version 10.2.0
module load llvm/9.0.1      //command to load LLVM version 9.0.1
```

- The compiler commands for compiling a respective language code are quite similar ( in format)

```jsx
gcc              //GCC command for compiling C files
g++              //GCC command for compiling C++ files
clang            //LLVM command for compiling C files
clang++          //LLVM command for compiling C++ files
```

- The commands to access the respective manual once their respective modules have been loaded

```jsx
man g++
man clang
```

The optimization flags for both LLVM and GCC are also common while there are few that exclusive for either one of them. The common flags along with their short descriptions are as follows:

- -O0 :  default optimizer.
- -O1/ -O : This command is to perform an optimized compile
- -O2 :  This compilation option is more optimized than the -O option is generally preferred for

              most of the codes 

- -O3 :  This is more aggressive than -O2 and has higher compile times. It is preferred for

              programs that loop involving intensive floating point calculations. 

- -Os : This is an optimization for the code size.

       

    ```cpp
    //the syntax for all of these command lines is
    gcc test.c -o test -O<level>
    clang test.c -o test -O<level>
    /*  Where the level refers to 0,1,2,3,s    */
    ```

## Frontends Supported

The front end of a compiler is another term used for the analysis phase of the compiler which consists of reading the source program and then checking it for syntax, lexical and grammatical errors. The final result of this phase is an intermediate between the source code and the symbol representation that will be fed to the synthesis phase (back end) as input to generate the  machine code.

### LLVM:

The various languages supported by the front ends for LLVM are:

- Ada
- C
- C++
- D
- Delphi
- Fortran
- Haskell
- Julia
- Objective C
- Rust
- Swift

Few of the front ends are still in the development process, these include the front ends for the languages:

- Java bytecode
- Common Intermediate language
- MacRuby

etc.

### GCC:

The distribution of GCC contains front ends for a various number of languages, few of them already implemented in  the main distribution while few of them are still works in progress. The ones included in the main distribution are for :

- C  (gcc)
- C++(g++)
- Objective C
- Fortran
- ADA (GNAT)
- Go
- D

Few of the works that are still in progress or slightly mature but have not yet been implemented in the main distribution are:

- GHDL, a front end for the hardware design language VHDL
- GCC Unified Parallel C, is a frontend in works for the language Unified Parallel C

etc.

## Generating code for Various Architectures:

The backend of a compiler is one of its most important components who main aim is to produce low level codes that are meant to be executed in specific environments i.e. for specific computer architectures. As these different architectures tend to have different capabilities, the backend works to do further optimization  thereby allowing us to generate binary files for different architectures while working on the a computer with a given architecture i.e. cross compilation.

The code being converted is a very simple hello world code written in C.

```c
#include<stdio.h>

int main()
{
	printf("Hello World !!\n");
	return 0;
}
```

The codes were generated for the following architectures and generated the following result upon attempt to run the binary file. The cross compilation was done from x86_64 to the other computer architectures.(My system has x86_64 architecture)

(The word output: has been used to just separate the output by the terminal from the command line)

### x86_64

The respective command line input and output are as follows

```cpp
gcc Helloworld.c -o Helloworld-x86_64  
./Helloworld-x86_64

output:
Hello World !!
```

Running the file command line to check the architecture for which the binary was made 

```cpp
file Helloworld-x86_64

output:
Helloworld-x86_64: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=a3a904551de1dd3b047781407c16132a363b25b3, for GNU/Linux 3.2.0, not stripped
```

### Arm 32bit

The respective command line input and output are as follows

```cpp
arm-linux-gnueabi-gcc Helloworld.c -o Helloworld_arm
./Helloworld_arm

output:
bash: ./Helloworld_arm: cannot execute binary file: Exec format error
```

Running the file command line to check the architecture for which the binary was made 

```cpp
file Helloworld_arm

output:
Helloworld_arm: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.3, BuildID[sha1]=c0726c493422c4d02374272c2636c6acefb83087, for GNU/Linux 3.2.0, not stripped
```

### Arm 64bit

The respective command line input and output are as follows

```cpp
aarch64-linux-gnu-gcc Helloworld.c -o Helloworld-aarch64
./Helloworld-aarch64

output:
bash: ./Helloworld-aarch64: cannot execute binary file: Exec format error
```

Running the file command line to check the architecture for which the binary was made 

```cpp
file Helloworld-aarch64

output:
Helloworld-aarch64: ELF 64-bit LSB shared object, ARM aarch64, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux-aarch64.so.1, BuildID[sha1]=7b1ebe9c85fbc56b15d8159b13a32dab1c909465, for GNU/Linux 3.7.0, not stripped
```

### MIPS

The respective command line input and output are as follows

```cpp
mips-linux-gnu-gcc Helloworld.c -o Helloworld-mips
./Helloworld-mips

output:
bash: ./Helloworld-mips: cannot execute binary file: Exec format error
```

Running the file command line to check the architecture for which the binary was made 

```cpp
file Helloworld-mips

output:
Helloworld-mips: ELF 32-bit MSB executable, MIPS, MIPS32 rel2 version 1 (SYSV), dynamically linked, interpreter /lib/ld.so.1, BuildID[sha1]=e80f2ec02226fe8841cfc2678214843366c6df77, for GNU/Linux 3.2.0, not stripped
```

From the above result we observe that since the system's architecture is x86_64 it generates an error whenever we try to run a binary file created for another architecture.

## Optimization Results:

The result were obtained on the code  Factorial.cpp which generates the factorials of the first 30 numbers (starting form 0).

```cpp
//Factorial.cpp
#include<iostream>
using namespace std;
int factorial(int x);
int main()
{
	auto begin = chrono::high_resolution_clock::now();
	int a=30;
	while(a>0)
	{
		cout<<factorial(10-a)<<endl;
		a--;
	}
	auto end = chrono::high_resolution_clock::now();
	cout<<chrono::duration_cast<chrono::microseconds>(end-begin).count()*(1e-3)<<"  milliseconds"<<endl;
	return 0;
}
int factorial(int x)
{
	if(x==0)
	{
		return 0;		
	}
	int prod=1;
	int i;
	for(i=2;i<=x;i++)
	{
		prod=prod*i;
	}
	return prod;
}
```

The optimization results have been  generated for the commands -O0, -O1, -O2, -O3 and -Os  only the times have been recorded.

### -O0:

GCC Results:

```cpp
g++ Factorial.cpp -o Fact -O0
./Fact

output:  0.864  milliseconds
```

LLVM Results:

```cpp
clang++ Factorial.cpp -o Fact -O0
./Fact

output: 0.926 milliseconds
```

### -O1:

GCC Results:

```cpp
g++ Factorial.cpp -o Fact -O0
./Fact

output:0.67  milliseconds
```

LLVM Results:

```cpp
clang++ Factorial.cpp -o Fact -O0
./Fact

output:0.643 milliseconds
```

### -O2:

GCC Results:

```cpp
g++ Factorial.cpp -o Fact -O0
./Fact

output:0.305 milliseconds
```

LLVM Results:

```cpp
clang++ Factorial.cpp -o Fact -O0
./Fact

output: 0.348 milliseconds
```

### -O3:

GCC Results:

```cpp
g++ Factorial.cpp -o Fact -O0
./Fact

output:0.23 milliseconds
```

LLVM Results:

```cpp
clang++ Factorial.cpp -o Fact -O0
./Fact

output:0.208 milliseconds
```

### -Os:

GCC Results:

```cpp
g++ Factorial.cpp -o Fact -O0
./Fact

output:0.797 milliseconds
```

LLVM Results:

```cpp
clang++ Factorial.cpp -o Fact -O0
./Fact

output:0.892 milliseconds
```

From the above reading we clearly infer that the execution times for the respective optimization  options follows the following pattern:

-O3< -O2 < -O1 < -Os  < -O0
