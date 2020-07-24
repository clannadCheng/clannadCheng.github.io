## 基础程序设计

### 标识符

> - 凡是自己起名称的字符都叫标识符
>
>  > 比如类名、变量名、方法名、接口名、包名...
>
> -  命名规则
>
>  > 1)、名称只能由字母、数字、下划线、$符号组成
>  >
>  > 2)、不能以数字开头
>  >
>  > 3)、名称不能使用JAVA中的关键字。
>  >
>  > 4)、坚决不允许出现中文及拼音命名。
>  >
>  > 5)、java中严格区分大小写，长度无限制
>
> - 命名规范
>
> >- 包名：多单组成是所有字母都小写 packagename
> >- 类名接口名：多单词组成时，所有单词的首字母大写 ClassName
> >- 变量名、方法名：多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写：variableName 
> >- 常量名：所有字母都大写。多单词时每个单词用下划线连接：FINAL_NAEM
>

#### 关键字

> - 被Java赋予了特殊含义的标识符、标识符：自定义名称的对象名称
> - 关键字中所有字母都为小写
> - 或非关键字 true、false
> - 保留字：现有java版本未使用，以后可能会使用 goto、const

#### class

> - 一个文件可以有多个类
>- class关键只后面只能放类名

- 代码示例 ：

``` java
class class1 {
    
}
class class2 {
    
}
```

#### public

> 一个类只能有一个public  且public 类名一定要与文件名一致

- 代码示例 ：

``` java
public class class1{
    
}
```

### 变量

- 命名规则

> - 变量必须先声明，后使用
> - 变量都定义在其作用域内。在作用域内，它是有效的。换句话说，出了作用域，就失效了
> -  同一个作用域内，不可以声明两个同名的变量

- 代码示例

  ``` java
  class VariableTest {
  	public static void main(String[] args) {
  		//变量的定义
  		int myAge = 12;
  		//变量的使用
  		System.out.println(myAge);
  		
  		//编译错误：使用myNumber之前并未定义过myNumber
  		//System.out.println(myNumber);
  
  		//变量的声明
  		int myNumber;
  		
  		//编译错误：使用myNumber之前并未赋值过myNumber
  		//System.out.println(myNumber);
  
  		//变量的赋值
  		myNumber = 1001;
  		//编译不通过
  		//System.out.println(myClass);
  
  		//不可以在同一个作用域内定义同名的变量
  		//int myAge = 22;
  		
  	}
  
  	public void method(){
  		int myClass = 1;
  	}
  }
  //class VariableTest {}//逆向思维，反证法
  ```
#### 数据类型

##### 基本数据类型

> - 整型：byte \ short \ int \ long
> - 浮点型：float \ double
> - 字符型：char
> - 布尔型：boolean	
> - 基本数据类型的默认值
>
> >
> >
> >



- 代码演示

  ``` java
  class VariableTest1 {
  	public static void main(String[] args) {
  		//1. 整型：byte(1字节=8bit) \ short(2字节) \ int(4字节) \ long(8字节)
  		//① byte范围：-128 ~ 127
  		//
  		byte b1 = 12;
  		byte b2 = -128;
  		//b2 = 128;//编译不通过
  		System.out.println(b1);
  		System.out.println(b2);
  		// ② 声明long型变量，必须以"l"或"L"结尾
  		// ③ 通常，定义整型变量时，使用int型。
  		short s1 = 128;
  		int i1 = 1234;
  		long l1 = 3414234324L;
  		System.out.println(l1);
  
  		//2. 浮点型：float(4字节) \ double(8字节)
  		//① 浮点型，表示带小数点的数值
  		//② float表示数值的范围比long还大
  
  		double d1 = 123.3;
  		System.out.println(d1 + 1);
  		//③ 定义float类型变量时，变量要以"f"或"F"结尾
  		float f1 = 12.3F;
  		System.out.println(f1);
  		//④ 通常，定义浮点型变量时，使用double型。
  		
         
  		//3. 字符型：char (1字符=2字节)
  		//① 定义char型变量，通常使用一对'',内部只能写一个字符
           // char c =''; //编译不通过 有且只能放一个固定一个值不能为空
           // char c = 'a'+1; //c='b'; c+1= 98 ;(a=97)
  		char c1 = 'a';
  		//编译不通过
  		//c1 = 'AB';
  		System.out.println(c1);
  
  		char c2 = '1';
  		char c3 = '中';
  		char c4 = 'ス';
  		System.out.println(c2);
  		System.out.println(c3);
  		System.out.println(c4);
  
  		//② 表示方式：1.声明一个字符 2.转义字符 3.直接使用 Unicode 值来表示字符型常量
  		char c5 = '\n';//换行符
  		c5 = '\t';//制表符
  		System.out.print("hello" + c5);
  		System.out.println("world");
  
  		char c6 = '\u0043';
  		System.out.println(c6);
  
  		//4.布尔型：boolean
  		//① 只能取两个值之一：true 、 false
  		//② 常常在条件判断、循环结构中使用
  		boolean bb1 = true;
  		System.out.println(bb1);
  
  		boolean isMarried = true;
  		if(isMarried){
  			System.out.println("你就不能参加\"单身\"party了！\\n很遗憾");
  		}else{
  			System.out.println("你可以多谈谈女朋友！");
  		}
  
  	}
  }
  
  ```

