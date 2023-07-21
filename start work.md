# overview
* C primer plus page 13 ,14  page 25 summary
	>C has the advantage that the principles of structured programming improved the clarity, reliability, and ease of maintenance of programs, large-scale programming still remains a challenge.  
	
	C++ OOP&Generic programing&Templates help to figure out the problems.
# get start
```C++  
#include <iostream>
using namespace std;
class date/*类的名称date*/{
public://声明公有成员，可在类外访问
	void setdate(int y,int m,int d);
	int isleapyear();
	void print();
private://类的私有成员，只能在类里面访问(hide data)
	int year;
	int month;
	int day;
};
main()
{
date time;//创建date类的一个对象time
}
```
The basic rules are the same with C
**preprogram directives** begin with #,when it's to be compile, preprosser
will use the content that the directive points at to replace the line
**head filenames
* C++ head filename has difference with C  
	* C++don't use the h extension with header files as a simple way to identify the type of file by its name.
	* There are also C header files that have been converted to C++ header files.These files have been renamed by dropping the h extension (making it a C++-stylename) and prefixing the filename with a c,such as ***cmath  
	* Anyway C++ programs can still use old C head filenames
**namespace overview**
why use it? 
>A big C++program may involve some alreday  existing code from several vendors  to help organize programs.,they may have some functions in the same name ,to indicate which vendor’s product you want,  
  Microflop Industries could place its definitions in a namespace called Microflop.Then Microflop::wanda() would become the full name for its wanda() function. Similarly, Piscine::wanda() could denote Piscine Corporation’s version of wanda().Thus, your program could now use the namespaces to discriminate between various versions   

namespace prefix
>example: using namespace std;
>This using directive makes all the names in the std namespace available.In this way,std::cout can be replaced with cout or you must use std::cout to identify it.

# cin&cout
cout,输出其后<<所接的待输出内容,且可输出多个
如cout<<"good\n"<<"handsome"<<a;一个部分对应一个<<,均结束后再以分号结尾哪些东西需要在双引号里,参照scanf
**endl**换行标志,cout<<endl,即换行
# cin
cin>>variable;
## c++创建变量时需初始化,否则报错
* 定义常量,有宏常量,和用const修饰的常量两种形式
	```C++
	//1、宏常量
#define day 7

int main() {

	cout << "一周里总共有 " << day << " 天" << endl;
	//day = 8;  //报错，宏常量不可以修改
	//2、const修饰变量
	const int month = 12;
	cout << "一年里总共有 " << month << " 个月份" << endl;
	//month = 24; //报错，常量是不可以修改的
	
	
	system("pause");
	return 0;
	}
	```
	* 字符串,C风格: char str[1]="string";
		C++风格: string str = "hello world"; // 需包含头文件#include/<string/>  
* 布尔类型bool
	 bool类型只有两个单字节值：

		  true --- 真（本质是1）
		 false --- 假（本质是0）
int main() {
	bool flag = true;
	cout << flag << endl; // 1

	flag = false;
	cout << flag << endl; // 0

	cout << "size of bool = " << sizeof(bool) << endl; //1
	
	system("pause");

	return 0;
}//
# 函数的分文件编写
1.  创建后缀名为.h的头文件
2.  创建后缀名为.cpp的源文件
3.  在头文件中写函数的声明
4.  在源文件中写函数的实现
即将源文件分为函数.cpp,main.cpp，分别写函数的定义和主程序，函数的声明及说明放头文件
作用:简明,查找相关函数,直接在头文件中查看,需要查看相关实现时,再在源文件中寻找查看

**命名空间,namespace**
namespace A,创建了命名空间A,相当于创建了一个用户自己命名的内存区域
在命名空间中定义变量,
namespace namespace_name {
// 声明或定义变量、函数、类等 
}
通过作用域标识进行访问
例如，假设有一个命名空间`myNamespace`，其中定义了一个函数`myFunction`，可以通过`myNamespace::myFunction()`来访问该函数。

目的是实现对变量名的分块管理
例:
```cpp
namespace Math {
int add(int a, int b) 
{ return a + b; } 
} 
namespace Physics { double calculateForce(double mass, double acceleration)
{ return mass * acceleration;
}
}
```



**异常处理**
异常就是程序在执行过程中，由于使用环境变化和用户操作等原因产生的错误，从而影响程序的运行。

异常处理是一种编程技术，用于在程序运行时处理可能出现的错误或异常情况。当程序在执行过程中遇到错误或无法继续正常执行时，它会抛出一个异常。异常处理机制允许我们在适当的地方捕获这些异常，并采取相应的措施来处理它们，从而使程序能够优雅地处理错误情况，而不会崩溃或产生未定义行为。

- 程序中常见的错误：语法错误，运行错误
- 异常处理机制的组成：检查异常（try）、抛出异常（throw）、捕获并处理异常（catch）


在C++中，异常处理主要通过 `try`、`catch` 和 `throw` 三个关键字来实现。
1. `try`：在 `try` 块中包含可能抛出异常的代码段。如果在 `try` 块中的代码执行过程中发生异常，程序会立即跳转到相应的 `catch` 块。
    
2. `catch`：`catch` 块用于捕获异常并处理它。在 `catch` 块中，我们可以定义一个或多个异常处理程序，每个处理程序与特定类型的异常相关联。当异常与某个处理程序相匹配时，程序会执行相应的处理代码。
    
3. `throw`：`throw` 关键字用于抛出异常。在 `try` 块内部的代码段可以通过 `throw` 关键字来手动引发异常。我们可以在 `throw` 语句中指定一个异常对象，这个异常对象可以是任意类型。

```cpp
#include <iostream>
using namespace std;

double divideNumbers(double a, double b) {
    if (b == 0) {
        throw "Division by zero is not allowed!";
    }
    return a / b;
}

int main() {
    double num1, num2;
    cout << "Enter two numbers: ";
    cin >> num1 >> num2;

    try {
        double result = divideNumbers(num1, num2);
        cout << "Result: " << result << endl;
    } catch (const char* errorMsg) {
        cout << "Exception caught: " << errorMsg << endl;
    }

    return 0;
}

```
正常情况下,除数是0会导致程序崩溃退出,这里使用错误处理的方式,优雅地解决了这一问题,在除数是0是,throw出异常对象,此处是那段话(字符串),异常对象被抛出到程序的调用栈中,寻找相应的异常处理程序,即匹配的catch代码块,执行错误处理,并跳过try代码块剩余内容.

匹配catch代码块规则是根据抛出异常类型匹配的,此处为字符串,因而匹配接受char\*为参数的catch代码块

一个try后可以接多个接受不同异常类型为参数的catch