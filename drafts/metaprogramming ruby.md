### block的局限：
关于block以及proc 、lamaba的解释，我觉得还不够好。其实如果从高阶函数(higher-order function)方面来解释，会更加方便。对于块来说，唯一的功能就是接受一个函数。
而高阶函数的具体功能有：

1. 可以被变量命名
2. 将函数作为参数传入函数
3. 将函数作为返回值
4. 可以被包含在数据结构当中

#### block的功能：
block可以传入匿名函数，最简单的例子：

```ruby
3.times{puts "love"}

[1,2,3,4].each{puts "love"}

```

更复杂一些的，可以接受参数：
```ruby
[1,2,3,4].each{|a| puts a}//[1,2,3,4]

```
yield的功能，同样也仅限于匿名函数的使用：
```ruby
def fun
	a = 10
	yield a
end
	fun {|x| puts x}
	
def test (x)
	puts x
	end
		
```


[Procs - 华盛顿大学 | Coursera](https://www.coursera.org/learn/programming-languages-part-c/lecture/GwWxg/procs) 这段视屏讲述了block 与proc的区别。
block可以靠yield传入不同函数，因此，乍看它起到了first-class 功能，但是它只能传入函数，但是不能返回函数，也无法将它存储在一个对象当中。因此功能不完全。只能算“second-class” 。

实例如下：
```ruby
a =[3,5,7,9]
b = a.map{|x| x + 1}     //[4,6,8,10]

c = a.map{|x| {|y| x >= y}}  //error

d = a.map{|x| (lambda {|y| x >= y})}
d.size	//4
d[2]	//#<Proc:0x00007f9f1194d830@(irb):34 (lambda)>
d.count {|x| x.call(6)}	//2
```
这就说明，block内的函数类型很有限，不能接受额外参数。