## 复习回顾

```java
1、类和对象的关系
	类是对象的模板, 对象是类的实例
	
2、类的定义格式
public class 类名{
	成员变量 (表示类的属性)
	成员方法 (表示类的行为或者功能)
	构造方法 (创建对象, 初始化成员变量的值)
}

3、对象的使用
	先定义类, 再通过类创建对象
	类名  对象名 = new 类名();
	访问成员变量: 对象名.成员变量名  
	访问成员访问: 对象名.成员方法名()

4、private关键字的作用
	权限修饰符, 被private修饰的成员只能在本类中使用
	修饰成员变量, 成员方法, 构造方法, 类 

5、this关键字的作用
	代表当前对象的引用
	使用场景: 形参名字和成员变量同名时, 使用this来访问成员变量

6、构造方法的定义格式和特点
    public 类名(参数列表){
        初始化代码;
    }
    
	1. 通过new关键字调用
	2. 作用: 创建对象, 初始化成员变量的值
	3. 每次创建对象, 都会调用一次构造方法
	4. 构造方法可以重载
```

## 1  API

#### 1.1  API概述

- 什么是API

  ​	API (Application Programming Interface) ：应用程序编程接口

  ​	JDK已有的一些功能 Scanner  Random  String  Arrays  ArrayList  Math  Date

- java中的API

  ​	指的就是 JDK中提供的各种功能的 Java类，这些类将底层的实现封装了起来，我们不需要关心这些类是如何实现的，只需要学习这些类如何使用即可，我们可以通过帮助文档来学习这些API如何使用。

#### 1.2  如何使用API帮助文档

- 打开帮助文档

![01](assets/01.png)

- 找到索引选项卡中的输入框

![02](assets/02.png)

- 在输入框中输入要查找的类，例如Random。

![03](assets/03.png)

- 看类在哪个包下

![04](assets/04.png)

- 看类的描述

![05](assets/05.png)

- 看构造方法

![06](assets/06.png)

- 看成员方法

![07](assets/07.png)

==快速生成方法调用的返回值：Ctrl + Alt + V==

```java
import java.util.Scanner;
public class ScannerDemo {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个字符串:");

        //读取字符串, 直到回车换行结束
        //String line = sc.nextLine();

        //读取字符串, 直到空格结束
        String line = sc.next();
        System.out.println(line);
    }
}
```

## 2  String类

#### 2.1  String类概述

​	String 类代表字符串类，Java 程序中所有的双引号字符串（比如"Hello"），都是 String 类的对象。

​	==String 类在 java.lang 包下，使用时不需要导包。==

#### 2.2  String类的特点

- 字符串不可变，它们的值在创建后不能被更改。
- 虽然 String 的值是不可变的，但是它们可以被共享。(常量池)
- 字符串的底层原理是字节数组。

#### 2.3  String类的构造方法

```java
//无参构造方法
String()

//常见带参构造方法
String(String original) //根据字符串常量创建字符串对象
String(char[] value)  //通过字符数组创建字符串对象（常用）
String(char[] value, int begin, int length)  //从数组的begin开始，共length个字符创建字符串
String(byte[] values)//根据byte数组创建字符串
    
//最常用的字符串定义格式
String s = "字符串内容";
```

**示例代码：**

```java
public class StringDemo {
	public static void main(String[] args) {
        //1、String()：创建一个空白字符串对象，不含有任何内容
        String s1 = new String();
        System.out.println("s1:" + s1);
        
		//2、String(String original) 根据字符串数据创建字符串对象
		String s2 = new String("hello");
		System.out.println(s2);
		
		//3、String(char[] value)  通过字符数组创建字符串对象
		char[] value = {'h','e','l','l','o'};
		String s3 = new String(value);
		System.out.println(s3);
		
		//4、String(char[] value, int offset, int length) 
        //根据字符数组的一部分数据创建字符串对象
		String s4 = new String(value,0,3); //hel
		String s5 = new String(value,2,3); //llo
		System.out.println(s4);
        System.out.println(s5);
        
        //5、String(byte[] values)  根据byte数组创建字符串
        byte[] arr = {97,98,99};
        String s6 = new String(arr); //abc
        System.out.println(s6);
		
		//6、最常用的方式：使用字符串常量构建
		String s7 = "hello";
		System.out.println(s7);
	}
}
```

#### 2.4  String创建对象的特点

​	1、使用new关键字创建字符串对象时，每次都会在堆中创建对象，并返回堆中的地址值给变量。所以new出来的字符串对象，每一个的地址都不同。

