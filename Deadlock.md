一、基本概念

死锁：两个或多个进程无限地等待一个事件，而该事件只能由这些等待进程之一来产生。

死锁的四个必要条件：

- 互斥：至少有一个资源必须处于非共享的模式，即一次只有一个进程使用，如果另一个进程申请该资源，那么申请进程必须等到该资源被释放为止。
- 占有并等待：一个进程必须占有至少一个资源，并等待另一个资源，而该资源为其他进程锁所占有。
- 非抢占：资源不可被抢占，资源只能在进程完成后释放。
- 循环等待：若干进程之间形成一种头尾相接的循环等待资源关系

二、实验代码及分析

1、Deadlock.java文件如下：

	class A{
		synchronized void methodA(B b){
			b.last();
		}
		synchronized void last(){
			System.out.println("Inside A.last()");
		}
	}
	class B{
		synchronized void methodB(A a){
			a.last();
		}
		synchronized void last(){
			System.out.println("Inside B.last()");
		}
	}
	class Deadlock implements Runnable{
		A a=new A();
		B b=new B();
	
		Deadlock(){
			Thread t=new Thread(this);
			int count=20000;
		
			t.start();
			while(count-->0);
			a.methodA(b);
		}
	
		public void run(){
			b.methodB(a);
		}
		public static void main(String args[]){
			new Deadlock();
		}
	}
2、在ubuntu中编写运行脚本Deadlock.sh文件，如下图所示:

	#!/bin/bash
	for c in `seq 100`;
	do
		echo "$c times"
		java Deadlock
	done
3、实验截图
运行脚本后的结果如下图所示：
![](https://raw.githubusercontent.com/zhanggx9/ES2016_14353387/master/Deadlock.png)

分析：

代码中使用了synchronized关键字，用它来修饰一个代码块时，能够保证在同一时刻只有一个线程执行该段代码，即其他想要调用该代码块的进程将被阻塞，当线程t开始之后，会被放入到调度队列，等待调度；当被调度时，就会运行run函数的内容，第一次会调用classB的内容，随后在一段时间后，会接着调用classA中的内容；若要达到死锁，则需要两个进程的运行时间和等待时间恰好满足死锁的必要条件。这样就会发生死锁。

