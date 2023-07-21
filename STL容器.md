## 基本概念

-   STL(Standard Template Library,**标准模板库**)
-   STL 从广义上分为: **容器(container) 算法(algorithm) 迭代器(iterator)**
-   **容器**和**算法**之间通过**迭代器**进行无缝连接。
-   STL 几乎所有的代码都采用了模板类或者模板函数   
## STL六大组件

STL大体分为六大组件，分别是:**容器、算法、迭代器、仿函数、适配器（配接器）、空间配置器**

1.  容器：各种数据结构，如vector、list、deque、set、map等,用来存放数据。
2.  算法：各种常用的算法，如sort、find、copy、for_each等
3.  迭代器：扮演了容器与算法之间的胶合剂。
4.  仿函数：行为类似函数，可作为算法的某种策略。
5.  适配器：一种用来修饰容器或者仿函数或迭代器接口的东西。
6.  空间配置器：负责空间的配置与管理。

### 容器算法与迭代器

1.vector容器
	C++中的vector是一个动态数组容器，可以自动扩容并提供了许多便利的操作和算法，是STL中最常用的容器之一。其实现基本与模板章节的最后一个实例相同,相当于一个可以存储各种类型元素的数组,不过一般数组是静态空间,而vector可以**动态扩展**(不是在源空间后拼接新空间,而是在内存中寻找空间,将原数据拷贝到新空间).
	以下是关于vector的常见操作和算法
	
 1.  创建vector容器
可以使用以下语句来创建一个空的vector容器：
`#include <vector> std::vector<int> myVector;`
```cpp
//vector实现函数提供了四种构造函数,可用下面四种方式初始化
	vector<int> v1; //无参构造
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	printVector(v1);

	vector<int> v2(v1.begin(), v1.end());//将begin到end的元素依次赋到v2中
	printVector(v2);

	vector<int> v3(10, 100);//-   `vector(n, elem);` //构造函数将n个elem拷贝给本身。
	printVector(v3);
	
	vector<int> v4(v3);
	printVector(v4);
```
2.  向vector中添加元素
可以使用push_back()函数将元素添加到vector末尾，如下所示：
`myVector.push_back(1); // 添加一个整数1到myVector中`
向vector对象赋值
-   `vector& operator=(const vector &vec);`//重载等号操作符
    
-   `assign(beg, end);` //将==\[beg, end)区间==中的数据拷贝赋值给本身。
	- 注意:左闭右开区间,两个参数可以是指针,也可以是迭代器,一般用v1.assign(v2.begin(),v2.end())将v2赋值给v1
    
-   `assign(n, elem);` //将n个elem拷贝赋值给本身。
3.  访问vector元素
可以使用下标操作符[ ]或at()函数来访问vector中的元素，如下所示：
```cpp
int x = myVector[0]; // 获取第一个元素 int y = myVector.at(1); // 获取第二个元素`
```
4.  获取vector容量和大小
可以使用size()函数获取vector中元素的个数，如下所示：
```cpp
`int size = myVector.size(); // 获取myVector中元素的个数`
```
另外提供了这些函数
-   `empty()` 函数用于判断容器是否为空，返回值为 `bool` 类型，若容器为空则返回 `true`，否则返回 `false`。
-   `capacity()` 函数用于返回当前容器能够容纳的元素数量，即容器的容量。
-   `size()` 函数用于返回容器中实际存储的元素数量。
-   `resize(int num)` 函数用于重新指定容器的长度为 `num`，如果容器变长，则以默认值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。
-   `resize(int num, elem)` 函数用于重新指定容器的长度为 `num`，如果容器变长，则以 `elem` 值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。
- 预留空间: `reserve(int len);`//容器预留len个元素长度，预留位置不初始化，元素不可访问。 ​
5.  插入和删除元素
可以使用insert()函数在任意位置插入元素，使用erase()函数删除任意位置的元素，如下所示：
```cpp
myVector.insert(myVector.begin() + 1, 2); // 在第二个位置插入一个整数2 myVector.erase(myVector.begin() + 1); // 删除第二个元素`
```
全部函数
-   `push_back(ele);` //尾部插入元素ele
-   `pop_back();` //删除最后一个元素
-   `insert(const_iterator pos, ele);` //迭代器指向位置pos插入元素ele
-   `insert(const_iterator pos, int count,ele);`//迭代器指向位置pos插入count个元素ele
-   `erase(const_iterator pos);` //删除迭代器指向的元素
-   `erase(const_iterator start, const_iterator end);`//删除迭代器从start到end之间的元素
-   `clear();` //删除容器中所有元素
6.  排序与元素互换
可以使用sort()函数对vector中的元素进行排序，如下所示：
```cpp
`std::sort(myVector.begin(), myVector.end()); // 对myVector进行升序排序`
```
注意:sort函数是包含在头文件 `<algorithm>`中的函数,不是vector类的成员函数.

swap函数,是vector类的成员函数,用于两容器内容的交换

7.  迭代器
vector的迭代器提供了一种方便的方式来遍历vector中的元素。例如，以下代码使用迭代器打印myVector中的所有元素：
```cpp
`for (std::vector<int>::iterator it = myVector.begin(); it != myVector.end(); ++it) {     std::cout << *it << " "; }`

