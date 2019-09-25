## Os Operation

### 进程间通信

####  管道 (pipe)

![管道示意图](https://images2015.cnblogs.com/blog/932246/201609/932246-20160909083943691-1511040684.png)

父进程调用 fork 后，如下图：

![父子进程通信](https://images2015.cnblogs.com/blog/932246/201609/932246-20160909083954504-660747163.png)

父子各关闭一个：

![父子进程通信](https://images2015.cnblogs.com/blog/932246/201609/932246-20160909084013707-2039185528.png)

```
#include<stdio.h>
#include<unistd.h>
 #include<string.h>
int main()
{
    int _pipe[2];
    int ret=pipe(_pipe);
    if(ret<0)
    {
         perror("pipe\n");
    }
    pid_t id=fork();
    if(id<0)
    {
       perror("fork\n");
    }
    else if(id==0)  // child
    {
        close(_pipe[0]);
        int i=0;
        char *mesg=NULL;
       while(i<100)
       {
           mesg="I am child";
           write(_pipe[1],mesg,strlen(mesg)+1);
           sleep(1);
           ++i;
        }
     }
    else  //father
    {
        close(_pipe[1]);
        int j=0;
        char _mesg[100];
        while(j<100)
        {
          memset(_mesg,'\0',sizeof(_mesg ));
          read(_pipe[0],_mesg,sizeof(_mesg));
          printf("%s\n",_mesg);
          j++;
        }
   }
   return 0;
}
```

* 消息队列
* 共享内存
* 信号量
* Socket 通信
* 


* [进程间通信之管道（pipe、fifo)](https://www.cnblogs.com/MrListening/p/5858358.html)


## 网络部分

