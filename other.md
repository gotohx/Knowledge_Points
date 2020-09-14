
 ## gdb用过吗，说一些gdb的命令
- 启动 gdp gcc -g test.c -o test ； gdb test 
- (gdb) start                         //开始调试
- (gdb) n                             //一条一条执行
- (gdb) step/s                        //执行下一条，如果函数进入函数
- (gdb) backtrace/bt                  //查看函数调用栈帧
- (gdb) info/i locals                 //查看当前栈帧局部变量
- (gdb) frame/f                       //选择栈帧，再查看局部变量
- (gdb) print/p                       //打印变量的值
- (gdb) finish                        //运行到当前函数返回
- (gdb) set var sum=0                 //修改变量值
- (gdb) list/l 行号或函数名             //列出源码
- (gdb) display/undisplay sum         //每次停下显示变量的值/取消跟踪
- (gdb) break/b  行号或函数名           //设置断点
- (gdb) continue/c                    //连续运行
- (gdb) info/i breakpoints            //查看已经设置的断点
- (gdb) delete breakpoints 2          //删除某个断点
- (gdb) disable/enable breakpoints 3  //禁用/启用某个断点
- (gdb) break 9 if sum != 0           //满足条件才激活断点
- (gdb) run/r                         //重新从程序开头连续执行
- (gdb) watch input[4]                //设置观察点
- (gdb) info/i watchpoints            //查看设置的观察点
- (gdb) x/7b input                    //打印存储器内容，b--每个字节一组，7--7组
- (gdb) disassemble                   //反汇编当前函数或指定函数
- (gdb) si                            // 一条指令一条指令调试 而 s 是一行一行代码
- (gdb) info registers                // 显示所有寄存器的当前值
- (gdb) x/20 $esp                    //查看内存中开始的20个数


## 两个进程某变量用gdb调试打印出的地址是否会一样
- 不一样
- 子进程会拷贝父进程的所有资源，变量。但是子进程从父进程拷贝下的所有资源会放到一个新的地址中。父子间共享的内存空间只有代码段。
- 子进程修改一个从父进程中拷贝下来的变量，父进程中的这个变量不会改变。
 
 



 
