# c-p80-C-5-
C语言学习笔记  p80 C语言预处理（5）
#include<stdio.h>
命令行定义
代码用未声明的值通常放在预编译阶段来改他
gcc test.c -D(命令行参数） SZ=5
int main()
{
      int arr[SZ]={0}
      int i=0;
      for(i=0;i<SZ;i++)
      {
            arr[i]=i;
      }
      for(i=0;i<SZ;i++)
      {
            printf("%d\n",arr[i]);
      }     
      return 0;
}


条件编译：
在编译一个程序的时候我们如果要将一条语句（一组语句）编译或者放弃是很方便的，因为有条件编译指令的存在。
int main()
{
      int arr[10]={1,2,3,4,5,6,7,8,9,0};
      int i=0;
      for(i=0;i<10;i++)
      {
            arr[i]=0;
 #ifdef DEBUG   //如果有DEBUG指令则为真，以下代码参与编译，若为假，则不参与，在预处理阶段进行处理        
            printf("%d",arr[i]);//此行代码没必要
 #endif           
      }
      return 0;
}


常见的条件编译指令
1.
#if 常量表达式
      //...
#endif

2.多分枝的条件编译
#if 常量表达式
      //...
#elif 常量表达式
      //...
#else
      //...
#endif      

int main()
{
      #if 1==1
            printf("haha\n");
      #elif 2==1
            printf("hehe"\n);
      #else
            printf("嘿嘿\n");
      #endif      
      return 0;
}


3.判断是否被定义,来决定是否执行代码
#define DEBUG 0
 
#if define(symbol)
#ifdef symbol

#if !defined(symbol)
#ifndef symbol
int main()
{
      #if defined(DEBUG)
      printf("hehe\n");
      #endif
      return 0;
}

int main()
{
#ifdef DEBUG
      printf("hehe\n");
#endif      
      return 0;
}      

int main()
{
#if !defined(DEBUG)//条件没定义参与编译，定义了不参与编译
      printf("hehe\n");
#endif  
      return 0;
}

int main()
{
      #ifndef DEBUG
            printf("hehe\n"
      #endif      
      return 0;
}



4.嵌套指令
#if definef(OS_UNIX)
  `   #ifdef OPTION1
                 unix_version_option1();
      #endif           
      #ifdef OPTION2
            unix_version_option2();
      #endif
#elif defined(OS_MSDOS)
      #ifdef OPTION2
            msdos_version_option2();
      #endif      
#endif


//文件包含：
#include可以使另外一个文件文件
#include<>：用于库文件包含
#include"":用于本地头文件，包括#include<>,但是比#inlcude<>更加费时
容易造成代码冗余，所以需要用#ifndef一起使用
还可以在代码前一行加上#pragma once，一般头文件都会用这两种中的一种，前者更加老


预处理阶段
预处理指令
1.条件编译指令
2.#include
3.#define
...（基本都是#开头的）
#error
#pragma
#line