​	2、创建字符串常量时，JVM首先在常量池中查找是否存在该字符串，找到了直接引用常量池地址，否则在常量池里创建字符串，并将地址返回给变量。

```java
public class StringDemo2 {
	public static void main(String[] args) {
		//每次都会在堆中创建对象，并返回地址
		String s1 = new String("hello");
		String s2 = new String("hello");
		
        //判断常量池中是否存在“hello”常量，如果存在直接返回地址值。
        //如果不存在，在常量池中创建“hello”对象，并返回地址值。
		String s3 = "hello";
		String s4 = "hello";
		
		System.out.println( s1==s2 ); //false
		System.out.println( s1==s3 ); //false
		System.out.println( s3==s4 ); //true
	}
}
```

**测试案例**

```java
【练习】下列代码运行后输出的结果是什么？
   public static void main(String[] args) {
        String s1 = new String("abc");
        String s2 = "abc";
        System.out.println(s1 == s2); //false
        
        
        String s3 = "a" + "b" + "c";  //String s3 = "abc";
        String s4 = "ab" + "c";  //String s4 = "abc";
        System.out.println(s3 == s4); //true
        System.out.println(s2 == s3); //true
        
        String s5 = "ab";
        String s6 = s5+"c";  // new String的过程
        System.out.println(s6 == s2); //false
}
```

#### 2.5  字符串的比较

**==号的作用：**

- 基本数据类型：比较的是具体的数据值。
- 引用数据类型：比较的是内存地址值。

**判断字符串内容是否相等：**

```java
public boolean equals(Object anObject) //严格区分大小写（判断密码）
public boolean equalsIgnoreCase(String anotherString) //不区分大小写 （判断验证码）
```

**案例代码**

```java
public class StringDemo2 {
	public static void main(String[] args) {
		//每次都会在堆中创建对象，并返回地址
		String s1 = new String("hello");
		String s2 = new String("hello");
		
        //判断常量池中是否存在“hello”常量，如果存在直接返回地址值。
        //如果不存在，在常量池中创建“hello”对象，并返回地址值。
		String s3 = "hello";
		String s4 = "hello";
		
		System.out.println( s1==s2 ); //false
		System.out.println( s1==s3 ); //false
		System.out.println( s3==s4 ); //true
        
        System.out.println( s1.equals(s2) ); //true
		System.out.println( s1.equals(s3) ); //true
		System.out.println( s3.equals(s4) ); //true
	}
}
```

#### 2.6  用户登录案例

**需求：**

​	已知用户名和密码，请用程序实现模拟用户登录。总共给三次机会，登录之后，给出相应的提示。

**步骤说明：**

1. 给出一组已知的用户名和密码。

2. 定义一个次数为3的循环。

3. 在循环内接收键盘录入的用户名和密码，用于和给出的用户名和密码进行比较。

   如果用户名和密码相同，提示登录成功、并结束循环。

   如果用户名和密码不相同，则提示剩余的机会。

**代码实现：**

```java
/*
 * 需求：键盘输入用户名和密码，判断用户名密码是否正确，
 * 		输入正确提示登录成功，输入错误提示登录失败，并提示还有几次机会。
 */
public class LoginTest {
	public static void main(String[] args) {
		//定义变量存储正确的用户名和密码
		String name = "admin";
		String pwd = "123456";
		
		Scanner sc = new Scanner(System.in);
		//循环获取用户输入
		for(int i=2; i>=0; i--){
			System.out.println("请输入用户名：");
			String scName =  sc.nextLine();
			System.out.println("请输入密码：");
			String scPwd = sc.nextLine();
			
			//判断用户名或密码是否正确
			if( name.equals(scName) && pwd.equals(scPwd) ){
				System.out.println("登录成功");
				break;
			}else{
				if(i==0){
					System.out.println("你的帐号被锁定，请与管理员联系");
				}else{
					System.out.println("登录失败，你还有"+i+"次机会");
				}
			}
		}
	}
}
```

### 上午总结

