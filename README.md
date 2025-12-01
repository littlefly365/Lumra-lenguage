# 🌙 Lumra — A Minimal Programming Language

Lumra is an experimental, lightweight, C-inspired programming language focused on simplicity, low-friction syntax and automatic code expansion.
Its goal is to provide a clean, beginner-friendly syntax that compiles down to ANSI C, allowing portability, clarity and extremely small binaries.



# ✨Features

Clean, minimal syntax

No semicolons required

Simple variable definition:

def word = hello
def num = 13


Functions without boilerplate

func help {
    print "the word is %word"
    print "the number is %num"
}

Automatic includes
Standard headers are injected only when needed.

start → main
Programs begin with a simple:

start
    help

# C output
Lumra code is expanded into C and then compiled normally.

# Extremely simple toolchain
The compiler/wrapper is intentionally small (initially written in Bash, later in C).

# Example Program
hello.lu

def word = hello
def num = 3

func help {
    print "the word is %word"
    print "the number is %num"
}

start
help

# Converted C output (simplified):
hello.c

#include <stdio.h>

char word = hello
int num = 3

void help() {
    printf("the word is %s\n", word);
    printf("the number is %d\n", num);
}
int main(){
help();
}

# 🛠 Compiler / Wrapper

The current Lumra implementation uses a simple converter that:

1. Reads .lu files


2. Expands Lumra syntax into valid C


3. Injects #include directives depending on features


4. Appends semicolons automatically


5. Builds using gcc or clang



As the project evolves, Lumra will move toward a dedicated parser/lexer implemented in C.

# 📦 File Extensions

.lu — Lumra source code

.lh — Lumra headers / includes

# 📜 License

Lumra is released under the BSD 3-Clause License, allowing:

Free commercial and private use

Modifications and redistribution

Minimal requirements

Only attribution needed


This keeps the language open while allowing flexibility in forks, tooling and experimental research.