##### 引用数据类型

>- 类(class)
>- 接口(interface)
>- 数组(array)
>
>1. 引用类型在内存中的值默认是null

###### **String**

>1. String属于引用数据类型,翻译为：字符串
>2. 声明String类型变量时，使用一对""
>3. String可以和8种基本数据类型变量做运算，且运算只能是连接运算：+
>4. 运算的结果仍然是String类型

- 代码示例

``` java

class StringTest {
	public static void main(String[] args) {
		
		String s1 = "Hello World!";

		System.out.println(s1);

		String s2 = "a";
		String s3 = "";

		//char c = '';//编译不通过

		//***********************
		int number = 1001;
		String numberStr = "学号：";
		String info = numberStr + number;// +：连接运算
		boolean b1 = true;
		String info1 = info + b1;// +：连接运算
		System.out.println(info1);

		//***********************
		//练习1
		char c = 'a';//97   A:65
		int num = 10;
		String str = "hello";
		System.out.println(c + num + str);//107hello
		System.out.println(c + str + num);//ahello10
		System.out.println(c + (num + str));//a10hello
		System.out.println((c + num) + str);//107hello
		System.out.println(str + num + c);//hello10a

		//练习2
		//*	*
		System.out.println("*	*");
		System.out.println('*' + '\t' + '*');
		System.out.println('*' + "\t" + '*');
		System.out.println('*' + '\t' + "*");
		System.out.println('*' + ('\t' + "*"));


		//***********************

		//String str1 = 123;//编译不通过
		String str1 = 123 + "";
		System.out.println(str1);//"123"
		
		//int num1 = str1;
		//int num1 = (int)str1;//"123"

		int num1 = Integer.parseInt(str1);
		System.out.println(num1);//123
	}
}
```






##### 数据类型运算规则

###### 自动类型提升

>结论：当容量小的数据类型的变量与容量大的数据类型的变量做运算时，结果自动提升为容量大的数据类型。
>	byte 、char 、short --> int --> long --> float --> double 
>
>特别的：当byte、char、short三种类型的变量做运算时，结果为int型



- 代码示例

  ```java
  class VariableTest2 {
  	public static void main(String[] args) {
  		
  		byte b1 = 2;
  		int i1 = 129;
  		//编译不通过
  		//byte b2 = b1 + i1;
  		int i2 = b1 + i1;
  		long l1 = b1 + i1;
  		System.out.println(i2);
  
  		float f = b1 + i1;
  		System.out.println(f);
  
  		short s1 = 123;
  		double d1 = s1;
  		System.out.println(d1);//123.0
  
  		//***************特别地*********************
  		char c1 = 'a';//97
  		int i3 = 10;
  		int i4 = c1 + i3;
  		System.out.println(i4);
  
  		short s2 = 10;
  		//char c2  = c1 + s2;//编译不通过
  
  		byte b2 = 10;
  		//char c3 = c1 + b2;//编译不通过
  
  		//short s3 = b2 + s2;//编译不通过
  
  		//short s4 = b1 + b2;//编译不通过
  		//****************************************
  
  	}
  }
  
  ```

