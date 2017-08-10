---
layout: post
title: 简单的队列实现（链表实现）
---


 单链表结构实现

	ADT接口 (QueueADT.java)

{% highlight java %}
public interface QueueADT {
	public void enQueue(Object element);//入队
	public Object deQueue();//出队
	public boolean isEmpty();//判断队列是否为空
	public int size();//队容量
	public String toString();//覆写toString方法
}

{% endhighlight %}


	节点类(Node.java)
{% highlight java %}
public class Node {
	public Object element;//当前结点元素
	public Node next;//下一结点
	public Node(){}
	public Node(Object element,Node next){
		this.element = element;
		this.next = next;
	}
}


{% endhighlight %}


	实现测试类(QueueImpl.java)
{% highlight java %}

public class QueueImpl implements QueueADT{
	private int count = 0;
	private Node font;
	private Node rear;

	public QueueImpl(){
		Node n = new Node(null,null);//构造函数new一个空的结点
		font = rear = n;//首尾指针指向该结点
		n.next = null;
	}
	
	public void enQueue(Object element) {
		Node nw = new Node(element,null);
		rear.next = nw;
		rear = nw;
		count++;
	}

	public Object deQueue() {
		if(!isEmpty()){
			Node f = font.next;//保存头结点
			font.next = f.next;
			Object re = f.element;
			f = null;
			count--;
			return re;
		}
		return null;
		
	}

	public boolean isEmpty() {
		return count == 0;
	}

	public int size() {
		return count;
	}
	public String toString(){//返回队列的顺序
		StringBuilder sb = new StringBuilder("[");
		
		if(!isEmpty()){
			for(Node current=font.next; current!=null; current=current.next){
				sb.append(current.element+",");
			}
			int len = sb.length();
			return sb.delete(len - 1, len).append("]").toString();
		}
		
		return "queue is empty";
	}
	
	public void print(){
		System.out.println(toString());
	}
	
	
	
	public static void main(String[] args) {
		QueueImpl q = new QueueImpl();
		q.enQueue("1");
		q.enQueue("2");
		q.enQueue("3");
		q.enQueue("4");
		q.enQueue("5");
		System.out.println("size:"+q.size());
		q.print();
		q.deQueue();
		q.deQueue();
		q.deQueue();
		q.deQueue();
		System.out.println("size:"+q.size());
		q.print();
	}
	

	
}

{% endhighlight %}

运行结果：
![screenshot]({{site.url}}/assets/3.png)

<!--![My helpful screenshot]({{site.url}}/assets/1.png)-->