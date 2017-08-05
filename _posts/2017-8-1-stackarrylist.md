---
layout: post
title: 简单的栈结构实现（数组实现）
---


数组结构实现

	ADT接口 (StackADT.java)

{% highlight java %}
public interface StackADT {
	public void push(Object element);
	
	public Object pop();
	
	public Object peek();
	
	public int size();
	
	public boolean isEmpty();
}

{% endhighlight %}


	实现测试类(StackDemo.java)
{% highlight java %}

public class StackDemo implements StackADT{
	
	private Object[] contents;
	private int top;
	private static int SIZE = 10;
	
	public StackDemo(){
		contents = new Object[SIZE];
		top = 0;
	}
	

	@Override
	public void push(Object element) {
		if(top==contents.length){
			expand();
		}
		
		contents[top++] = element;
			
	}

	@Override
	public Object pop() {
		if(isEmpty()){
			System.out.println("stack is empty");
		}
		
		Object result = contents[--top];
		contents[top] = null;
		
		return result;
	}

	@Override
	public Object peek() {
		if(isEmpty()){
			return null;
		}
		
		Object result = contents[top-1];
		
		return result;
	}

	@Override
	public int size() {
		return top;
	}

	@Override
	public boolean isEmpty() {

		return (size()==0);
	}

	public void expand(){
		Object[] larger = new Object[size()*2];
		for(int index=0;index<top;index++){
			larger[index] = contents[index];
		}
		
		contents = larger;
		
	}
	
	public static void main(String[] args) {

		StackDemo  sd = new StackDemo();
		
		int i = 20;
		
		while(i>0){
			sd.push(i--);
		}
				
		System.out.println("stack size:"+sd.size());
		
		System.out.println(sd.pop());
		
		System.out.println(sd.size());
		
		System.out.println(sd.peek());
		
		System.out.println(sd.size());
		
	}
	
}


{% endhighlight %}

运行结果：
![screenshot]({{site.url}}/assets/2.png)