```java
1. API
	应用程序编程接口 , 开发商提供的功能( JDK的核心类库)
    通过API帮助文档, 可以查看API的使用

2. String类的特点
	在java.lang包中, 不需要导包就能使用.
    String的字符串一旦创建, 就不能改变, 但是字符串值是可以共享的(常量池中的字符串可以共享)
    String的底层是字符(字节)数组

3. String类的构造方法
	String()
    String(String str)
    String(char[] arr)
    String(byte[] arr)
    String(char[] arr, int start, int length)
    
    推荐使用:
	String s = "字符串常量";

4. String创建对象的特点
	String s = new String("abc");
	在常量池寻找是否存在"abc"字符串, 不存在时在常量池中创建, 并引用地址到堆中, 堆中创建对象,指向常量池中的"abc" ,并把堆中的地址返回给s变量
	
	String s = "abc";
	JVM会在常量池中检查是否存在"abc"字符串, 存在时直接引用地址给变量s, 否则在常量池中创建"abc",并将地址返回给s变量.
     
    字符串变量的拼接, 其实都是创建了新的字符串对象

5. 字符串的比较
==
	基本数据类型: 比较数据值是否相等
	引用数据类型: 比较的是内存地址值是否相等

equals()
    在字符串中, 是比较两个字符串的内容是否相等, 而且区分大小写
equalsIgnoreCase()
    在字符串中, 是比较两个字符串的内容是否相等, 不区分大小写
```

#### 2.7  字符串遍历

字符串遍历相关方法：

```java
//获取字符串长度
int length(); 

//返回字符串中指定索引处的字符，索引从0开始。
char charAt(int index);
```

案例代码：

```java
/*
	需求：键盘录入一个字符串，遍历输出字符串中的每一个字符。
*/
import java.util.Scanner;
public class StringDemo3 {
	public static void main(String[] args) {
        // 1. 创建键盘录入对象
        Scanner sc = new Scanner(System.in);
        
        // 2. 获取键盘录入字符串
        System.out.println("请输入一个字符串：");
        String str = sc.nextLine();	
        
		// 3. 循环遍历字符
		for(int i=0; i<str.length(); i++){
			System.out.println( str.charAt(i) );
		}
	} 
}
```

字符串遍历方式2 

```java
char[] toCharArray();  //将字符串转换为char数组
```

```java
/*
	遍历方式2：char[] toCharArray()
*/
public class StringDemo4 {
	public static void main(String[] args) {、
    String str = "abcde";
    //将字符串转换为字符数组
	char[] arr = str.toCharArray();
	//遍历字符数组
	for(int i=0 ;i<arr.length; i++){
		System.out.println(arr[i]);
	}
    
}
```

#### 2.8  统计字符次数

**需求：**

​	键盘录入一个字符串，统计该字符串中大写字母字符，小写字母字符，数字字符出现的次数。

**思路分析：**

​	1  键盘录入一个字符串。

​	2  定义三个统计变量。

​	3  遍历字符串，拿到每一个字符。

​	4  判断字符是大写的、小写的、还是数字字符的，并分别让对应的统计变量自增。

​	5  输出统计变量

**案例代码：**

```java
/*	
	大写字母：'A'~'Z'
	小写字母：'a'~'z'
	数字：'0'~'9'
    基本汉字对应编码范围：19968 ~ 40869
*/
public class StringDemo4 {
    
    public static void main(String[] args) {
        // 1.获取键盘录入
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个字符串：");
        String line = sc.nextLine();

        //定义四个统计变量
        int bigCount = 0;
        int smallCount = 0;
        int numberCount = 0;
        int chinese = 0;

        //遍历字符串，得到每一个字符
        for(int i=0; i<line.length(); i++) {

            char ch = line.charAt(i);
            //判断该字符属于哪种类型，然后对应类型的统计变量+1
            if(ch>='A' && ch<='Z') {
                bigCount++;
            } else if(ch>='a' && ch<='z') {
                smallCount++;
            } else if(ch>='0' && ch<='9') {
                numberCount++;
            }else if(ch>=19968 && ch <= 40869){
                chinese++;
            }
        }

        //输出四种类型的字符个数
        System.out.println("大写字母：" + bigCount + "个");
        System.out.println("小写字母：" + smallCount + "个");
        System.out.println("数字：" + numberCount + "个");
        System.out.println("中文：" + chinese + "个");
    }
}
```

#### 2.9  字符串拼接

**需求：**

​	定义方法，把数组中的元素按照指定格式拼接成一个字符串返回。

​	字符串拼接格式为：[元素1，元素2，元素3]

**案例代码：**

