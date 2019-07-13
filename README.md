###for()、增强for()、foreach()、stream().foreach()
------------

* **测试一**
```java
public class TestFor {
    private static void doSome(String s) {
    }
    public static void main(String[] args) {
        /*添加数据*/
        List<String> list = new ArrayList<>();
        for (int i = 0; i < 10; i++) {
            list.add("第" + i + "条数据");
        }
        /*for循环*/
        long st1 = System.currentTimeMillis();
        for (int i = 0; i < list.size(); i++) {
            doSome(list.get(i));
        }
        /*增强for循环*/
        long st2 = System.currentTimeMillis();
        for (String s : list) {
            doSome(s);
        }
        /*foreach*/
        long st3 = System.currentTimeMillis();
        list.forEach(s -> doSome(s));
        /*stream.foreach*/
        long st4 = System.currentTimeMillis();
        list.stream().forEach(s -> doSome(s));
        long st5 = System.currentTimeMillis();
        print(st1, st2, st3, st4, st5);
    }
    /*时间输出*/
	public static void print(long s1, long s2, long s3, long s4, long s5) {
        System.out.println("for           循环: " + (s2 - s1) + "ms");
        System.out.println("增强for       循环: " + (s3 - s2) + "ms");
        System.out.println("foreach       循环：" + (s4 - s3) + "ms");
        System.out.println("stream.foreach循环：" + (s5 - s4) + "ms");
    }
}
```
**结果：**

		for           循环: 0ms
		增强for       循环: 0ms
		foreach       循环：129ms
		stream.foreach循环：3ms
------------

* **测试二**
```java
List<String> list = new ArrayList<>();
for (int i = 0; i < 1000; i++) {
	list.add("第" + i + "条数据");
}
```
**结果：**

		for           循环: 1ms
		增强for       循环: 1ms
		foreach       循环：121ms
		stream.foreach循环：3ms
------------

* **测试三**
```java
List<String> list = new ArrayList<>();
for (int i = 0; i < 1000000; i++) {
	list.add("第" + i + "条数据");
}
```
**结果：**

		for           循环: 17ms
		增强for       循环: 23ms
		foreach       循环：165ms
		stream.foreach循环：18ms
------------

* **测试四**
```java
private static void doSome(String s) {
	try {
		Thread.sleep(1);
	} catch (InterruptedException e) {
		e.printStackTrace();
	}
}
```
**结果：**

		for           循环: 184ms
		增强for       循环: 169ms
		foreach       循环：224ms
		stream.foreach循环：116ms


