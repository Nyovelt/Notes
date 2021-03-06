---
description: ShanghaiTech University - Spring 2021
---

# CS 131: Programming Languages and Compilers

## Introduction

![Compiler](.gitbook/assets/image%20%2822%29.png)

### Definition

A **Compiler** is "A program that takes a source-code program and translates it into an equivalent program in target language"

### String

A **String** is a sequence of characters.

* Alphabet: A finite set of symbols （ASCII characters）
* String has words and sentences
* $$st$$ is the concatenation of $$s$$and $$t$$
  * $$ s \epsilon = \epsilon s = s $$
* $$ \epsilon $$is the empty string
  * $$ s^0 = \epsilon $$
* $$ \mid s \mid $$ is the length of s
* Suppose s is banana
* **Prefix:**前缀
  * ban banana
* **Suffix:**后缀
  * banana, ana
* **Substring:**子字符串
* **Subsequence**:子字符
  * bnan, nn

A **Language** is a set of Strings over a fixed **Alphabet** $$\Sigma$$, constructed using a specific Grammar.

* e.g. $$ \{\varepsilon, 0,01,011,0111, \ldots\} $$
* Not all Strings of chars in the Alphabet is in the certain Language, only those who satisfy the Grammar rules.
* Alphabet $$ ={0,1} $$ and using Grammar rule  $$ \mathrm{RE}=01^{*}$$ , we can specify the above example Language, while $$ 01 $$ isn't.

Below is **Operations** and **Examples**.

![Operations of Languages](.gitbook/assets/image%20%2823%29.png)

![Example of Laguage Operations](.gitbook/assets/image%20%2830%29.png)

A **Grammar** $$G$$ ****is the description of method （_rules_） of how to construct a certain Language over a certain Alphabet

