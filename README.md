# C

C程序的编译流程

    precompiled        预编译
    compile            编译
    compilation        汇编
    assemble           集合
    load               装载
    link               链接

    compiler       编译器
    assembler      汇编器
    linker         链接器
    loader         装载器

    c源码处理阶段

        1  precompiled

            宏展开
            删除注释
            文本替换

            gcc -E main.c -o main.i

        2   编译

            将C源码翻译为汇编语言(助记符),汇编语言并不是机器语言
            汇编语言就是一种更贴近二进制的助记符语言

            movl    %edi, -20(%rbp)
            movq    %rsi, -32(%rbp)
            movl    -20(%rbp), %eax
            movl    %eax, %esi
            movl    $.LC0, %edi
            movl    $0, %eax
            call    printf
            movl    $0, -4(%rbp)
            jmp     .L2


            gcc -S main.c -o main.s  | gcc -S main.i -o main.s

            编译过程的五个阶段

                词法分析
                语法分析
                语义检查和中间代码生成
                代码优化
                目标代码生成

        3   汇编

            将汇编语言转化为机器语言，内容保存在目标文件中
            gcc -c main.c -o main.o

            main.o 是一个二进制文件,如果使用vim去查看文件内容，你会发现内容为乱码，不要怀疑。
            如果要使内容可读，需要借助工具

            nm main.o
            readelf -S main.o
            objdump -t main.o
            ...


        4   链接

            当编写了多个C文件时，我们将他们编译链接成一个可执行的文件，此时就需要用到链接脚本文件（ld）
            ld脚本主要功能就是：将多个目标文件（.o）和库文件（.a\.so）链接成一个可执行的文件。

            1 链接配置（可有可无）

            如一些符号变量的定义、入口地址、输出格式等

                STACK_SIZE = 0X200;
                OUTPUT_FORMAT(elf32-littlearm)
                OUTPUT_ARCH(arm)
                ENTRY(_start)

            2 内存布局定义

                脚本中以MEMORY命令定义了存储空间，其中以ORIGIN定义地址空间的起始地址，LENGTH定义地址空间的长度。

                MEMORY
                {
                FLASH (rx) : ORIGIN = 0, LENGTH = 64K
                }

            3 段链接定义

                脚本中以SECTIONS命令定义一些段（text、data、bss等段）链接分布。

             ld test.o -o test;

             [guangsujiqiang@su-ct7 binary_search_tree]$>ld test.o -o test
             ld: warning: cannot find entry symbol _start; defaulting to 00000000004000b0
             test.o: In function `main':
             main.c:(.text+0x1f): undefined reference to `printf'
             main.c:(.text+0x51): undefined reference to `printf'

             没有__start是因为c程序以main为主函数,汇编以start为主函数入口,使用gcc取代ld进行链接即可
             gcc test.o -o test -lselfpkg -L /home/my/lib


        5   装载

            将可执行文件load到内存中，开始运行