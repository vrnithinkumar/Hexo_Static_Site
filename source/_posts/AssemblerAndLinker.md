---
title: Assembler And Linker
date: 2016-08-01 15:05:32
subtitle: " \" An simple effort to understand Assembler and Linker \""
author: "Nithin VR"
header-img: "StandUp_760_348.png"
catalog: true
tags: 
    -ASM
    -Assembler
    -Linker    
    -Loader
---
 
## Introduction

Between compiling and executing a High-Level programming language, Many intermediate steps like Lexical Analysing, Syntax Analysing, Semantic Analysing, Pre Optimizing, Assembly Code generation, Post Optimizing,  Assembling,  Linking and Loading are happening. In this post we are mainly covering 

  - Assembler
  - Linker
  - Loader
  - Disassembler

### Assembler

Assembler will create  object code from the assembly code. After Assembly Code generation and Post Optimizing, the generated assembly code is translated to Object code. Assembly Language aka **asm** is low-level programming language which is specific for CPU architecture. Its actually human readable representation of machine code.

For example:
Assembly Code for moving value 55 hex into register BL

    MOV BL, 055H

Corresponding Machine Code

    10111000
An assembler will generate object code by translating combinations of mnemonics and syntax for operations and addressing modes into their numerical equivalents. Each object code file combined to create the executable file.

**In short, assembler will** 

 - Translate assembly instructions, macros, and  pseudo-instructions
into binary machine instructions
 - Convert decimal numbers, etc. specified by
programmer into binary.

**Types of Assemblers**

 - One pass assembler

 - Two pass assembler

### Linker
### Assembler
### Loader
### Disassembler

### Todos

 - Write Tests
 - Rethink Github Save
 - Add Code Comments
 - Add Night Mode
