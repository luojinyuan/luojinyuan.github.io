---
layout: post
title: 简单的栈结构实现（链表实现）
---


 单链表结构实现

	ADT接口 (StackADT.java)

{% highlight java %}
public interface StackADT {

	//压入一个元素
	public void push(Object element);
	
	//弹出一个元素
	public Object pop();
	
	//返回栈顶元素的引用
	public Object peek();
	
	//判空
	public boolean isEmpty();
	
	//栈容量
	public int size();
	
	public String toString();
	
	
}
{% endhighlight %}


	节点类(LinearNode.java)
{% highlight java %}
public class LinearNode {
	private Object element;//结点元素
	private LinearNode next;//下一结点
	
	public LinearNode(Object element){
		this.element = element;
	}
	
	public void setNext(LinearNode top){
		this.next = top;
	}
	
	public LinearNode getNext(){
		
		return this.next;
	}
	
	public Object getElement(){
		return this.element;
	}

	
}

{% endhighlight %}


	实现测试类(StackDemo.java)
{% highlight java %}
public class StackDemo implements StackADT{

	private LinearNode top;
	private int count;
	public StackDemo(){
		top = null;
		count = 0;
	}
	
	
	@Override
	public void push(Object element) {
		LinearNode node = new LinearNode(element);
		node.setNext(top);
		top = node;
		count++;
	}

	@Override
	public Object pop() {
		if(isEmpty()){
			System.out.println("stack is empty");
		}
		
		Object result = top.getElement();
		top = top.getNext();
		count--;
		
		return result;
		
	}

	@Override
	public Object peek() {
		
		return top.getElement();
	}

	@Override
	public boolean isEmpty() {
		
		return (count==0);
	}

	@Override
	public int size() {
		
		return count;
	}

	
	
	public static void main(String args[]){
		
		StackDemo sd = new StackDemo();
		
		sd.push(1);
		sd.push(2);
		sd.push("aa");
		
		System.out.println("stack's count:"+sd.size());
		
		System.out.println(sd.pop());
		System.out.println(sd.size());
		
	}
	
}

{% endhighlight %}

运行结果：
![screenshot]({{site.url}}/assets/1.png)

<!--![My helpful screenshot]({{site.url}}/assets/1.png)-->