```java
/*
 * 定义方法，把数组中的元素按照指定格式拼接成一个字符串返回
 * 格式：[元素1，元素2，元素3]
 */
public class StringTest4 {
	public static void main(String[] args) {
		int[] arr = {1,2,3};
		String s = arrayToString(arr);
		System.out.println(s);
	}
	
	/*
	 * 两个明确：
	 * 		1、明确参数：数组，这里使用int数组
	 * 		2、明确返回值：字符串String[1 ,2 ,3]
	 */
	public static String arrayToString(int[] arr){
		String s = "";
		//对数组元素进行字符串拼接
		s+="[";
		for(int i=0; i<arr.length; i++){
			//最后一个元素不用加逗号
			if(i==arr.length-1){
				s+=arr[i];
			}else{
				s+=arr[i];
                s+=", ";
			}
		}
		s+="]";
		return s;
	}
    
    //实现方式2
     public static String arrayToString2(int[] arr){

        String s = "";
        s+="[";

       if(arr.length>0){
           s+=arr[0];
           for(int i=1; i<arr.length;i++){
               s+=", "+arr[i];
           }
       }

        s+="]";
        return s;
    }
    
}
```

#### 2.10  字符串反转

**需求：**

​	定义一个方法，实现字符串反转。键盘录入一个字符串，调用该方法后，在控制台输出结果。

​	例如，键盘录入 abc，输出结果 cba。

**代码实现：**

```java
public class StringDemo5 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入一个字符串：");
		String s = sc.nextLine();
        //调用自定义方法实现字符串反转
		String ss = reverse(s);
		System.out.println(s + "反转后："+ ss);
	}
	
	/*
	 * 参数：String类型
	 * 返回值：String类型
	 */
	public static String reverse(String str){ //"abc"
		//接收反转后的字符串
		String newStr = "";
		//反转遍历
		for(int i=str.length()-1; i>=0; i--){
            //拼接字符串
			//newStr += str.charAt(i);
            char ch = str.charAt(i); //c
            newStr = newStr + ch; //""+c  c // c+b cb //cb+a cba
		}
		return newStr;
	}
}
```

## 3  StringBuilder类

#### 3.1  StringBuilder类的概述

**String进行字符串拼接时的特点**

​	每拼接一个字符串，内存中都会产生新的字符串对象。这种操作比较浪费内存空间，效率也较低。

![1561190407244](assets/1561190407244.png)

**StringBuilder的特点**

​	StringBuilder 是一个可变的字符串类，我们可以把它看成是一个容器，这里的可变指的是StringBuilder对象中的内容是可变的。StringBuilder位于java.lang包下，不需要导包。

**String和StringBuilder区别**

​	1、==String是内容是固定的类==，进行String的拼接其实是创建新的字符串对象。

​	2、==StringBuilder是内容可变的类==，可以动态进行字符串内容的拼接。

#### 3.2  StringBuilder的构造方法

```java
【常见的构造方法】
public StringBuilder()  //构建空的字符串对象（常用的，推荐使用的）
    
public StringBuilder(String str) //构建指定的字符串对象
```

**示例代码：**

```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        
        //public StringBuilder()：创建一个空白可变字符串对象，不含有任何内容
        StringBuilder sb = new StringBuilder();
        System.out.println("sb:" + sb);
        System.out.println("sb的长度:" + sb.length());

        //public StringBuilder(String str)：根据字符串的内容，来创建可变字符串对象
        StringBuilder sb2 = new StringBuilder("hello");
        System.out.println("sb2:" + sb2);
        System.out.println("sb2长度:" + sb2.length());
    }
}
```

#### 3.3  StringBuilder的添加和反转方法

**1、append和reverse方法：**

```java
public StringBuilder append(任意类型) //将参数拼接成字符串，并返回StringBuilder对象本身。

public StringBuilder reverse()  //将字符串反转，并返回StringBuilder对象本身。

```

**2、链式编程：**

​	当一个方法调用后、返回的还是该对象本身，就可以连续调用该方法。

​	格式 ： 对象名.方法名(参数).方法名(参数)...

**3、案例代码：**

```java
public class StringBuiderDemo2 {
	public static void main(String[] args) {
		
		StringBuilder sb = new StringBuilder();
		//append方法对传入的数据进行字符串拼接
		sb.append("hello");
		sb.append("world");
		sb.append(true);
		sb.append(123);
		System.out.println(sb);
		
		//链式编程
		StringBuilder sb2 = new StringBuilder();
		sb2.append("2019").append("年").append("06").append("月");
		System.out.println(sb2);
	}
}
```

#### 3.4  StringBuilder和String相互转换

```java
1、StringBuilder转String：
	调用 StringBuilder 的 toString() 方法

2、String转StringBuilder：
	调用有参构造方法 StringBuilder(String s)，传入字符串
```

