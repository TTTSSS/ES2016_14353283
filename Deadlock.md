一、截图

![image](https://cloud.githubusercontent.com/assets/22443270/19890434/9cf59b38-a075-11e6-86ae-bcd2c0e1d453.png)

二、产生死锁的4个必要条件：
死锁就是两个或者多个进程，互相请求对方占有的资源。
互斥条件：一个资源每次只能被一个进程使用
请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺
循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系
三、解释
当t.start(),之后，线程t就被插入到调度队列里，当调度到他的时候，就跑run()里面的代码。而count是让main函数等待，等到线程t创建好后，
两个线程一起去请求锁。至于死锁的时间随机，我认为是由于要满足互相同时请求对方占有的资源，所以时间是不确定的。
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
//构造函数
	Deadlock(){
		Thread t = new Thread(this);
		int count = 20000;
		
		t.start();//线程t开始
		while(count-->0);//等待count
		a.methodA(b);
	}
	public void run(){
		b.methodB(a);
	}
	
	public static void main(String args[]){
		new Deadlock();
	}
}
