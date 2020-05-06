## fork

fork的作用是根据一个现有的进程复制出一个新进程，原来的进程称为父进程（Parent Process），
新进程称为子进程（Child Process）。系统中同时运行着很多进程，这些进程都是从最初只有一个进程开始一个一个复制出来的。
在Shell下输入命令可以运行一个程序，是因为Shell进程在读取用户输入的命令之后会调用fork复制出一个新的Shell进程，
然后新的Shell进程调用exec执行新的程序。

**我们知道一个程序可以多次加载到内存，成为同时运行的多个进程**，例如我们平时所说的双开游戏.

#### 详情请参考多进程模块下的fork.md