```java
public class StringBuiderDemo3 {
	public static void main(String[] args) {
		
		StringBuilder sb = new StringBuilder();
		sb.append("hello").append(" world");
		
		// 1. StringBuilder 转 String
		String s  = sb.toString();
		System.out.println(s);
		
		// 2. String 转 StringBuilder
		String str = "hello java";
		StringBuilder sb2 = new StringBuilder(str);
		System.out.println(sb2);
	}
}
```

#### 3.5  StringBuilder实现字符串拼接

**需求：**

​	定义方法，把数组中的元素按照指定格式拼接成一个字符串返回。

​	字符串拼接格式为：[元素1，元素2，元素3]。

​	字符串拼接要求使用StringBuilder实现。

**案例代码：**

```java
/*
 * 定义方法将int数组按照指定格式拼接成字符串，
 * 拼接效果：[元素1,元素2,元素3]
 */
public class StringTest9 {
	public static void main(String[] args) {
		int[] arr = {10,20,30,40};
		String s = arrayToString(arr);
		System.out.println(s);
	}
	
	/*
	定义方法两个明确：
		方法返回值：String类型
		方法参数：int[] 
	*/
	public static String arrayToString(int[] arr){
		//创建字符串拼接对象
		StringBuilder sb = new StringBuilder();
		
		//进行字符串拼接，拼接格式：[1,2,3]
		sb.append("[");
		for(int i=0; i<arr.length; i++){
			if(i==arr.length-1){
				sb.append(arr[i]);
			}else{
				sb.append(arr[i]).append(", ");
			}
		}
		sb.append("]");
		
		//转换成字符串并返回
		String s = sb.toString();
		return s;
	}
    
    
     /*
        进行字符串拼接，拼接格式：[1,2,3]
        方法优化改造
     */
  	public static String arrayToString2(int[] arr){
        //创建字符串拼接对象
        StringBuilder sb = new StringBuilder();

        //拼接开始符号
        sb.append("["); //[1

        //拼接元素内容
        if(arr.length>0){
            sb.append(arr[0]);
            for(int i=1; i<arr.length; i++){ // ,2 ,3
                sb.append(",").append(arr[i]);
            }
        }

        //拼接结束符号
        sb.append("]");

        //转换成字符串并返回
        String s = sb.toString();
        return s;
    }
    
}
```

#### 3.6  StringBuilder实现字符串反转

**需求：**

​	定义一个方法，实现字符串反转。键盘录入一个字符串，调用该方法后，在控制台输出结果。

​	例如，键盘录入 abc，输出结果 cba。

​	要求使用StringBuilder实现。

**代码实现：**

```java
/*
 * 1、定义方法，将字符串内容反转并返回。
 * 2、使用键盘录入字符串，调用方法完成字符串反转。
 */
public class Test {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入一个字符串：");
		String s = sc.nextLine();
		String str = reverse(s);
		System.out.println(s+"反转后："+str);
	}
	
	//1、定义方法，将字符串内容反转并返回。
	public static String reverse(String str){
		/*
		//字符串转StringBuilder
		StringBuilder sb = new StringBuilder(str);
		//调用反转的方法
		sb.reverse();
		//StringBuilder转字符串
		String s = sb.toString();
		return s;
		*/
		
		//链式编程简化写法
        //new StringBuilder(str) 匿名对象
		return new StringBuilder(str).reverse().toString();
	}
}
```

### 总结

```java
能够知道帮助文档的使用步骤
 看类所在的包
 看构造方法
 看成员方法

能够知道字符串对象通过构造方法创建和直接赋值的区别
 通过构造方法创建, 在堆中会创建一个对象, 在常量池中也会创建一个对象
 直接赋值,只在常量池中创建字符串常量

能够知道String和StringBuilder的区别
	String是内容不可变的类(底层是数组), 做String的拼接, 每次都会创建新的对象
	StringBuilder是一个字符串容器, 内容是可以动态拼接的

能够完成String和StringBuilder的相互转换
	String-->StringBuilder  : 
		String s = "hello";
		StringBuilder sb = new StringBuilder(s);
	
	StringBuilder-->String
	StringBuilder sb = new StringBuilder();
	sb.append("hello").append("world");
	//转成字符串
	String s = sb.toString();

能够使用StringBuilder完成字符串的拼接
	拼接字符串方法: append(任意类型)

随堂案例
    能够完成用户登录案例
    能够完成统计字符串中大写,小写,数字字符的个数
    能够使用StringBuilder完成数组的拼接
    能够使用StringBuilder完成字符串的反转
```

