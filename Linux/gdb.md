# GDB
The **G**NU Project **D**e**B**ugger  
GNU의 기본 디버거이다. GDB를 통해 Stack, Register, Memory등과 같은 정보를 얻을 수 있다.

GDB를 통해 프로그램이 실행되는 동안 프로그램 내에서 진행되고 있는 부분들을 알아볼 수 있다.

### The Latest Version of GDB 
> 현 시점<small>(02.10.2020)</small>의 최신 버전은 9.1

GDB Version : 9.1  
02.08.2020

### GDB 가 Support 하는 언어
* Ada
* Assembly
* C
* C++
* D
* Fortran
* Go
* Objective-C
* OpenCL
* Modula-2
* Pascal
* Rust

## How to Use GDB
GDB 디버거를 사용하기 위해서는 exe 파일로 만들어 주어야 한다.
  * source 파일 자체를 GDB로 돌릴 수 없다.
  * <code>.c</code>, <code>.go</code>, <code>.cpp</code> 와 같은 소스파일 그대로 사용 불가.

### Installation
Homebrew 가 깔려 있다면 아래의 명령어를 입력하자.
```bash
brew install gdb
```

FTB 서버에서 다운
* [링크](http://ftp.gnu.org/gnu/gdb/)

### Compile  
```bash
gcc -g <fileName> -o <outputFileName>
```

* 예를들어 <code>factorial.c</code> 라는 소스파일을 factorial이라는 이름으로 컴파일 하고자 한다면
```bash
gcc -g factorial.c -o factorial 
```
컴파일이 완료되면 <code>outputFileName</code>으로 이름 지어진 <code>Unix executable file</code> 이 생성된다.  <br>
<img width="89" alt="factorial-exe" src="https://user-images.githubusercontent.com/48475824/74133636-5a91d480-4c2c-11ea-964f-c17b837b3799.png">

### Start GDB
```bash
gdb ./<outputFileName>
```

### Commands
### list
* list   
<code>list \<functionName></code>  
지정한 function의 11라인을 출력  
  * <code>list main</code>
  ```c
  // factorial 의 main function 출력의 예
  2
  3	long factorial(int);
  4
  5	// Factorial
  6	int main()
  7	{
  8	    int num;
  9	    long fact;
  10
  11	    printf("Enter a Positive Integer\n");
  ```

### disas  
 <code>disas \<functionName></code>  
 함수를 disassemble. 해당 함수의 어셈블리 코드를 볼 수 있다.  
 문법은 AT&T asm 문법이다.  
  * <code>disas main</code>  
  ```c
  (gdb) disas main
Dump of assembler code for function main:
   0x0000000100000e40 <+0>:	push   %rbp
   0x0000000100000e41 <+1>:	mov    %rsp,%rbp
   0x0000000100000e44 <+4>:	sub    $0x20,%rsp
   0x0000000100000e48 <+8>:	movl   $0x0,-0x4(%rbp)
   0x0000000100000e4f <+15>:	lea    0xfa(%rip),%rdi        # 0x100000f50
   0x0000000100000e56 <+22>:	mov    $0x0,%al
   0x0000000100000e58 <+24>:	callq  0x100000f1e
   0x0000000100000e5d <+29>:	lea    0x106(%rip),%rdi        # 0x100000f6a
   0x0000000100000e64 <+36>:	lea    -0x8(%rbp),%rsi
   0x0000000100000e68 <+40>:	mov    %eax,-0x14(%rbp)
   0x0000000100000e6b <+43>:	mov    $0x0,%al
   0x0000000100000e6d <+45>:	callq  0x100000f24
   0x0000000100000e72 <+50>:	cmpl   $0x0,-0x8(%rbp)
   0x0000000100000e76 <+54>:	mov    %eax,-0x18(%rbp)
   0x0000000100000e79 <+57>:	jge    0x100000e95 <main+85>
   0x0000000100000e7f <+63>:	lea    0xe7(%rip),%rdi        # 0x100000f6d
   0x0000000100000e86 <+70>:	mov    $0x0,%al
   0x0000000100000e88 <+72>:	callq  0x100000f1e
   0x0000000100000e8d <+77>:	mov    %eax,-0x1c(%rbp)
   0x0000000100000e90 <+80>:	jmpq   0x100000eb9 <main+121>
   0x0000000100000e95 <+85>:	mov    -0x8(%rbp),%edi
   0x0000000100000e98 <+88>:	callq  0x100000ed0 <factorial>
   0x0000000100000e9d <+93>:	mov    %rax,-0x10(%rbp)
   0x0000000100000ea1 <+97>:	mov    -0x8(%rbp),%esi
   0x0000000100000ea4 <+100>:	mov    -0x10(%rbp),%rdx
   0x0000000100000ea8 <+104>:	lea    0xf7(%rip),%rdi        # 0x100000fa6
   0x0000000100000eaf <+111>:	mov    $0x0,%al
   0x0000000100000eb1 <+113>:	callq  0x100000f1e
   0x0000000100000eb6 <+118>:	mov    %eax,-0x20(%rbp)
   0x0000000100000eb9 <+121>:	xor    %eax,%eax
   0x0000000100000ebb <+123>:	add    $0x20,%rsp
   0x0000000100000ebf <+127>:	pop    %rbp
   0x0000000100000ec0 <+128>:	retq
End of assembler dump.
  ```

### Exit GDB
GDB에서 Exit하기 위해서는 아래 명령어중 하나를 사용하면 된다.

* 명령어 1  
<code>q</code>+<code>Enter</code>

* 명령어 2  
<code>quit</code>+<code>Enter</code>

* 명령어 3  
<code>ctrl</code>+<code>d</code>