其中，begin()函数返回指向vector开头(第一个元素)的迭代器，**end()函数返回指向vector结尾后一个位置的迭代器**。可以使用++运算符将迭代器向前移动，并使用*运算符访问迭代器指向的元素。另外,还有front()和back()函数,他们分别返回容器中第一个和最后一个数据元素
```
==end函数返回最后一个元素后一个位置的迭代器==,不能解引用,主要目的是为了方便遍历容器中元素
* vector容器嵌套容器示例
```cpp
#include <vector>

//容器嵌套容器
void test01() {

	vector< vector<int> >  v;

	vector<int> v1;
	vector<int> v2;
	vector<int> v3;
	vector<int> v4;

	for (int i = 0; i < 4; i++) {
		v1.push_back(i + 1);
		v2.push_back(i + 2);
		v3.push_back(i + 3);
		v4.push_back(i + 4);
	}

	//将容器元素插入到vector v中
	v.push_back(v1);
	v.push_back(v2);
	v.push_back(v3);
	v.push_back(v4);


	for (vector<vector<int>>::iterator it = v.begin(); it != v.end(); it++) {

		for (vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++) {
			cout << *vit << " ";
		}
		cout << endl;
	}

}

int main() {

	test01();

	system("pause");

	return 0;
}
```
 2.string容器
	-   string是C++风格的字符串，而string本质上是一个类
	- string和char * 区别：
		-   char * 是一个指针
		-   string是一个类，类内部封装了char*，管理这个字符串，是一个char*型的容器。
	特点
	string 类内部封装了很多成员方法
	例如：查找find，拷贝copy，删除delete 替换replace，插入insertstring管理char*所分配的内存，不用担心复制越界和取值越界等，由类内部进行负责
	string类:
		1.构造函数:提供了多种构造函数原型
		-   `string();` //创建一个空的字符串 例如: string str; `string(const char* s);` //使用字符串s初始化
		-   `string(const string& str);` //使用一个string对象初始化另一个string对象
		-   `string(int n, char c);` //使用n个字符c初始化
		2.赋值操作的成员函数
		功能描述：
		-   给string字符串进行赋值
		  赋值的函数原型：
		string& operator=(const char\* s); //char\*类型字符串 赋值给当前的字符串
		string& operator=(const string &s); //把字符串s赋给当前的字符串
		string& operator=(char c); //字符赋值给当前的字符串
		string& assign(const char \*s); //把字符串s赋给当前的字符串
		string& assign(const char \*s, int n); //把字符串s的前n个字符赋给当前的字符串
		string& assign(const string &s); //把字符串s赋给当前字符串
		string& assign(int n, char c); //用n个字符c赋给当前字符串
		3.字符串的拼接
		**函数原型：**
		-   `string& operator+=(const char* str);` //重载+=操作符
		-   `string& operator+=(const char c);` //重载+=操作符
		-   `string& operator+=(const string& str);` //重载+=操作符
		-   `string& append(const char *s);`  //把字符串s连接到当前字符串结尾
		-   `string& append(const char *s, int n);` //把字符串s的前n个字符连接到当前字符串结尾
		 -   `string& append(const string &s);` //同operator+=(const string& str)
		-   `string& append(const string &s, int pos, int n);`//字符串s中从pos开始的n个字符连接到字符串结尾
		**总结**
		赋值和拼接等操作有多种方式实现,相应使用方法也比较符合语言习惯
	Advanced features
	**string查找和替换**
	-   查找：查找指定字符串是否存在
	-   替换：在指定的位置替换字符串
  
在 C++ 中，字符串是通过 `string` 类型来表示的。`string` 类型提供了很多有用的方法来对字符串进行操作，其中包括查找和替换。

==字符串的查找和替换只在母字符串内进行,而不是在整个内存空间中,因此，在 C++ 中进行字符串查找和替换操作通常是安全和高效的，因为它们只涉及到字符串本身的操作，而不会影响内存中其他数据的状态。==

## string构造与赋值
####  string构造函数

构造函数原型：

- `string();` //创建一个空的字符串 例如: string str; `string(const char* s);` //使用字符串s初始化
- `string(const string& str);` //使用一个string对象初始化另一个string对象
- `string(int n, char c);` //使用n个字符c初始化

赋值提供了等号运算符重载和assign函数
- `string& operator=(const char* s);` //char*类型字符串 赋值给当前的字符串
- `string& operator=(const string &s);` //把字符串s赋给当前的字符串
- `string& operator=(char c);` //字符赋值给当前的字符串
- `string& assign(const char *s);` //把字符串s赋给当前的字符串
- `string& assign(const char *s, int n);` //把字符串s的前n个字符赋给当前的字符串
- `string& assign(const string &s);` //把字符串s赋给当前字符串
- `string& assign(int n, char c);` //用n个字符c赋给当前字符串
还提供了加号运算符的重载用于拼接字符串,也有append函数
- `string& operator+=(const char* str);` //重载+=操作符
- `string& operator+=(const char c);` //重载+=操作符
- `string& operator+=(const string& str);` //重载+=操作符
- `string& append(const char *s);`  //把字符串s连接到当前字符串结尾
- `string& append(const char *s, int n);` //把字符串s的前n个字符连接到当前字符串结尾
- `string& append(const string &s);` //同operator+=(const string& str)
- `string& append(const string &s, int pos, int n);`//字符串s中从pos开始的n个字符连接到字符串结尾
## 字符串查找

`string` 类型提供了三种查找字符串的方法：`find()`，`rfind()` 和 `find_first_of()`。

### `find()`

`find()` 方法查找一个字符串中第一次出现另一个字符串的位置。如果找到了该字符串，方法将返回该字符串的起始位置的索引值。如果未找到该字符串，方法将返回`string::npos`
```cpp
`string str = "hello world"; size_t pos = str.find("world"); if (pos != string::npos) {     cout << "Found at position " << pos << endl; } else {     cout << "Not found" << endl; }`
```
### `rfind()`

`rfind()` 方法与 `find()` 方法类似，但它从字符串的末尾开始查找。
```cpp
`string str = "hello world"; size_t pos = str.rfind("l"); if (pos != string::npos) {     cout << "Found at position " << pos << endl; } else {     cout << "Not found" << endl; }`
```
### `find_first_of()`

`find_first_of()` 方法查找一个字符串中第一次出现另一个字符串中任意一个字符的位置。
```cpp
`string str = "hello world"; size_t pos = str.find_first_of("aeiou"); if (pos != string::npos) {     cout << "Found at position " << pos << endl; } else {     cout << "Not found" << endl; }`
```
## 字符串替换

`string` 类型提供了两种替换字符串的方法：`replace()` 和 `substr()`。
### `replace()`
`replace()` 方法替换一个字符串中的一部分内容。它接受三个参数：起始位置，替换长度和替换的字符串。
```cpp
`string str = "hello world"; str.replace(6, 5, "there"); cout << str << endl;  // 输出 "hello there"`
```
### `substr()`
`substr()` 方法返回一个字符串中从指定位置开始的指定长度的子字符串。
```cpp