## 扩展：String类常用方法汇总

```java
//判断相等
boolean equals(Object anObject)
    判断字符串内容是否相等，区分大小写。
boolean equalsIgnoreCase(String anotherString)
    判断字符串内容是否相等，不区分大小写。

//大小写转换
String toLowerCase()
	字符串全部转小写返回。
String toUpperCase()
	字符串全部转大写返回。

//提取子串
String substring(int beginIndex)
	从beginIndex位置起，获取后面剩余子串返回。
String substring(int beginIndex, int count)
	取出beginIndex开始，共count个字符。


//字符串查找
int indexOf(int ch) 
    返回指定字符在字符串中第一次出现的位置索引。找不到时返回-1
int indexOf(String str)
    返回指定子字符串在此字符串中第一次出现的位置索引，找不到返回-1
int lastIndexOf(int ch)
    返回指定字符在此字符串中最后一次出现处的索引。
    
boolean startsWith(String prefix)
    判断字符串是否以指定的前缀开始。
boolean endsWith(String suffix)
    判断字符串是否以指定的后缀结束。
    
//字符串替换
String trim()
	截去字符串两端的空格，但对于中间的空格不处理。
String replace(char oldChar, char newChar)
	用字符newChar替换当前字符串中所有的oldChar字符，并返回一个新的字符串。

//字符串切割
String[] split(String regex)
	根据指定的regex符号将字符串分割成字符串数组返回。
	
//其他方法
int length()
	获取字符串长度。
char charAt(int index)
	根据索引返回指定字符，索引从0开始。
public char[] toCharArray()
	将字符串转换为字符数组返回。
	
//基本数据类型转字符串
public static String valueOf(任意基本数据类型);
//调用格式 ：String.valueOf(实际参数);
```

##### 扩展代码:

```java
public class StringMethodDemo {
    public static void main(String[] args) {

        String s1 = "javase";
        String s2 = "JAVAEE";

        //大小写转换
        System.out.println( s1.toUpperCase()  );//JAVASE
        System.out.println( s2.toLowerCase() );//javaee

        //提取子串
        System.out.println( s1.substring(4)  ); //se
        System.out.println( s1.substring(0,4) ); //java

        //字符串查找
        System.out.println( s1.indexOf('v') ); //2
        System.out.println( s1.indexOf('a') ); //1
        System.out.println( s1.indexOf('k') ); //-1
        System.out.println( s2.indexOf("EE") ); //4
        System.out.println( s2.indexOf("JAVA") ); //0

        System.out.println( s1.lastIndexOf('a') ); //3

        //判断字符串的开始和结束的内容

        String s3 = "18888888888"; //手机号码
        System.out.println( s3.startsWith("1") ); //true

        String file = "考试成绩.xls";
        System.out.println( file.endsWith(".xls") ); //true

        //字符串替换
        String s4 = "  admin  ";
        System.out.println(s4.length());  //9
        System.out.println( s4.trim() ); //admin
        System.out.println( s4.trim().length() ); //5
		
        //字符串去空格
        String s5 = " hello world ";
        System.out.println(s5.trim()); //hello world
		
        //字符串替换
        //String replace(char oldChar, char newChar)
        String date = "2019-07-07";
        System.out.println( date.replace('-','/') );

        //字符串切割
        //String[] sp
        // lit(String regex)
        String[] arr = date.split("-");
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
		
        //基本数据类型转字符串
        int a = 10;
        String s6 = a+"";
        System.out.println(s6);

        String s = String.valueOf(a);
        System.out.println(s);

        String s7 = "ab";
        byte[] bytes = s7.getBytes();
        System.out.println(Arrays.toString(bytes));

    }
}
```

#### 字符串非空判断

```java
public class StringTest2 {
    public static void main(String[] args) {
        //空字符串，长度为0
        String s1 = "";
        System.out.println(s1.length()); //0

        //空白字符的字符串
        String s2 = " ";
        System.out.println(s2.length());//1

        //空字符串，没有指向任何的堆内存地址
        String s3 = null;
//        System.out.println(s3.length());//NullPointerException

        //判空处理
        //0长度的空串，有长度的空串，null
        if(s3!=null && s3.trim().length()>0){
            //如果判断条件为true，此时s2就是非空的字符串
            System.out.println("----------");
        }
    }
}
```

