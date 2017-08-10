---
layout: post
title: 简单的队列实现（数组实现）
---


 单链表结构实现

	ADT接口 (QueueADT.java)

{% highlight java %}
public interface QueueADT {
	public void enQueue(Object element);//入队
	public Object deQueue();//出队
	public int size();//队大小
	public boolean isEmpty();//判空
	public boolean isFull();//判满
}


{% endhighlight %}



	实现测试类(QueueArrayImpl.java)
{% highlight java %}

public class QueueArrayImpl implements QueueADT{
	private Object[] que;
	private int font = 0;//首指针（伪指针）
	private int rear = 0;//尾指针（伪指针）
	private int count = 0;//记录队列元素数目
	public QueueArrayImpl(int len){//构造函数初始化指定大小的队列
		que = new Object[len];
	}
	
	//入队
	public void enQueue(Object element) {
		if(isFull()){
			System.out.println("queue is full!");
		}else{
			que[rear] = element;
			rear = (rear+1)%que.length;
			count++;
		}
	}
	//出队
	public Object deQueue() {
		if(isEmpty()){
			System.out.println("queue is empty!");
		}else{
			Object result = que[font];
			que[font] = null;
			font = (font+1)%que.length;//循环数组的通常做法（即求模）
			count--;
			return result;
		}
		return null;
	}
	//队列大小
	public int size() {
		return count;
	}
	//判空
	public boolean isEmpty() {
		return (count==0);
	}
	//判满
	public boolean isFull(){
		return (count==que.length);
	}
	//输出队列顺序预处理
	public String toString(){
		if(!isEmpty()){//队列不为空时
			StringBuilder sb = new StringBuilder("[");
			int f = font;
			int r = rear;
			if(f==r){//在队列不为空时，首尾指针相等即为队列为full
				while(f<=que.length-1){
					sb.append(que[f]+",");
					f++;
				}
				for(int i=0; i<r;i++){
					sb.append(que[i]+",");
				}
						
				
			}else if(f<r){
				while(f<r){
					sb.append(que[f]+",");
					f++;
				}
			}else if(f>r){//当首指针大于尾指针
				while(f<=que.length-1){
					sb.append(que[f]+",");
					f++;
				}
				for(int i=0; i<r;i++){
					sb.append(que[i]+",");
				}
				
			}
			//operate stringbuilder
			int l = sb.length();
			return sb.delete(l - 1, l).append("]").toString();
	
			
			
		}
		
		return "que is empty";
	}
	//输出队列
	public void print(){
		System.out.println(toString());
	}
	

	public static void main(String[] args) {
		QueueArrayImpl qa = new QueueArrayImpl(10);
		
		qa.enQueue(10);
		qa.enQueue(9);
		qa.enQueue(8);
		qa.enQueue(7);
		qa.enQueue(6);
		qa.enQueue(5);
		qa.enQueue(4);
		qa.enQueue(3);
		qa.enQueue(2);
		qa.enQueue(1);
		System.out.println("queue'size:"+qa.size());
		qa.print();
		qa.deQueue();
		qa.deQueue();
		qa.deQueue();
		System.out.println("queue'size:"+qa.size());
		qa.print();
		qa.enQueue(11);
		qa.enQueue(12);
		qa.enQueue(13);
		System.out.println("queue'size:"+qa.size());
		qa.print();
		
	}
	

	
}


{% endhighlight %}

运行结果：
![screenshot]({{site.url}}/assets/4.png)

<!--![My helpful screenshot]({{site.url}}/assets/1.png)-->