`string str = "hello world"; string substr = str.substr(6, 5); cout << substr << endl;  // 输出 "world"`
```
使用这些方法，您可以在 C++ 中轻松地查找和替换字符串。
注:这些函数原型都是使用int pos来定位,pos即位置,其为int型,称为索引值或下标,与数组类似,相当于相对于字符串首字符的偏移量

## 字符串比较
**比较方式：**

-   字符串比较是按字符的ASCII码进行对比

= 返回 0

\> 返回 1

< 返回 -1

  `compare()`: `string` 类型的成员函数，用于比较两个字符串是否相等。该函数返回值为 0 表示两个字符串相等，返回值为负数表示第一个字符串小于第二个字符串，返回值为正数表示第一个字符串大于第二个字符串。
用例：
```cpp
string s1 = "hello";
	string s2 = "aello";

	int ret = s1.compare(s2);

	if (ret == 0) {
		cout << "s1 等于 s2" << endl;
	}
	else if (ret > 0)
	{
		cout << "s1 大于 s2" << endl;
	}
	else
	{
		cout << "s1 小于 s2" << endl;
	}
```

 
 string字符存取
	string中单个字符存取方式有两种
	-   `char& operator[](int n);`  //通过[ ]方式取字符
	-   `char& at(int n);`  //通过at方法获取字符
	即通过预算符重载或at函数,可以通过索引值访问
string的插入与删除
	函数原型：
-   `string& insert(int pos, const char* s);`  //插入字符串
-   `string& insert(int pos, const string& str);`  //插入字符串
-   `string& insert(int pos, int n, char c);` //在指定位置插入n个字符c
-   `string& erase(int pos, int n = npos);` //删除从Pos开始的n个字符
即str.insert(插入的位置,插入的内容)
从字符串中提取子串
	函数原型：
-   `string substr(int pos = 0, int n = npos) const;` //返回由pos开始的n个字符组成的字符串

### deque(double-ended queue)双端队列容器
![图片](D:\junk\clip_image002-1547547642923.jpg)
#### deque与vector区别
deque容器和vector容器都是C++中的顺序容器，但它们之间有一些不同之处。与vector相比，deque额外增加了实现在容器头部添加和删除元素的成员函数push_front()和pop_front()，同时删除了capacity()、reserve()和data()成员函数。当需要向序列两端频繁的添加或删除元素时，应首选deque容器。

deque内部的存储结构是分段连续的，但是段和段之间的数据是不一定是连续的。这意味着deque允许使用常数项时间对头端进行元素的插入和删除操作2。另外，deque没有容量的概念，因为它是动态的以分段连续空间组合而成，随时可以增加一段新的空间并链接起来。
#### deque的一些用法
1.赋值,构造等
	与vector容器相同
2.deque容器的大小操作
-   `deque.empty();` //判断容器是否为空
    
-   `deque.size();` //返回容器中元素的个数
    
-   `deque.resize(num);` //重新指定容器的长度为num,若容器变长，则以默认值填充新位置。
    
    ​ //如果容器变短，则末尾超出容器长度的元素被删除。
    
-   `deque.resize(num, elem);` //重新指定容器的长度为num,若容器变长，则以elem值填充**新位置**。
    
    ​ //如果容器变短，则末尾超出容器长度的元素被删除。
3.插入删除数据
* 两端插入操作：

- `push_back(elem);` //在容器尾部添加一个数据
- `push_front(elem);` //在容器头部插入一个数据
- `pop_back();` //删除容器最后一个数据
- `pop_front();` //删除容器第一个数据

指定位置操作：

- `insert(pos,elem);` //在pos位置插入一个elem元素的拷贝，返回新数据的位置。
    
- `insert(pos,n,elem);` //在pos位置插入n个elem数据，无返回值。
    
- `insert(pos,beg,end);` //在pos位置插入[beg,end)区间的数据，无返回值。
    
- `clear();` //清空容器的所有数据
    
- `erase(beg,end);` //删除[beg,end)区间的数据，返回下一个数据的位置。
    
- `erase(pos);` //删除pos位置的数据，返回下一个数据的位置。
取数据\
* at(index);或[]运算符;
* front();back()返回首元素,返回尾元素
排序
* 使用排序函数
 `sort(iterator beg, iterator end)` //对beg和end区间内元素进行排序

## STACK容器
先进后出
- `stack<T> stk;` //stack采用模板类实现， stack对象的默认构造形式
- `stack(const stack &stk);` //拷贝构造函数

赋值操作：

- `stack& operator=(const stack &stk);` //重载等号操作符

数据存取：

- `push(elem);` //向栈顶添加元素
- `pop();` //从栈顶移除第一个元素
- `top();`  //返回栈顶元素

大小操作：

- `empty();` //判断堆栈是否为空
- `size();`  //返回栈的大小

## queue容器
只允许先进先出,头进尾出,只支持头尾元素的访问
![[Pasted image 20230616123330.png]]
构造函数：

- `queue<T> que;` //queue采用模板类实现，queue对象的默认构造形式
- `queue(const queue &que);` //拷贝构造函数

赋值操作：

- `queue& operator=(const queue &que);` //重载等号操作符

数据存取：

- `push(elem);` //往队尾添加元素
- `pop();` //从队头移除第一个元素
- `back();` //返回最后一个元素
- `front();`  //返回第一个元素

大小操作：

- `empty();` //判断堆栈是否为空
- `size();`  //返回栈的大小

## 链表(list)
链表（Linked List）是一种常见的数据结构，用于存储和组织数据。它由一系列节点组成，每个节点包含数据和一个指向下一个节点的指针（或引用）。相邻节点之间通过指针链接在一起，形成链式结构。
常见的链表类型包括单向链表（Singly Linked List）、双向链表（Doubly Linked List）和循环链表（Circular Linked List）。下面对每种链表进行详细讲解：

1. 单向链表（Singly Linked List）：每个节点包含数据和一个指向下一个节点的指针。最后一个节点的指针通常指向空（nullptr）。单向链表只允许从头节点开始顺序访问，无法快速访问到前一个节点。常用操作包括在链表头部插入节点、在链表尾部插入节点、在指定位置插入节点、删除节点和查找节点等。
    
2. 双向链表（Doubly Linked List）：每个节点包含数据、一个指向前一个节点的指针和一个指向后一个节点的指针。双向链表可以双向遍历，可以从头节点或尾节点开始遍历，相比单向链表，可以更方便地进行插入、删除和查找操作。但是双向链表相对于单向链表需要额外的内存空间存储指向前一个节点的指针。
    
3. 循环链表（Circular Linked List）：最后一个节点的指针指向链表的头部，形成一个循环。循环链表可以用于实现循环访问的需求，例如循环队列。操作和单向链表类似，但需要特别注意循环的结束条件。
C++提供的list容器属于双向链表
由于list不是连续内存空间,进行遍历和实现算法时必须用迭代器,且迭代器只支持向前,向后移动
list的优点：

- 采用动态存储分配，不会造成内存浪费和溢出
- 链表执行插入和删除操作十分方便，修改指针即可，不需要移动大量元素

list的缺点：

- 链表灵活，但是空间(指针域) 和 时间（遍历）额外耗费较大

List有一个重要的性质，插入操作和删除操作都不会造成原有list迭代器的失效，这在vector是不成立的。

## 构造函数
**函数原型：**

- `list<T> lst;` //list采用采用模板类实现,对象的默认构造形式：
- `list(beg,end);` //构造函数将\[beg, end)区间中的元素拷贝给本身。
- `list(n,elem);` //构造函数将n个elem拷贝给本身。
- `list(const list &lst);` //拷贝构造函数。

## 赋值和交换
- `assign(beg, end);` //将\[beg, end)区间中的数据拷贝赋值给本身。
- `assign(n, elem);` //将n个elem拷贝赋值给本身。
- `list& operator=(const list &lst);` //重载等号操作符
- `swap(lst);` //将lst与本身的元素互换(交换两个链表的数据)

## 大小操作
- `size();`  //返回容器中元素的个数
    
- `empty();`  //判断容器是否为空
    
- `resize(num);` //重新指定容器的长度为num，若容器变长，则以默认值填充新位置。
    
    ​ //如果容器变短，则末尾超出容器长度的元素被删除。
    
- `resize(num, elem);`  //重新指定容器的长度为num，若容器变长，则以elem值填充新位置。
## 插入删除元素
- push_back(elem);//在容器尾部加入一个元素
- pop_back();//删除容器中最后一个元素
- push_front(elem);//在容器开头插入一个元素
- pop_front();//从容器开头移除第一个元素
- insert(pos,elem);//在pos位置插elem元素的拷贝，返回新数据的位置。
- insert(pos,n,elem);//在pos位置插入n个elem数据，无返回值。
- insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据，无返回值。
- clear();//移除容器的所有数据
- erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置。
- erase(pos);//删除pos位置的数据，返回下一个数据的位置。
- remove(elem);//删除容器中所有与elem值匹配的元素。



数据存取,只支持- `front();` //返回第一个元素。
- `back();` //返回最后一个元素。
- list容器中不可以通过[]或者at方式访问数据
反序和排序
- `reverse();` //反转链表
- `sort();` //链表排序,默认为升序,也可接受一个参数(比如自定义比较函数,返回布尔值),根据参数进行升序或降序排序
```cpp
bool ComparePerson(Person& p1, Person& p2) {

	if (p1.m_Age == p2.m_Age) {
		return p1.m_Height  > p2.m_Height;
	}
	else
	{
		return  p1.m_Age < p2.m_Age;
	}
	L.sort(ComparePerson);
```
 根据比较结果，`sort` 函数确定了这两个元素的相对顺序。如果比较结果为 `true`，则第一个元素在第二个元素之前；如果比较结果为 `false`，则第一个元素在第二个元素之后。
因此这个程序排序的准则是先按照年龄升序排列，如果年龄相同，则按照身高降序排列。

## set/multiset容器
1.概念:
`std::set` 和 `std::multiset` 是 C++ 标准库中的关联容器，前者用于存储一组不重复的元素,并自动排序。后者允许存储重复元素
**简介：**
在 C++ 的 `std::set` 中，键值指的是用于比较和排序元素的属性或值。
例如，对于整数类型的 `std::set`，默认情况下将使用元素值作为键值。对于字符串类型的 `std::set`，默认情况下将使用字符串的字典顺序作为键值
1. `std::set` 容器：
    
    - `std::set` 是一个有序集合容器，其中的元素按照键值自动进行排序。
    - 它不允许重复的元素，每个元素在容器中都是唯一的。
    - 元素是不可修改的，一旦插入到容器中，就不能再更改其键值。
    - `std::set` 使用红黑树作为底层数据结构，这使得插入、删除和查找操作的平均时间复杂度为 O(log n)，其中 n 是容器中的元素数量。
    - `std::set` 提供了一系列的成员函数，例如 `insert`、`erase`、`find` 等，用于操作和访问容器中的元素。
2. `std::multiset` 容器：
    
    - `std::multiset` 是一个有序的集合容器，允许存储重复的元素。
    - 它与 `std::set` 相似，但不会进行元素的唯一性检查，允许容器中存在相同键值的元素。
    - `std::multiset` 使用红黑树作为底层数据结构，同样具有 O(log n) 的平均时间复杂度。
    - `std::multiset` 也提供了类似于 `std::set` 的成员函数，用于操作和访问容器中的元素。

以下是一些常见的操作和特性，适用于 `std::set` 和 `std::multiset` 容器：

- 插入元素：可以使用 `insert` 函数将一个元素插入容器中。
- 删除元素：可以使用 `erase` 函数删除指定值的元素，或使用迭代器删除指定位置的元素。
- 查找元素：可以使用 `find` 函数查找指定值的元素，并返回迭代器指向该元素。
- 元素计数：可以使用 `count` 函数计算指定值的元素在容器中出现的次数。
- 迭代访问：可以使用迭代器遍历容器中的所有元素，或使用范围循环进行遍历。
- 容器大小：可以使用 `size` 函数获取容器中的元素数量。empty()是否为空
- 容器清空：可以使用 `clear` 函数清空容器中的所有元素。

2.提供的函数及注意
除简介中函数,也支持swap函数
由于自动排序,故insert函数只有一个参数,即插入的元素,不用位置参数,因为位置由排序确定
- `find(key);` //查找key是否存在,若存在，返回该键的元素的迭代器；若不存在，返回set.end();
- `count(key);` //统计key的元素个数(显然用于multiset)

3.排序规则
默认为从小到大
改变排序规则的方法:
法一:定义一个数据类.并为其定义一个比较器
```cpp
struct MyCompare { 
bool operator()(int a, int b) const { 
// 根据自定义的比较逻辑进行排序 
return a % 10 < b % 10; } }; 
int main() { 
// 创建set对象并使用自定义比较器 
std::set<int, MyCompare> s2;
```
注:C++中struct和class均定义类,区别在struct定义内容权限均为public
`set`的构造函数有多个重载形式，其中一个形式接受一个比较器作为参数。该比较器可以是函数指针、函数对象或仿函数类型。
法二:在定义数据类时,对<运算符重载,`set` 将使用该运算符对数据类进行排序。
法三:自定义比较函数
```cpp
bool messageCmp(const message &a, const message &b) {
            if (a.age == b.age)
                return a.name < b.name;
            else
                return a.age < b.age;
        }

int main() {

    set<message, decltype(messageCmp)*> set(messageCmp) ;

    set.insert(message(7,"Tony"));
    set.insert(message(4,"Jbse"));
    set.insert(message(4,"Jane"));

    for (auto it = set.begin(); it != set.end(); ++it)
        cout<<it->age<<"->"<<it->name<<endl;

```
使用此方法,set接受的比较器为函数指针,C++11新标准引入了类型指示符[decltype](https://so.csdn.net/so/search?q=decltype&spm=1001.2101.3001.7020)，它的作用是返回操作数的数据类型。因此decltype(messageCmp)返回的就是函数类型,在后面加个\*就表示指向函数类型的指针即函数指针了;
而创建set对象时,在()内加messageCmp函数名,因为函数名相当于函数指针,即这里是调用构造函数将函数指针传递给比较器
## pari对组的创建
用于创建包含两个元素的对组。每个对组中的元素可以具有不同的类型，允许将两个不同类型的值组合在一起。
要创建一个 `std::pair` 对组，可以使用以下语法：
```cpp
`std::pair<T1, T2> pair_name(value1, value2);`
```
其中，`T1` 和 `T2` 是两个元素的类型，`pair_name` 是对组的变量名，`value1` 和 `value2` 是要存储在对组中的两个值。
我们可以通过 `my_pair.first` 和 `my_pair.second` 来访问对组中的两个元素，并且可以修改对组中的元素的值。

## map/multimap
当需要将键与值结合起来存储数据时使用
简介:
- map中所有元素都是pair
- pair中第一个元素为key（键值），起到索引作用，第二个元素为value（实值）
- 所有元素都会根据元素的键值自动排序
- 内部使用红黑树（Red-Black Tree）实现，它保证了对数时间复杂度的查找、插入和删除操作。
- 通过使用键来访问和修改对应的值。
- multimap允许多个有相同键的元素

构造函数与赋值:
**构造：**

- `map<T1, T2> mp;` //map默认构造函数:
- `map(const map &mp);` //拷贝构造函数

**赋值：**

- `map& operator=(const map &mp);` //重载等号操作符

支持size,empty,swap函数
插入和删除
- `insert(elem);` //在容器中插入元素。
- `clear();` //清除所有元素
- `erase(pos);` //删除pos迭代器所指的元素，返回下一个元素的迭代器。
- `erase(beg, end);` //删除区间\[beg,end)的所有元素 ，返回下一个元素的迭代器。
- `erase(key);` //删除容器中值为key的元素。

查找与统计
- `find(key);` //查找key是否存在,若存在，返回该键的元素的迭代器；若不存在，返回set.end();
- `count(key);` //统计key的元素个数
```cpp
map<int, int>::iterator pos = m.find(3);

	if (pos != m.end())
	{
		cout << "找到了元素 key = " << (*pos).first << " value = " << (*pos).second << endl;
	}
	else
	{
		cout << "未找到元素" << endl;
	}
```
与set的区别,set直接使用元素值查找,这里是使用的键值

自定义排序:与set相同


## 函数对象
1.函数对象
* 概念
  - 重载**函数调用操作符**的类，其对象常称为**函数对象**
  - **函数对象**使用重载的()时，行为类似函数调用，也叫**仿函数**
  - 重载( )是对类重载,重载后被视作类的成员函数,可以直接访问类各个对象的私有成员
2.谓词
概念：
- 返回bool类型的仿函数称为**谓词**
- 如果operator()接受一个参数，那么叫做一元谓词
- 如果operator()接受两个参数，那么叫做二元谓词
3.内建函数对象
概念:内建函数对象是指一些预定义的函数对象，它们位于C++标准库中。需引入头文件,# include <functional/>
分类:
* 算数仿函数
* 关系仿函数
* 逻辑仿函数
使用方法:按照调用一般的仿函数(函数对象)的方式使用,显然是模板类,需指定类型,创建类的对象,用()运算符传递参数,进行调用

一、算术仿函数
功能描述：
实现四则运算其中negate是一元运算，其他都是二元运算
仿函数原型：
```cpp
template<class T> T plus<T> //加法仿函数
template<class T> T minus<T> //减法仿函数
template<class T> T multiplies<T> //乘法仿函数
template<class T> T divides<T> //除法仿函数
template<class T> T modulus<T> //取模仿函数
template<class T> T negate<T> //取反仿函数
用例:
#include <functional>
//negate取反
void test01()
{
	negate<int> n;
	cout << n(50) << endl;
}
//plus
void test02()
{
	plus<int> p;
	cout << p(10, 20) << endl;
}
int main() {
	test01();
	test02();
	system("pause");
	return 0;
}

```
结果以返回值形式传递
二、关系仿函数
实现关系对比
仿函数原型：
```cpp
template<class T> bool equal_to<T> //等于
template<class T> bool not_equal_to<T> //不等于
template<class T> bool greater<T> //大于
template<class T> bool greater_equal<T> //大于等于
template<class T> bool less<T> //小于
template<class T> bool less_equal<T> //小于等于
```
三、逻辑仿函数
实现逻辑运算
```cpp
template<class T> bool logical_and<T> //逻辑与
template<class T> bool logical_or<T> //逻辑或
template<class T> bool logical_not<T> //逻辑非
```
了解即可

## STL常用算法
**概述**:

- 算法主要是由头文件`<algorithm>` `<functional>` `<numeric>`组成。
    
- `<algorithm>`是所有STL头文件中最大的一个，范围涉及到比较、 交换、查找、遍历操作、复制、修改等等
    
- `<numeric>`体积很小，只包括几个在序列上面进行简单数学运算的模板函数
    
- `<functional>`定义了一些模板类,用以声明函数对象。
一.常用遍历算法
- `for_each` //遍历容器
- `transform` //搬运容器到另一个容器中
**for_each
	**功能描述：**
	- 实现遍历容器
	- **函数原型：**
	-`Function for_each(iterator beg, iterator end, _func);`
    // 遍历算法 遍历容器元素
       // beg 开始迭代器
      // end 结束迭代器
      // func 函数或者函数对象
     **原理简介**
     - `for_each` 函数首先会通过输入迭代器遍历指定范围内的元素。遍历过程中，它会依次获取迭代器指向的元素，并将其作为参数传递给函数对象。
     - 函数对象会执行对元素的操作，可以是打印、修改、统计等任意操作。这个过程由函数对象的 `operator()` 实现。
     - 在遍历完所有元素后，`for_each` 函数返回传入的函数对象，以便在需要时进行进一步的操作。
     一个简化的实现
```cpp
template <typename InputIterator, typename Function>
Function for_each(InputIterator first, InputIterator last, Function fn) {
    for (; first != last; ++first) {
        fn(*first); // 调用函数对象，传递当前元素
    }
    return fn; // 返回函数对象
}
```
**transform
	**功能描述：**
	- 搬运容器到另一个容器中
	- **函数原型：**
	-`outputIterator transform(iterator beg1, iterator end1, iterator beg2, _func);`
	- //beg1 源容器开始迭代器
	- //end1 源容器结束迭代器
	- //beg2 目标容器开始迭代器
	- //func 函数或者函数对象
	`transform`函数接受四个参数：`first1`和`last1`是输入范围的起始和结束迭代器，`result`是输出范围的起始迭代器，`op`是一个一元操作函数对象（或函数指针）。
	算法遍历输入范围内的每个元素,对于每个输入元素，算法将调用`op`函数，并将当前元素作为参数传递给它。`op`函数可以是函数指针、函数对象（重载了函数调用运算符）或Lambda表达式。
	`op`函数的返回值将被存储到输出范围中，即`result`迭代器指定的位置。然后，`result`迭代器会递增，指向输出范围中的下一个位置。
	当遍历完输入范围中的所有元素时，`transform`算法结束并返回输出范围的结束迭代器
二.常用查找算法
**算法简介：**
- `find` //查找元素
- `find_if` //按条件查找元素
- `adjacent_find` //查找相邻重复元素
- `binary_search` //二分查找法
- `count` //统计元素个数
- `count_if` //按条件统计元素个数
1. find
	   **函数原型：**
    - `find(iterator beg, iterator end, value);`
      以值(value)查找元素,查找自定义类型元素时,注意重载等号,提供判断元素相等的判断方法
2. find_if
    **函数原型：**
     find_if(iterator beg, iterator end, \_Pred);
     `std::find_if`算法接受一个谓词（Predicate）作为参数，用于在给定范围内查找满足特定条件的元素。
     谓词可以是:函数指针,函数对象,lambda函数,要求他们都只接受一个参数    
     ```cpp
     std::vector<int> numbers = {1, 2, 3, 4, 5};
auto it = std::find_if(numbers.begin(), numbers.end(), [](int num) {
    // 根据条件判断 num 是否满足要求
    return num % 2 == 0;
});

     ```

	以上三种方式都可以用作`std::find_if`的谓词参数。它们都用来描述一个条件，这个条件用来判断在范围内的元素是否满足我们想要找到的条件。当找到满足条件的元素时，`find_if`算法将返回指向该元素的迭代器；如果没有找到满足条件的元素，它将返回`end()`迭代器。
3. adjacent_find
      **函数原型：**
   - `adjacent_find(iterator beg, iterator end);`
    
    // 查找相邻重复元素,返回相邻元素的第一个位置的迭代器
    
4.  binary_search
   **函数原型：**
- `bool binary_search(iterator beg, iterator end, value);`
  查找指定元素,查到返回true,否则false
  使用二分查找法查找,要求查找容器中元素为有序序列
5. count
   统计元素个数,count->按值统计;count_if->按条件统计
   count(iterator beg, iterator end, value);
   count_if(iterator beg, iterator end, \_Pred);
三.常用排序算法
1. sort
   sort(iterator beg, iterator end,\_Pred);
   按照_Pred所指示顺序排序,比如_Pred是以前者>后者返回true,则排序为降序排序
   可以不带_pred参数,默认为从小到大排序
2.  random_shuffle
   洗牌
   `random_shuffle(iterator beg, iterator end);`
   // 指定范围内的元素随机调整次序
3. merge
   `merge(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);`
   // 容器元素合并，并存储到另一容器中
   注意: 两个容器必须是**有序的**,合并后的容器中元素按照合并前的排序方式排序;vtarget.resize(v1.size() + v2.size());应提前分配好空间
4. reverse
   翻转容器中元素,略

四,常用拷贝替换算法
- `copy` // 容器内指定范围的元素拷贝到另一容器中
- `replace` // 将容器内指定范围的旧元素修改为新元素
- `replace_if`  // 容器内指定范围满足条件的元素替换为新元素
- `swap` // 互换两个容器的元素
1. copy
   copy(iterator beg, iterator end, iterator dest);
   将\[beg,end)区间内元素拷贝到dest容器中,同样,目标容器需提前开辟空间
2. replace
   replace(iterator beg, iterator end, oldvalue, newvalue);
   将范围内等于oldvalue(旧值)的元素替换为newvalue新值
3. replace_if
   按条件替换,replace_if(iterator beg, iterator end, \_pred, newvalue);
4. swap
   swap(container c1, container c2);
   交换c1容器和c2容器内容,两容器类型要相同

五,常用算术生成算法(#include \<numeric>)
- `accumulate` // 计算容器元素累计总和 
- `fill` // 向容器中添加元素
1. accumulate
   accumulate(iterator beg, iterator end, init);
   将beg到end区间内元素与初值init(可以是任何类型,整形,浮点型)相加,返回总和值
2. fill
   fill(iterator beg, iterator end, value);
   向beg和end区间内填充值value


六,常用集合算法
- `set_intersection` // 求两个容器的交集
    
- `set_union` // 求两个容器的并集
    
- `set_difference`  // 求两个容器的差集

1. set_intersection
   `set_intersection(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);`
   // 求两个集合的交集
   // **注意:两个集合必须是有序序列(寻找元素实用的是二分查找),返回值交集中最后一个元素位置,目标空间开辟两集合中空间的最小值即可
2. set_union
   set_union(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);
   求两结合并集,相关要求与set_intersection类似,目标空间开辟为两集合空间和
3. set_diffirence
   //求两结合差集
   set_difference(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);
   dest开辟空间为两集合较大空间
     在集合论中，差集是指从一个集合中去掉另一个集合中的所有元素后得到的新集合。如果我们有两个集合A和B，A减去B的差集表示为A - B。
     差集的定义如下：
     A - B = { x | x ∈ A 且 x ∉ B }
 