###### 强制类型转换

> 自动类型提升运算的逆运算。
>
> 1. 需要使用强转符：()
> 2. 注意点：强制类型转换，可能导致精度损失。
> 3. 整型常量，默认类型为int型  int可以指给其他类型
> 4. 浮点型常量，默认类型为double型  



- 代码示例

  ``` java
  class VariableTest3 {
  	public static void main(String[] args) {
  		
  		double d1 = 12.9;
  		//精度损失举例1
  		int i1 = (int)d1;//截断操作
  		System.out.println(i1);
  		
  		//没有精度损失
  		long l1 = 123;
  		short s2 = (short)l1;
  		
  		//精度损失举例2
  		int i2 = 128;
  		byte b = (byte)i2;
  		System.out.println(b);//-128
  
  	}
  }
  
  class VariableTest4 {
  	public static void main(String[] args) {
  		
  		//1.编码情况1：
  		long l = 123213;
  		System.out.println(l);
  		//编译失败：过大的整数
  		//long l1 = 21332423235234123;
  		long l1 = 21332423235234123L;
  
  
  		//****************
  		//编译失败
  		//float f1 = 12.3;
  		float f1 = (float)12.3;
  		//2.编码情况2：
  		//整型常量，默认类型为int型
  		//浮点型常量，默认类型为double型
  		byte b = 12;
  		//byte b1 = b + 1;//编译失败
  
  		//float f1 = b + 12.3;//编译失败
  		
  	}
  }
  
  ```


##### 生命周期

> 成员变量  vs  局部变量

### 运算符

#### 算术运算符

- 代码演示

``` java
/*
运算符之一：算术运算符
+ - + - * / % (前)++ (后)++ (前)-- (后)-- +
*/
class AriTest {
	public static void main(String[] args) {
		
		//除号：/
		int num1 = 12;
		int num2 = 5;
		int result1 = num1 / num2;
		System.out.println(result1);//2

		int result2 = num1 / num2 * num2;
		System.out.println(result2);//10

		double result3 = num1 / num2;
		System.out.println(result3);//2.0

		double result4 = num1 / num2 + 0.0;//2.0
		double result5 = num1 / (num2 + 0.0);//2.4
		double result6 = (double)num1 / num2;//2.4
		double result7 = (double)(num1 / num2);//2.0
		System.out.println(result5);
		System.out.println(result6);

		// %:取余运算
		//结果的符号与被模数的符号相同
		//开发中，经常使用%来判断能否被除尽的情况。
		int m1 = 12;
		int n1 = 5;
		System.out.println("m1 % n1 = " + m1 % n1);

		int m2 = -12;
		int n2 = 5;
		System.out.println("m2 % n2 = " + m2 % n2);

		int m3 = 12;
		int n3 = -5;
		System.out.println("m3 % n3 = " + m3 % n3);

		int m4 = -12;
		int n4 = -5;
		System.out.println("m4 % n4 = " + m4 % n4);
		
		
		//(前)++ :先自增1，后运算
		//(后)++ :先运算，后自增1
		int a1 = 10;
		int b1 = ++a1;
		System.out.println("a1 = " + a1 + ",b1 = " + b1);
		
		int a2 = 10;
		int b2 = a2++;
		System.out.println("a2 = " + a2 + ",b2 = " + b2);
		
		int a3 = 10;
		++a3;//a3++;
		int b3 = a3;
		
		//注意点：
		short s1 = 10;
		//s1 = s1 + 1;//编译失败
		//s1 = (short)(s1 + 1);//正确的
		s1++;//自增1不会改变本身变量的数据类型
		System.out.println(s1);

		//问题：
		byte bb1 =127;
		bb1++;
		System.out.println("bb1 = " + bb1);

		//(前)-- :先自减1，后运算
		//(后)-- :先运算，后自减1
		
		int a4 = 10;
		int b4 = a4--;//int b4 = --a4;
		System.out.println("a4 = " + a4 + ",b4 = " + b4);

	}
}

```





### 流程控制

#### if else  elseif

### 数组

#### 算法

#### 数据结构

## 面向对象编程 

### 类/对象

### 类的结构

### 三大特性

### 接口

### 设计模式

