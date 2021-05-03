---
description: ShanghaiTech University - Spring 2021
---

# CS 131: Programming Languages and Compilers

## Introduction

![](.gitbook/assets/image%20%2822%29.png)

### Definition

A **Compiler** is "A program that takes a source-code program and translates it into an equivalent program in target language"

### String

A **String** is a sequence of characters

### Phases



## Lexical Analyzer （词法分析）

Reads the source program character by character and returns the **tokens** of the source program

* 分析并把 identifiers 放入符号表
* 利用正则表达式来分析 tokens
* 利用有限自动机来分析 Token 以完成词法分析

### Token

Describes a pattern of characters having some meaning in the source program \(such as identifiers, operators, keywords, numbers, delimiters and so on\)

* e.g. identifiers, operators, numbers

### Regular Expression （正则表达式）

### Finite Automata （有限自动机）

### NFA

### DFA 

### Implementation of Lexers

### RE to NFA

### RE to DFA

### Minimize DFA

### Other Issues for Lexers

## Syntax Analyzer （句法分析）

如果说词法分析这一步提供了可供计算机识别的**词**，那么句法分析是为了理解句子结构。

通常这一步会生成 **parse tree**, **parse tree** 用以描述句法结构。

### Difference with Lexical Analyzer

* The syntax analyzer deals with **recursive** constructs of the language
* Both do similar things; But the lexical analyzer deals with simple **non-recursive** constructs of the language.
* The lexical analyzer recognizes the smallest meaningful units （**tokens**） in a source program.
* The syntax analyzer works on the smallest meaningful units （**tokens**） in a source program to recognize meaningful structures （**sentences**） in our programming language.

### Parse Tree Abstraction

### CFG （上下文无关文法）

### Derivation Directions（派生文法）&Ambiguity（二义性）

### Top-Down Parsers

Construction of the parse tree starts at the root, and proceeds towards the leaves.

* Recursive Predictive Parsing
* Non-Recursive Predictive Parsing （**LL Parsing**）. （**L**-left to right; **L**-leftmost derivation）
* 语法构架能力弱

### Bottom-Up Parsers

Construction of the parse tree starts at the leaves, and proceeds towards the root.

* Bottom-up parsing is also known as **shift-reduce parsing**
* **LR Parsing** – much general form of shift-reduce parsing: **LR**, **SLR**, **LALR** \(**L**-left to right; **R**-rightmost derivation\)

### Other Issues for Parsers