* Type 0: Turing Machine Recursive Enumerable Gramma
* Type 1: Context-sensitive Grammar （CSG）
* Type 2: Context-free Grammar \(CFG,上下文无关文法）， _mostly recursive_
* Type 3: Right-linear Grammar Regular Expressions \(RE,正则表达式）， _non-recursive_

{% hint style="info" %}
Expressiveness: Type 0 &gt; Type 1 &gt; Type 2 &gt; Type 3
{% endhint %}

### Phases

![](.gitbook/assets/image%20%2849%29.png)

## Lexical Analyzer （词法分析器）

Reads the source program character by character and returns the **tokens** of the source program

* 分析并把 identifiers 放入符号表
* 利用正则表达式来分析 tokens
* 利用有限自动机来分析 Token 以完成词法分析
* 词法分析器 = 读入（scanning） + 词法分析（lexical analysis）

![Lexical Analyzer](.gitbook/assets/image%20%2837%29.png)

### Token

Describes a pattern of characters having some meaning in the source program \(such as identifiers, operators, keywords, numbers, delimiters and so on\)

* e.g., identifiers, operators, numbers

A **Lexeme （词素）** is an instance of a Token, along with its unique attributes.

* e.g. `17`
  * INT 
  * Token.value = 17

![Process of determing a Token &#x901A;&#x5E38;&#x4F7F;&#x7528;&#x53CC; buffers &#x6765;&#x907F;&#x514D; buffer &#x533A;&#x592A;&#x5C0F;&#x7684;&#x95EE;&#x9898;](.gitbook/assets/image%20%2836%29.png)

### Regular Expression （正则表达式）

我们利用**正则表达式**来 描述 **Tokens** 匹配 **Tokens**

* 每个**正则表达式** $$r$$ 描述一个语言 $$L(r)$$
  * $$r$$被叫做 **regular set**
* **正则表达式**是左结合的，从左向右匹配的
* **正则表达式**是一个 **Type-3 Grammar Rule**

#### **Properties**

![Properties](.gitbook/assets/image%20%2827%29.png)

![Extended Properties](.gitbook/assets/image%20%2831%29.png)

* e.g.
  * Integers:
    * Digit = \[0-9\]\*
    * Integer = Digit Digit\*
  * Identifier
    * letter = \[a-zA-Z\]
    * identifier = letter （letter + digit）\*
  * Whitespace
    * WS = \('\n' + '\t' + ' '\)+
* Examples
  * Even Binary number 
    * 1\[0+1\]\*0 \| 0

### Finite Automata （有限自动机）

#### Transition Diagram

![Transition Disgram Examples](.gitbook/assets/image%20%2840%29.png)

当一个 Token 被识别：

* 如果是关键字，那么会返回 **Token of the keyword**
* 如果是符号表里的 ID，那么返回 **entry of symbol table**
* 如果符号表没有这个ID，那么加入ID并返回新的 **entry of symbol table**

```c
switch (state){
case 0:
    c = nextchar();
    if (c == [something])
        state = [state], lexeme_beginning ++;
    else if (c == [something])
        [do something]
    else if (c == [final state]) // terminal
        retract(1); //forward
        lexical_value = install_num(); // install something 
        return (NUM);
    else
        state = fail();
```

#### Finite automata

A **recognizer** for a language is a program that takes a string x, and answers “yes” if x is a sentence of that language, and “no” otherwise.

We call the recognizer of the tokens as a **finite automaton**.

**Example**

![Regular expression: \(a+b\)\*abb](.gitbook/assets/image%20%2828%29.png)

* **Start Arrow**
* **State**
* **Transition Edge**
* **Accepting State**:同心圆，接受并结束，状态3
* **Death State:错误**状态，未定义的 transition 指向该状态
* Transition table:

| state | a | b |
| :--- | :--- | :--- |
| 0 | {0,1} | {0} |
| 1 | -- | {2} |
| 2 | -- | {3} |

{% hint style="info" %}
注意 empty string 可以被某些自动机接收
{% endhint %}

### NFA

Non-Deterministic Finite Automata （NFAs） **easily** represent regular expression, but are **less precise.** 

**Accept s:** an Accepting State that spells out **s**.

An NFA is a mathematical model that consists of:

* S, a **finite** set of **states**
* $$\Sigma$$, the symbols of the **input alphabet**
* _move_, a **transition function**
  * move\(state, symbol\) $$\to$$ sets of states
* A state $$s_0 \in S$$, the **start state**
* $$F \subseteq S  $$, a set of **final** or **accepting states**
* $$ \epsilon$$**move: ε- transitions** are allowed in NFAs. In other words, we can move from one state to another one without consuming any symbol

{% hint style="info" %}
The $$\epsilon$$-Closure of $$S = S \cup \{ $$ All States that can go to without consuming any input $$\}$$
{% endhint %}

### DFA 

Deterministic Finite Automata （DFAs） require **more complexity** to represent regular expressions but offer **more precision**.

**Does not allow** $$ \epsilon$$**move,**  for every $$s \in S$$, there is ONLY ONE decision for every input _Symbol._

**Accept s:** an Accepting State that spells out **s** _and **ONLY and ONLY ONE** path_.

{% hint style="info" %}
No $$\epsilon$$-closure !!!
{% endhint %}

### Implementation of Lexers

One Token, A _Recognizer. There are 4 ways. \(r stands for RE\)_

1.  $$r \to NFA \to Recognizer$$
2. $$ r \to  NFA \to DFA \to Recognizer$$
3. $$ r \to DFA \to Recognizer$$
4. $$ r \rightsquigarrow DFA \to Minimized ~ DFA \to Recognizer$$

### RE to NFA

Algorithm is called **Thompson's Construction**.

![](.gitbook/assets/image%20%2834%29.png)

There are some requirements on such construction:

* $$N(s)$$and $$N(t)$$CANNOT have any intersections
* REMEMBER to assign unique names to all states

Properties of the resulting NFA:

* Exactly 1 Start State & 1 Accepting State
* $$#$$ of States in NFA  $$\leq 2 \times$$\(\# of Symbols + \# of Operators\) in $$r$$
* States do not have multiple outgoing edges with the same input symbol
* States have at most 2 outgoing $$\epsilon$$ edges

### RE to DFA

**\[Step 1\]**: We make Augmented RE: concatenate with symbol \# \(meaning "finish"\).

* e.g. \(a+b\)\*a\#
* Ensures at least one operator in the RE

**\[Step 2\]:** Build syntax tree for this Augmented RE:

![](.gitbook/assets/image%20%2829%29.png)

* $$\epsilon$$, \# and $$a \in \Sigma$$ all are at leaves
* All other operators are inner nodes
* Non-$$\epsilon$$ leaves get its position number, increasing from left $$\to$$ right

**\[Step 3\]:** Compute `nullable()`, `firstpos()` & `lastpos()` for ALL nodes.

1. `firstpos(n)`: Function returning the set of positions where the _first_ Symbol can be at, in the _sub-RE_ rooted at `n`
2. `lastpos(n)`: Function returning the set of Positions where the _last_ Symbol can be at, in the sub-RE rooted at `n`
3. `nullable(n)`: Function judging whether the _sub-RE_ rooted at `n` can generate $$\epsilon$$

![](.gitbook/assets/image%20%2825%29.png)

**\[Step 4\]:** Compute `followpos()` for Leaf positions

`followpos(i)`: Function returning the set of positions _which can follow_ position i in the generated String

Conduct a _Post-order_ _Depth First Traversal_ on the syntax tree, and do the following oprations when leaving $$\cdot$$ / \* nodes:

* $$ c{1} \cdot c{2}: $$ For all $$ i \in $$ `lastpos(c1)` , `followpos(i)`= `followpo(i)`  $$\cup $$ `firstpos(c2)`
* $$  c^{*}:$$  For all $$ i \in $$ `lastpos(c)`, `followpos(i)`$$= $$ `followpos(i)` $$\cup $$ `firstpos(c)`

**\[Step 5\]:** Construct the DFA.

```c
void construct() {
    S0=firstpos(root);
    DStates= {(S0, unmarked)};
    while (DStates has an unmarked State U) {
        Mark State U;
        for (each possible input char c) 
        {
            V= {};
            for (each position p in U whose symbol is c)
                V=UnionofVandfollowpos(p);
            if (V is not empty) {
                if (V is not in DStates)
                    Include V in DStates, unmarked;
                Add the Transition U--c->V;
            }
        }
    }
}
```

* A State $$S$$in resulting DFA is an Accepting State iff \# node $$\in S $$
* Start State of the resulting DFA is $$S_0$$

#### Calculate \epsilon-Closure

```c
set epsClosure(set S) 
{
        for (each State s in S)
            Push s onto stack;
        closure = S;
        while (stack is not empty) 
        {
        Pop State u;
        for (each State v that u->v is an epsilon Transition) 
        {
              if (v is not in closure) 
              {
                  Include v in closure;
                  Push v onto stack;            
              }
         }    
         }
         return closure;
 }

```

#### Implement NFA as Recognizer

```c
bool  recognizer() {
    S=epsClosure(s0);
    while ((c=getchar()) !=EOF)
        S=epsClosure(move(S, c));
    if (S and F has intersections)
        return ACCEPT;
    return REJECT;
}
```

{% hint style="info" %}
Performance of NFA-type Recognizers: Space $$O(|r|)$$; Time $$O(|r| \times |s|)$$
{% endhint %}

#### Implement DFA as Recognizer

```c
bool recognizer() {
    s=s_0;
    while ((c=getchar()) !=EOF)
        s=move(s, c);
    if (s is in F)
        return ACCEPT;
    return REJECT;
}
```

{% hint style="info" %}
Performance of DFA-type Recognizers: Space $$O(|2^{|r|})$$; Time $$O(|s|)$$
{% endhint %}

#### Convert NFA to DFA

Algorithm is called **Subset Construction\(子集构造法\)**, since we make subset of States in original NFA into a single State in resulting DFA

```c
void subsetConstruction() {
    S0=epsClosure({s0});
    DStates= {(S0, unmarked)};
    while (DStates has any unmarked State U) {
        MarkState U;
        for (each possible inputchar c) {
            V=epsClosure(move(U, c));
            if (V is not empty) {
                if (V is not in DStates)
                    Include V in DStates, unmarked;
                Add the Transition U--c->V;
            }
        }
    }
}
```

* A State $$S$$ in resulting DFA is an Accepting State iff $$ \exists s \in S, s$$ is an Accepting State in original NFA
* Start State of the resulting DFA is $$S_0$$

### Minimize DFA

```c
void minimize() {
    PI = {G_A, G_n};
    do {
        for (every group G in PI){
            for (every pair of States (s,t) in G){
                if (for every possible input char c, transition s--c -> and t--c-> go to states in the same group)
                    s,t are in the same subgroup;
                else
                    s,t should split into different subgroups;
            }
            Split G according to the above information;
        }
    }while (PI changed in this iteration)
    Every Group in PI is a state in the minimal DFA;
}  
```

* A State S in the minimal DFA is an Accepting State iff $$ \exists s \in S $$, s is an Accepting State in original DFA
* Start State of the minimal DFA is the one containing original Starting State

### Other Issues for Lexers

#### Look ahead

#### Comment Skip

#### Symbol Table

## Syntax Analyzer （句法分析）

如果说词法分析这一步提供了可供计算机识别的**词**，那么句法分析是为了理解句子结构。

通常这一步会生成 **parse tree**, **parse tree** 用以描述句法结构。

### Difference with Lexical Analyzer

* The syntax analyzer deals with **recursive** constructs of the language
* Both do similar things; But the lexical analyzer deals with simple **non-recursive** constructs of the language.
* The lexical analyzer recognizes the smallest meaningful units （**tokens**） in a source program.
* The syntax analyzer works on the smallest meaningful units （**tokens**） in a source program to recognize meaningful structures （**sentences**） in our programming language.

### Parse Tree Abstraction

A **Parse Tree / Syntax Tree \(语法树\)** is a graphical representation of the structure of a program, where leaf nodes are Tokens.

### CFG （上下文无关文法）

A **Context-free Grammar \(CFG\)** is a **Type-2** Grammar rule, which serves the construction of a Parse Tree from a streamof Tokens. We use a set of Production Rules to characterize a CFG

![](.gitbook/assets/image%20%2842%29.png)

A **Terminal \(终结符号\)** is a Token; A **Non-terminal \(非终结符号\)** is a syntactic variable.

* The Start Symbol is the first one of Non-terminals; Usually represents the whole program
* A Sentence is a string of Terminals such that Start Symbol $$ S \Rightarrow{ }^{+} s $$

A **Production Rule \(生成规则\)** is a law of production, from a Non-terminal to a sequence of Terminals & Non-terminals.

* e.g. $$ A \rightarrow \alpha A \mid \beta $$, where $$ A $$ is a Non-terminal and $$ \alpha, \beta $$ are Terminals
* May be _recursive_
* The procedure of applying these rules to get a sentence of Terminals is called **Sentential Form** / **Derivation**

{% hint style="info" %}
$$ | $$ Context-free Languages $$ |>| $$ Regular Languages $$ | $$, e.g. $$ \{(^{i})^{i}: i  \geq  0 \} $$.
{% endhint %}

### Derivation Directions（派生文法）&Ambiguity（二义性）

**Left-most Derivation**  **\(左递归\)**$$ \left(\Rightarrow_{l m}\right) $$ means to replace the leftmost Non-terminal at each step.

* If $$ \beta A \gamma \Rightarrow \operatorname{lm} \beta \delta \gamma $$, then NO Non-terminals in $$ \mathcal{\beta} $$
* Corresponds to _Top Down Parsing_

**Right-most Derivation**  $$ (\Rightarrow r m) $$means Replace the rightmost Non-terminal at each step.

* If $$ \beta A \gamma \Rightarrow_{r m} \beta \delta \gamma $$, then NO Non-terminals in $$ \gamma $$
* Corresponds to _Bottom Up Parsing_, in reversed manner

![](.gitbook/assets/image%20%2847%29.png)

A CFG is **Ambiguous** when it produces more than one Parse Tree for the same sentence. Must remove Ambiguity for apractical CFG, by:

* Enforce _Precedence \(优先级\)_ and _Associativity \(结合律\)_
  *  e.g. $$  * > +$$ , then $$ + $$ gets expanded first
* Grammar Rewritten

![](.gitbook/assets/image%20%2844%29.png)

### Top-Down Parsers

Construction of the parse tree starts at the root, and proceeds towards the leaves.

* Recursive Predictive Parsing
* Non-Recursive Predictive Parsing （**LL Parsing**）. （**L**-left to right; **L**-leftmost derivation）
* 语法构架能力弱

#### Implement

1. Eliminate Left Recursion $$\to$$ Recursive-descent Parsing
2. Eliminate Left Recursion $$\to$$ Left Factoring $$\to$$Recursive Predictive Parsing
3. Eliminate Left Recursion $$\to$$Left Factoring $$\to$$Construct Parsing Table $$\to$$Non-recursive Predictive Parsing

#### Left Recursion Elimination \(消除左递归\)

$$ A \Rightarrow^{+} A_{\alpha} $$: Left Recursion

* Top Down Parsing **CANNOT** handle Left-recursive Grammars
* Can be eliminated by rewriting

For _Immediate_ Left Recursions \(Left Recursion that may appear in a single step\), eliminate by:

![&#x7ACB;&#x5373;&#x5DE6;&#x9012;&#x5F52;&#x7684;&#x6D88;&#x9664;](.gitbook/assets/image%20%2843%29.png)

```c
/* Non-terminals arranged in order: A1, A2, ... An. */
void eliminate() 
{
    for (i from 1 to n) {
        for (j from 1 to i-1)
            Replace Aj with its products in every Prodcution Rule Ai->Aj ...;
        Eliminate Immediate Left Recursions Ai->Ai ...;    
    }
}
```

![&#x5DE6;&#x9012;&#x5F52;&#x7684;&#x6D88;&#x9664;](.gitbook/assets/image%20%2845%29.png)

#### Implementing Recursive-descent Parsing

```c
/*  Example:
*    E -> T | T + E*    
     T -> int | int * T | ( E )
*/
bool term(TOKENtok)  { return*ptr++==tok; }
bool E1()             { returnT(); }
bool E2()             { returnT() &&term(PLUS) &&E(); }
bool E() {
     TOKEN*save=ptr;
     return (ptr=save, E1()) || (ptr=save, E2());
}
bool T1()             { returnterm(INT); }
bool T2()             { returnterm(INT) &&term(TIMES) &&T(); }
bool T3()             { returnterm (OPEN) &&E() &&term(CLOSE); }
bool T() {
     TOKEN*save=ptr;
     return (ptr=save, T1()) || (ptr=save, T2()) || (ptr=save, T3());
}
```

#### Left Factoring: Produce LL\(1\) Grammar

LL\(1\) means Only 1 Token Look-ahead ensures which Pruduction Rule to expand now.

To convert LL\(1\)  to a CFG, for each Non-terminal :

![](.gitbook/assets/image%20%2841%29.png)

{% hint style="info" %}
\|\| LL\(1\) \|\| &lt; \|\| CFG \|\|, so not all Grammar can be convert to LL\(1\)

* Such Grammar will have an entry with multiple Production Rules to use in the Parsing Table, thusWill be inappropriate for Predictive Parsing
{% endhint %}

#### Implementing Recursive Predictive Parsing

{% hint style="info" %}
This part stongly suggest to see  [https://www.josehu.com/assets/file/compilers.pdf](https://www.josehu.com/assets/file/compilers.pdf) for better understanding.
{% endhint %}

![](.gitbook/assets/image%20%2846%29.png)

#### Parsing Table Construction

{% hint style="info" %}
This part stongly suggest to see  [https://www.josehu.com/assets/file/compilers.pdf](https://www.josehu.com/assets/file/compilers.pdf) for better understanding.
{% endhint %}

#### Implementing LL\(1\) Parsing

{% hint style="info" %}
This part stongly suggest to see  [https://www.josehu.com/assets/file/compilers.pdf](https://www.josehu.com/assets/file/compilers.pdf) for better understanding.
{% endhint %}

### Bottom-Up Parsers

Construction of the parse tree starts at the leaves, and proceeds towards the root.

* Bottom-up parsing is also known as **shift-reduce parsing**
* **LR Parsing** – much general form of shift-reduce parsing: **LR**, **SLR**, **LALR** \(**L**-left to right; **R**-rightmost derivation\)

{% hint style="info" %}
This part stongly suggest to see  [https://www.josehu.com/assets/file/compilers.pdf](https://www.josehu.com/assets/file/compilers.pdf) for better understanding.
{% endhint %}

## Thanks

* \[Guanzhou HU's Notes\]\([https://www.josehu.com/](https://www.josehu.com/)\)
* TAs: 季杨彪, 杨易为, 尤存翰





