# C语言
> 上一次，我们讲了一些简单的内容，希望同学们有完成上次布置的练习。这节课，我们主要讲讲struct和union, 指针，还有malloc，以及GDB。还是扯几句题外话吧，目前，C语言还是非常流行的。我们班有同学去华为工作，主要也是写C代码，为什么C语言还是这么流行呢？可以看看博客： https://www.tomorrow.wiki/archives/1893 。C语言适用于对性能要求非常高和偏底层的一些领域。所以，万一同学们去了菊厂，那今天多学一点C肯定是有帮助的。相信我们复旦的同学，一定能把C语言轻松搞定！         —— 谢东方

## 指针
> 指针是C语言中比较难的内容，我记得我之前学面向对象的时候，被指针坑惨了。不过，学懂之后，你就知道，还是有掌握的可能的。

参考一下，这篇blog：https://blog.csdn.net/rich369/article/details/107180139

指针就是数据的地址，相当于门牌号，有了门牌号，我们就可以找到相对应的数据，进而去修改它。使用的过程如下：
```c
#include <stdio.h>
void passByValue(int a, int b);
void passByPointer(int *a, int *b);
void print(int a, int b);
int main(int argc, char** argv) {
    int a = 0, b = 0;
    printf("before change ");print(a, b);
    passByValue(a, b);
    printf("after passByValue ");print(a, b);
    passByPointer(&a, &b);
    printf("after passByPointer ");print(a, b);
    return 0;
}

void passByValue(int a, int b) {
    a += 1;
    b += 1;
}

void passByPointer(int *aPtr, int *bPtr) {
    *aPtr += 1;
    *bPtr += 1;
}
void print(int a, int b) {
    printf("value: a = %d, b = %d\n", a, b);
}
```
比如说，我们有变量int a; 获取它的指针（地址）int* aPtr = &a;然后获取它的值，通过*aPtr的方式。注意，如果你没有初始化指针就直接使用，很容易出现段错误。比方说:
```c
int* aPtr;
int b = *aPtr;// 可能会发生段错误
```
因为aPtr没有经过初始化可能为任意值，而这个地址，可能是内核的地址，你没有访问权限，就会报错。以后一定要小心哦！

数组其实内部也是一个指针，所以，可以有下面这段代码。
```c
#include <stdio.h>

int main(int argc, char** argv) {
    char str[] = "china,china,china!";
    int len = sizeof(str)/sizeof(str[0]);// sizeof返回byte数量
    char *ptr = str;
    for (int i = 0 ; i < len; i++) {
        printf("%c\n", *ptr);
        ptr++; // 指针++对于不同类型的指针来说，地址的变化是不一样的。
    }
    return 0;
}
```
接下来打印指针。
```c
#include<stdio.h>
int main(int argc, char** argv) {
    // 指针其实就是地址，不同类型的指针经过++，增减的值取决于类型的大小，比如int是4个字节，char是一个字节
    printf("char size: %ld, int size: %ld.\n", sizeof(char), sizeof(int));
    char* chPtr = NULL;// Java里面是null
    int* intPtr = NULL;
    for (int i = 0 ; i < 3; i++) {
        printf("chPtr: %p\n", chPtr++);
        printf("intPtr: %p\n", intPtr++);
    }
    return 0;
}
```

所以，你可以明白char** argv，实际上可以理解为char[][] argv，char[]可以理解为字符串，所以char[][]相当于Java里面的String[] argv。

## struct & union
> struct扮演了类似于Java类中数据的角色,union主要是为了省空间。在一些极端情况下是非常有用的。
```

```
