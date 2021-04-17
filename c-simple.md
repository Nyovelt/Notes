# C Simple

#### Pointers

* Dangling references
* memory leaks
* C 是一个弱类型语言， 也就是说对于每一个类型，结构， 对于其边界没有严格的检查。对于指针也是这样， C将自由和信任交到了程序员手上， 因此会产生很多不安全的内存访问行为。
  * 而 Rua st 则添加了诸多限制。
* 函数指针：
  * char \*foo\(args\)
  * f = &foo
    * 能被取地址
  * \(\*f\)\("cat", 3\)
    * 能被调用， 返回 char\*
* Tricky:
  * int\* a\[10\]; =&gt; a is an array of pointers
  * int \*a, b; =&gt; a is pointer, b is integer

#### Memory

* 程序一共有四块内存区
  * 栈：存放局部变量
    * return address, arguments, local variables
    * Constants
    * see [编译时你在做什么？有没有空？可以来拯救吗？](https://aaaab3n.moe/technology/2019/11/29/c-cpp-black-magic.html)
  * 堆：存放动态变量 - difficult to manage
    * malloc
    * calloc
    * free
    * realloc
    * 
  * 静态：存放 functions 之外的变量
    * Static variables
    * Global variables
    * Constants
    * String Literals
  * 代码：当程序运行时存储，不可更改
    * Machine Instructions
    * Constants
  * ![](https://snz04pap002files.storage.live.com/y4ms7978SdKAnRisT2pTi3Dt7K-57msUyxYmihpxd3Op6N3vVU322DnJGUOYX8xrL9gEoZe0CeXa8JK4O1wp3TbenlHKWoIBk1EW_AukWnx-hDhpUcdGxPZ5-mmaqwBGhpx1lV4dsgRKmhXNSuoMKAqnOphlOLlK4T5Yy-Q194wF6J9Nt284s9mLD1bfdaMg6Ek?width=784&height=858&cropmode=none)
* string:
  * `a = malloc(sizeof((char))* strlen(b)+1)`
    * pay attention to **+1s**
  * `strcpy(a,b)` 不安全， 因为不知道结尾\(\0\)
  * `strncpy(a,b, strlen(b)+1)`安全。 if its too short it will not copy the null terminator!
* Union

  * hold different types in **the same location**
  * 也就是说会存在**内存复写**
  * size为最大数据结构的大写， 对齐到 4k ， 例如 char 虽然是 1 字节， 但 union 会 size = 4
  * [https://www.geeksforgeeks.org/c-language-2-gq/structure-union-gq/](https://www.geeksforgeeks.org/c-language-2-gq/structure-union-gq/) Q8 is worth doing Q19 helps understanding
  * ```text
    #include <stdio.h>
    #include <string.h>
    union a{
        char b[6];
        char c[9];
    } data;
    ​
    int main(){
        // char d[7];
        union a A = {"abcdef"};
        strcpy(A.c, "12345678");
        printf("%s", A.b);
    }
    ​
    ```

  output is 12345678

  ```text
  ​
  - ```C
    #include <stdio.h>
    #include <string.h>
    typedef union {
        unsigned long long num;
        struct {
            unsigned short a;
            unsigned short b;
            unsigned short c;
            unsigned short d;
        } data;
    } Datatype;
  
    int main(){
    Datatype y;
    y.num= 0xABCDDCBADCABAAAA;
    printf("%d\n", y.data.a);
    printf("%d\n", y.data.b);
    printf("%d\n", y.data.c);
    printf("%d\n", y.data.d);
    }
  
    // result is proved by gcc, clang, msvc on x86 devices
    [Running]  gcc test.c -o test && test
    43690
    56491
    56506
    43981
    [Done] exited with code=0 in 1.206 seconds
  
    >>> 0xABCD
    43981
    >>> 0xDCBA
    56506
    >>> 0xDCAB
    56491
    >>> 0xAAAA
    43690
    >>>
  ```

  * 由此可见， 结构体中的类型是自上而下的，而小端序是先下后上的。于是产生了 x 反而对应末尾的2字节。
  * ```text
    #include <stdio.h>
    #include <string.h>
    typedef union {
        char d[4];
        int e;
        struct {
            char a;
            char b;
            char c;
        } data;
    } Datatype;
    ​
    int main(){
    Datatype y;
    strcpy(y.d, "ABC");
    printf("%d\n", y.e);
    printf("%c\n", y.data.a);
    printf("%c\n", y.data.b);
    printf("%c\n", y.data.c);
    }
    ​
    Result:
        4407873 //0x434241
        A           
        B
        C
    ```

    * char\[\] 类型或者数组类型也是自上而下的， 因此在内存中从上往下是 'A', 'B', 'C'。 int 按照小端序读是从下往上读，从左往右的拼接数字，所以是 '\0''C''B''A' = 0x00434241 = 4407873\(D\)
  * 如果感觉自己被加强了，可以试试 [3\(b\)](https://robotics.shanghaitech.edu.cn/courses/ca/20s/notes/midterm_sol.pdf)

