# **1. STL概论**

长久以来，软件界一直希望建立一种可重复利用的东西，以及一种得以制造出”可重复运用的东西”的方法,让程序员的心血不止于随时间的迁移，人事异动而烟消云散，从函数(functions)，类别(classes),函数库(function libraries),类别库(class libraries)、各种组件，从模块化设计，到面向对象(object oriented )，为的就是复用性的提升。

复用性必须建立在某种标准之上。但是在许多环境下，就连软件开发最基本的数据结构(data structures) 和算法(algorithm)都未能有一套标准。大量程序员被迫从事大量重复的工作，竟然是为了完成前人已经完成而自己手上并未拥有的程序代码，这不仅是人力资源的浪费，也是挫折与痛苦的来源。

为了建立数据结构和算法的一套标准，并且降低他们之间的耦合关系，以提升各自的独立性、弹性、交互操作性(相互合作性,interoperability),诞生了STL。

## **1.1 STL基本概念**

STL(Standard Template Library,标准模板库)，是惠普实验室开发的一系列软件的统 称。现在主要出现在 c++中，但是在引入 c++之前该技术已经存在很长时间了。  STL 从广义上分为: 容器(container) 算法(algorithm) 迭代器(iterator),容器和算法之间通过迭代器进行无缝连接。STL 几乎所有的代码都采用了模板类或者模板函数，这相比传统的由函数和类组成的库来说提供了更好的代码重用机会。STL(Standard Template Library)标准模板库,在我们 c++标准程序库中隶属于 STL 的占到了 80%以上。

## **1.2 STL六大组件简介**

STL提供了六大组件，彼此之间可以组合套用，这六大组件分别是:容器、算法、迭代器、仿函数、适配器（配接器）、空间配置器。

**容器：**各种数据结构，如vector、list、deque、set、map等,用来存放数据，从实现角度来看，STL容器是一种class template。

**算法：**各种常用的算法，如sort、find、copy、for_each。从实现的角度来看，STL算法是一种function tempalte.

**迭代器：**扮演了容器与算法之间的胶合剂，共有五种类型，从实现角度来看，迭代器是一种将operator* , operator-> , operator++,operator--等指针相关操作予以重载的class template. 所有STL容器都附带有自己专属的迭代器，只有容器的设计者才知道如何遍历自己的元素。原生指针(native pointer)也是一种迭代器。

**仿函数：**行为类似函数，可作为算法的某种策略。从实现角度来看，仿函数是一种重载了operator()的class 或者class template

**适配器：**一种用来修饰容器或者仿函数或迭代器接口的东西。

**空间配置器：**负责空间的配置与管理。从实现角度看，配置器是一个实现了动态空间配置、空间管理、空间释放的class tempalte.

STL六大组件的交互关系，容器通过空间配置器取得数据存储空间，算法通过迭代器存储容器中的内容，仿函数可以协助算法完成不同的策略的变化，适配器可以修饰仿函数。

## **1.3 STL优点**

- STL 是 C++的一部分，因此不用额外安装什么，它被内建在你的编译器之内。
- STL 的一个重要特性是将数据和操作分离。数据由容器类别加以管理，操作则由可定制的算法定义。迭代器在两者之间充当"粘合剂",以使算法可以和容器交互运作
- 程序员可以不用思考 STL 具体的实现过程，只要能够熟练使用 STL 就 OK 了。这样他们就可以把精力放在程序开发的别的方面。
- STL 具有高可重用性，高性能，高移植性，跨平台的优点。
  - 高可重用性：STL 中几乎所有的代码都采用了模板类和模版函数的方式实现，这相比于传统的由函数和类组成的库来说提供了更好的代码重用机会。关于模板的知\ 识，已经给大家介绍了。
  - 高性能：如 map 可以高效地从十万条记录里面查找出指定的记录，因为 map 是采用红黑树的变体实现的。
  - 高移植性：如在项目 A 上用 STL 编写的模块，可以直接移植到项目 B 上。

![2024-11-26_17-13-23.png.jpeg](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-13-23.png.jpeg)

STL之父Alex Stepanov 亚历山大·斯特潘诺夫(STL创建者)

# **2. STL三大组件**

## **2.1 容器**

容器，置物之所也。

研究数据的特定排列方式，以利于搜索或排序或其他特殊目的，这一门学科我们称为数据结构。大学信息类相关专业里面，与编程最有直接关系的学科，首推数据结构与算法。几乎可以说，任何特定的数据结构都是为了实现某种特定的算法。STL容器就是将运用最广泛的一些数据结构实现出来。

常用的数据结构：数组(array),链表(list),tree(树)，栈(stack),队列(queue),集合(set),映射表(map),根据数据在容器中的排列特性，这些数据分为**序列式容器**和**关联式容器**两种。

- 序列式容器强调值的排序，序列式容器中的每个元素均有固定的位置，除非用删除或插入的操作改变这个位置。Vector容器、Deque容器、List容器等。
- 关联式容器是非线性的树结构，更准确的说是二叉树结构。各元素之间没有严格的物理上的顺序关系，也就是说元素在容器中并没有保存元素置入容器时的逻辑顺序。关联式容器另一个显著特点是：在值中选择一个值作为关键字key，这个关键字对值起到索引的作用，方便查找。Set/multiset容器 Map/multimap容器

![2024-11-26_17-14-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-14-23.png.png)

## **2.2 算法**

算法，问题之解法也。

以有限的步骤，解决逻辑或数学上的问题，这一门学科我们叫做算法(Algorithms).

广义而言，我们所编写的每个程序都是一个算法，其中的每个函数也都是一个算法，毕竟它们都是用来解决或大或小的逻辑问题或数学问题。STL收录的算法经过了数学上的效能分析与证明，是极具复用价值的，包括常用的排序，查找等等。特定的算法往往搭配特定的数据结构，算法与数据结构相辅相成。

算法分为:**质变算法**和**非质变算法**。

- 质变算法：是指运算过程中会更改区间内的元素的内容。例如拷贝，替换，删除等等
- 非质变算法：是指运算过程中不会更改区间内的元素内容，例如查找、计数、遍历、寻找极值等等

**再好的编程技巧，也无法让一个笨拙的算法起死回生**

## **2.3 迭代器**

迭代器(iterator)是一种抽象的设计概念，现实程序语言中并没有直接对应于这个概念的实物。在<<Design Patterns>>一书中提供了23中设计模式的完整描述，其中iterator模式定义如下：提供一种方法，使之能够依序寻访某个容器所含的各个元素，而又无需暴露该容器的内部表示方式。

迭代器的设计思维-STL的关键所在，STL的中心思想在于将容器(container)和算法(algorithms)分开，彼此独立设计，最后再一贴胶着剂将他们撮合在一起。从技术角度来看，容器和算法的泛型化并不困难，c++的class template和function template可分别达到目标，如果设计出两这个之间的良好的胶着剂，才是大难题。

迭代器的种类：

| **输入迭代器** | **提供对数据的只读访问**                                     | **只读，支持++、==、！=**               |
| -------------- | ------------------------------------------------------------ | --------------------------------------- |
| 输出迭代器     | 提供对数据的只写访问                                         | 只写，支持++                            |
| 前向迭代器     | 提供读写操作，并能向前推进迭代器                             | 读写，支持++、==、！=                   |
| 双向迭代器     | 提供读写操作，并能向前和向后操作                             | 读写，支持++、--，                      |
| 随机访问迭代器 | 提供读写操作，并能以跳跃的方式访问容器的任意数据，是功能最强的迭代器 | 读写，支持++、--、[n]、-n、<、<=、>、>= |

## **2.3 案例**

```cpp
#define _CRT_SECURE_NO_WARNINGS
#include<iostream>
#include<vector>
#include<algorithm>
//cout << "n:" << n << endl;
using namespace std;

//STL 中的容器 算法 迭代器
void test01() {
    vector<int> v; //STL 中的标准容器之一 ：动态数组
    v.push_back(1); //vector 容器提供的插入数据的方法
    v.push_back(5);
    v.push_back(5);
    v.push_back(7);
    //迭代器
    vector<int>::iterator pStart = v.begin(); //vector 容器提供了 begin()方法 返回指向第一个元素的迭代器
    vector<int>::iterator pEnd = v.end(); //vector 容器提供了 end()方法 返回指向最后一个元素下一个位置的迭代器
    //通过迭代器遍历
    while (pStart != pEnd) {
        cout << *pStart << " ";
        pStart++;
    }
    cout << endl;
    vector<int>::iterator pStart1 = v.begin(); //这里要使用一个新的，旧的已经结束了（指向末尾了）
    //算法 count 算法 用于统计元素的个数
    int n = count(pStart1, pEnd, 5);
    cout << "n:" << n << endl;
}
/*1 5 5 7
n:2*/

//STL 容器不单单可以存储基础数据类型，也可以存储类对象
class Teacher {
public:
    Teacher(int age) : age(age) {};

    ~Teacher() {};
public:
    int age;
};

void test02() {
    vector<Teacher> v; //存储 Teacher 类型数据的容器
    Teacher t1(10), t2(20), t3(30);
    v.push_back(t1);
    v.push_back(t2);
    v.push_back(t3);
    vector<Teacher>::iterator pStart = v.begin();
    vector<Teacher>::iterator pEnd = v.end();
    //通过迭代器遍历
    while (pStart != pEnd) {
        cout << pStart->age << " ";
        pStart++;
    }
    cout << endl;
}
/*10 20 30*/

//存储 Teacher 类型指针
void test03() {
    vector<Teacher *> v; //存储 Teacher 类型指针
    Teacher *t1 = new Teacher(10);
    Teacher *t2 = new Teacher(20);
    Teacher *t3 = new Teacher(30);
    v.push_back(t1);
    v.push_back(t2);
    v.push_back(t3);
    //拿到容器迭代器
    vector<Teacher *>::iterator pStart = v.begin();
    vector<Teacher *>::iterator pEnd = v.end();
    //通过迭代器遍历
    while (pStart != pEnd) {
        cout << (*pStart)->age << " ";
        pStart++;
    }
    cout << endl;
}
/*10 20 30*/

//容器嵌套容器 难点(不理解，可以跳过)
void test04() {
    vector<vector<int> > v;
    vector<int> v1;
    vector<int> v2;
    vector<int> v3;

    for (int i = 0; i < 5; i++) {
        v1.push_back(i);
        v2.push_back(i * 10);
        v3.push_back(i * 100);
    }
    v.push_back(v1);
    v.push_back(v2);
    v.push_back(v3);

    for (vector<vector<int> >::iterator it = v.begin(); it != v.end(); it++) {
        for (vector<int>::iterator subIt = (*it).begin(); subIt != (*it).end(); subIt++) {
            cout << *subIt << " ";
        }
        cout << endl;
    }
}
/*0 1 2 3 4
0 10 20 30 40
0 100 200 300 400*/

int main() {
//    test01();
//    test02();
//    test03();
    test04();
    system("pause");
    return EXIT_SUCCESS;
}
```

# **3. 常用容器**

## **3.1 string容器**

### **3.1.1 string容器基本概念**

C风格字符串(以空字符（`'\0'`）结尾的字符数组)太过复杂难于掌握，不适合大程序的开发，所以C++标准库定义了一种string类，定义在头文件<string>。

String和c风格字符串对比：

- Char*是一个指针，String是一个类

string封装了char*，管理这个字符串，是一个char*型的容器。

- String封装了很多实用的成员方法

查找find，拷贝copy，删除delete 替换replace，插入insert

- 不用考虑内存释放和越界

string管理char*所分配的内存。每一次string的复制，取值都由string类负责维护，不用担心复制越界和取值越界等。

### **3.1.2 string容器常用操作**

#### **3.1.2.1 string 构造函数**

```cpp
string();//创建一个空的字符串 例如: string str;      
string(const string& str);//使用一个string对象初始化另一个string对象
string(const char* s);//使用字符串s初始化
string(int n, char c);//使用n个字符c初始化 
```

#### **3.1.2.2 string基本赋值操作**

```cpp
string& operator=(const char* s);//char*类型字符串 赋值给当前的字符串
string& operator=(const string &s);//把字符串s赋给当前的字符串
string& operator=(char c);//字符赋值给当前的字符串
string& assign(const char *s);//把字符串s赋给当前的字符串
string& assign(const char *s, int n);//把字符串s的前n个字符赋给当前的字符串
string& assign(const string &s);//把字符串s赋给当前字符串
string& assign(int n, char c);//用n个字符c赋给当前字符串
string& assign(const string &s, int start, int n);//将s从start开始n个字符赋值给字符串
```

#### **3.1.2.3 string存取字符操作**

```cpp
char& operator[](int n);//通过[]方式取字符
char& at(int n);//通过at方法获取字符
```

#### **3.1.2.4 string拼接操作**

```cpp
string& operator+=(const string& str);//重载+=操作符
string& operator+=(const char* str);//重载+=操作符
string& operator+=(const char c);//重载+=操作符
string& append(const char *s);//把字符串s连接到当前字符串结尾
string& append(const char *s, int n);//把字符串s的前n个字符连接到当前字符串结尾
string& append(const string &s);//同operator+=()
string& append(const string &s, int pos, int n);//把字符串s中从pos开始的n个字符连接到当前字符串结尾
string& append(int n, char c);//在当前字符串结尾添加n个字符c
```

#### **3.1.2.5 string查找和替换**

```cpp
int find(const string& str, int pos = 0) const; //查找str第一次出现位置,从pos开始查找
int find(const char* s, int pos = 0) const;  //查找s第一次出现位置,从pos开始查找
int find(const char* s, int pos, int n) const;  //从pos位置查找s的前n个字符第一次位置
int find(const char c, int pos = 0) const;  //查找字符c第一次出现位置
int rfind(const string& str, int pos = npos) const;//查找str最后一次位置,从pos开始查找
int rfind(const char* s, int pos = npos) const;//查找s最后一次出现位置,从pos开始查找
int rfind(const char* s, int pos, int n) const;//从pos查找s的前n个字符最后一次位置
int rfind(const char c, int pos = 0) const; //查找字符c最后一次出现位置
string& replace(int pos, int n, const string& str); //替换从pos开始n个字符为字符串str
string& replace(int pos, int n, const char* s); //替换从pos开始的n个字符为字符串s
```

#### **3.1.2.6 string比较操作**

```cpp
/*
compare函数在>时返回 1，<时返回 -1，==时返回 0。
比较区分大小写，比较时参考字典顺序，排越前面的越小。
大写的A比小写的a小。
*/
int compare(const string &s) const;//与字符串s比较
int compare(const char *s) const;//与字符串s比较
```

#### **3.1.2.7 string子串**

```cpp
string substr(int pos = 0, int n = npos) const;//返回由pos开始的n个字符组成的字符串
```

#### **3.1.2.8 string插入和删除操作**

```cpp
string& insert(int pos, const char* s); //插入字符串
string& insert(int pos, const string& str); //插入字符串
string& insert(int pos, int n, char c);//在指定位置插入n个字符c
string& erase(int pos, int n = npos);//删除从Pos开始的n个字符 
```

#### **3.1.2.9 string和c-style字符串转换**

```cpp
//string 转 char*
string str = "itcast";
const char* cstr = str.c_str();
//char* 转 string 
char* s = "itcast";
string str(s);
```

> 在 C++ 中，存在从 `const char*` 到 `std::string` 的隐式类型转换，但从 `std::string` 到 C 风格字符串（`const char*`）则需要显式调用 `c_str()` 函数。这涉及到 C++ 中不同类型字符串的处理方式，下面我将详细解释这个概念。
>
> **1. 隐式转换：从** `const char*` **到** `std::string`
>
> 在 C++ 中，`std::string` 构造函数支持从 `const char*` 类型的 C 风格字符串隐式转换。因此，像下面的代码是合法的：
>
> ```cpp
> const char* cstr = "hello";
> std::string str = cstr;  // 隐式类型转换
> ```
>
> 这里，`const char*` 类型的字符串 `"hello"` 会自动被转换为 `std::string` 类型，`std::string` 的构造函数会将这个 C 风格字符串复制到内部的字符数组中。
>
> **2. 没有从** `std::string` **到** `const char*` **的隐式转换**
>
> 虽然 `std::string` 存储的是一个字符数组，并且它本身也以 null 终止符（`\0`）结尾，但 **C++ 不允许直接从** `std::string` **到** `const char*` **的隐式转换**。这种设计主要是为了安全性和避免潜在的内存问题。
>
> 因此，`std::string` 到 `const char*` 的转换需要显式调用 `c_str()` 函数。这个函数返回指向字符串数据的 `const char*` 指针，类似于：
>
> ```cpp
> std::string str = "hello";
> const char* cstr = str.c_str();  // 显式转换
> ```
>
> **3.** `c_str()` **函数的作用**
>
> - `c_str()` 是 `std::string` 类的一个成员函数，返回一个指向 C 风格字符串的 `const char*` 指针。
> - 这个指针指向的内容是以 null 终止符结尾的，并且它代表了 `std::string` 对象内部存储的字符数据。
>
> **4. 为什么没有隐式转换？**
>
> C++ 设计者决定不提供从 `std::string` 到 `const char*` 的隐式转换，原因如下：
>
> - **安全性**：隐式转换可能会带来一些隐患，比如不小心修改了一个 `const` 字符串的内容，或者错误地将 `std::string` 对象传递给不接受 `const char*` 类型的函数。
> - **明确性**：通过显式调用 `c_str()`，程序员可以清楚地表明他们正在使用 C 风格的字符串表示方式。这种方式更加显式，避免了意外的类型转换。

为了修改string字符串的内容，下标操作符[]和at都会返回字符的引用。但当字符串的内存被重新分配之后，可能发生错误.

```cpp
int main(){
    string s = "abcdefg";
    char& a = s[2];
    char& b = s[3];

    a = '1';
    b = '2';

    cout << s << endl;
    cout << (int*)s.c_str() << endl;

    s = "pppppppppppppppppppppppp";

    a = '1';
    b = '2';

    cout << s << endl;
    cout << (int*)s.c_str() << endl;
}
/*
ab12efg
0x4794bffa50
pppppppppppppppppppppppp
0x1ecdb136ed0*/
```

## **3.2 vector容器**

### **3.2.1 vector容器基本概念**

vector的数据安排以及操作方式，与array非常相似，两者的唯一差别在于空间的运用的灵活性。Array是静态空间，一旦配置了就不能改变，要换大一点或者小一点的空间，可以，一切琐碎得由自己来，首先配置一块新的空间，然后将旧空间的数据搬往新空间，再释放原来的空间。Vector是动态空间，随着元素的加入，它的内部机制会自动扩充空间以容纳新元素。因此vector的运用对于内存的合理利用与运用的灵活性有很大的帮助，我们再也不必害怕空间不足而一开始就要求一个大块头的array了。

Vector的实现技术，关键在于其对大小的控制以及重新配置时的数据移动效率，一旦vector旧空间满了，如果客户每新增一个元素，vector内部只是扩充一个元素的空间，实为不智，因为所谓的扩充空间(不论多大)，一如刚所说，是"配置新空间-数据移动-释放旧空间"的大工程,时间成本很高，应该加入某种未雨绸缪的考虑，稍后我们便可以看到vector的空间配置策略。

![2024-11-26_17-15-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-15-23.png.png)

### **3.2.2 vector迭代器**

Vector维护一个线性空间，所以不论元素的型别（即类型）如何，普通指针都可以作为vector的迭代器，因为vector迭代器所需要的操作行为，如operaroe*, operator->, operator++, operator--, operator+, operator-, operator+=, operator-=, 普通指针天生具备。Vector支持随机存取，而普通指针正有着这样的能力。所以vector提供的是随机访问迭代器(Random Access Iterators).

根据上述描述，如果我们写如下的代码：

```
Vector<int>::iterator it1;
Vector<Teacher>::iterator it2;
```

it1的型别其实就是`Int*`,it2的型别其实就是`Teacher*`.

```cpp
#define _CRT_SECURE_NO_WARNINGS
#include<iostream>
#include<vector>
using namespace std;

int main(){

    vector<int> v;
    for (int i = 0; i < 10;i++){
        v.push_back(i);
        cout << v.capacity() << endl;  // v.capacity()容器的容量
    }
    system("pause");
    return EXIT_SUCCESS;
}
/*
1
2
4
4
8
8
8
8
16
16*/
```

### **3.2.3 vector的数据结构**

Vector所采用的数据结构非常简单，线性连续空间，它以两个迭代器_Myfirst和_Mylast分别指向配置得来的连续空间中目前已被使用的范围，并以迭代器_Myend指向整块连续内存空间的尾端。

为了降低空间配置时的速度成本，vector实际配置的大小可能比客户端需求大一些，以备将来可能的扩充，这边是**容量**的概念。换句话说，**一个vector的容量永远大于或等于其大小，一旦容量等于大小，便是满载，下次再有新增元素，整个vector容器就得另觅居所。**

**注意：**

所谓动态增加大小，并不是在原空间之后续接新空间(因为无法保证原空间之后尚有可配置的空间)，而是一块更大的内存空间，然后将原数据拷贝新空间，并释放原空间。因此，对vector的任何操作，一旦引起空间的重新配置，指向原vector的所有迭代器就都失效了。这是程序员容易犯的一个错误，务必小心。

### **3.2.4 vector常用API操作**

#### **3.2.4.1 vector构造函数**

```cpp
vector<T> v; //采用模板实现类实现，默认构造函数
vector(v.begin(), v.end());//将v[begin(), end())区间中的元素拷贝给本身。
vector(n, elem);//构造函数将n个elem拷贝给本身。
vector(const vector &vec);//拷贝构造函数。

//例子 使用第二个构造函数 我们可以...
int arr[] = {2,3,4,1,9};
vector<int> v1(arr, arr + sizeof(arr) / sizeof(int)); 
```

#### **3.2.4.2 vector常用赋值操作**

```cpp
assign(beg, end);//将[beg, end)区间中的数据拷贝赋值给本身。
assign(n, elem);//将n个elem拷贝赋值给本身。
vector& operator=(const vector  &vec);//重载等号操作符
swap(vec);// 将vec与本身的元素互换。
```

#### **3.2.4.3 vector大小操作**

```cpp
size();//返回容器中元素的个数
empty();//判断容器是否为空
resize(int num);//重新指定容器的长度为num，若容器变长，则以默认值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。
resize(int num, elem);//重新指定容器的长度为num，若容器变长，则以elem值填充新位置。如果容器变短，则末尾超出容器长>度的元素被删除。
capacity();//容器的容量
reserve(int len);//容器预留len个元素长度，预留位置不初始化，元素不可访问。
```

> 注意：capacity 并不会因为 resize 操作而改变，即它只会改变容器的大小，释放或增加元素，但不释放已经分配的内存（容量）。

#### **3.2.4.4 vector数据存取操作**

```cpp
at(int idx); //返回索引idx所指的数据，如果idx越界，抛出out_of_range异常。
operator[];//返回索引idx所指的数据，越界时，运行直接报错
front();//返回容器中第一个数据元素
back();//返回容器中最后一个数据元素
```

#### **3.2.4.5 vector插入和删除操作**

```cpp
insert(const_iterator pos, int count,ele);//迭代器指向位置pos插入count个元素ele.
push_back(ele); //尾部插入元素ele
pop_back();//删除最后一个元素
erase(const_iterator start, const_iterator end);//删除迭代器从start到end之间的元素
erase(const_iterator pos);//删除迭代器指向的元素
clear();//删除容器中所有元素
```

### **3.2.5 vector小案例**

#### **3.2.5.1巧用swap，收缩内存空间**

```cpp
int main(){

    vector<int> v;
    for (int i = 0; i < 100000;i ++){
        v.push_back(i);
    }

    cout << "capacity:" << v.capacity() << endl;
    cout << "size:" << v.size() << endl;

    //此时 通过resize改变容器大小
    v.resize(100);

    cout << "capacity:" << v.capacity() << endl;
    cout << "size:" << v.size() << endl;

    vector<int> kk(v);//调用拷贝构造函数
    v.swap(kk);
    cout << "capacity:" << v.capacity() << endl;
    cout << "capacity:" << v.size() << endl;

    vector<int>(v).swap(v);//vector<int>(v)使用了拷贝构造函数。
    cout << "capacity:" << v.capacity() << endl;
    cout << "size:" << v.size() << endl;

    system("pause");
    return EXIT_SUCCESS;
}
/*
capacity:131072
size:100000
capacity:131072
size:100
capacity:100
capacity:100
capacity:100
size:100*/
```

> 细节：
>
> - 拷贝构造函数可以将容量压缩。
> - `swap` **函数**：`swap` 是 C++ 标准库 `std::vector` 提供的一个成员函数，它用于交换两个容器的内容、大小和容量。交换操作的速度非常快，因为它只是交换了两个容器的指针（内部的动态数组指针），而不是拷贝所有元素，即只交换内部指针、大小和容量。

#### **3.2.5.2 reserve预留空间**

```cpp
#define _CRT_SECURE_NO_WARNINGS
#include<iostream>
#include<vector>
using namespace std;

int main(){

    vector<int> v;

    //预先开辟空间
    v.reserve(100000);

    int* pStart = NULL;
    int count = 0;
    for (int i = 0; i < 100000;i++){
        v.push_back(i);
        if (pStart != &v[0]){
            pStart = &v[0];
            count++;
        }//这里用来统计v的空间变换的次数
    }

    cout << "count:" << count << endl;

    system("pause");
    return EXIT_SUCCESS;
}
/*
count:1*/
```

## **3.3 deque容器**

### **3.3.1 deque容器基本概念**

Vector容器是单向开口的连续内存空间，deque则是一种双向开口的连续线性空间。所谓的双向开口，意思是可以在头尾两端分别做元素的插入和删除操作，当然，vector容器也可以在头尾两端插入元素，但是在其头部操作效率奇差，无法被接受。

![2024-11-26_17-16-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-16-23.png.png)

Deque容器和vector容器最大的差异，一在于deque允许使用常数项时间对头端进行元素的插入和删除操作。二在于deque没有容量的概念，因为它是动态的以分段连续空间组合而成，随时可以增加一段新的空间并链接起来，换句话说，像vector那样，"旧空间不足而重新配置一块更大空间，然后复制元素，再释放旧空间"这样的事情在deque身上是不会发生的。也因此，deque没有必须要提供所谓的空间保留(reserve)功能.

虽然deque容器也提供了Random Access Iterator,但是它的迭代器并不是普通的指针，其复杂度和vector不是一个量级，这当然影响各个运算的层面。因此，除非有必要，我们应该尽可能的使用vector，而不是deque。对deque进行的排序操作，为了最高效率，可将deque先完整的复制到一个vector中，对vector容器进行排序，再复制回deque.

### **3.3.2 deque容器实现原理**

Deque容器是连续的空间，至少逻辑上看来如此，连续现行空间总是令我们联想到array和vector,array无法成长，vector虽可成长，却只能向尾端成长，而且其成长其实是一个假象，事实上(1) 申请更大空间 (2)原数据复制新空间 (3)释放原空间 三步骤，如果不是vector每次配置新的空间时都留有余裕，其成长假象所带来的代价是非常昂贵的。

Deque是由一段一段的定量的连续空间构成。一旦有必要在deque前端或者尾端增加新的空间，便配置一段连续定量的空间，串接在deque的头端或者尾端。Deque最大的工作就是维护这些分段连续的内存空间的整体性的假象，并提供随机存取的接口，避开了重新配置空间，复制，释放的轮回，代价就是复杂的迭代器架构。

既然deque是分段连续内存空间，那么就必须有中央控制，维持整体连续的假象，数据结构的设计及迭代器的前进后退操作颇为繁琐。Deque代码的实现远比vector或list都多得多。

Deque采取一块所谓的map(注意，不是STL的map容器)作为主控，这里所谓的map是一小块连续的内存空间，其中每一个元素(此处成为一个结点)都是一个指针，指向另一段连续性内存空间，称作缓冲区。缓冲区才是deque的存储空间的主体。

![2024-11-26_17-17-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-17-23.png.png)

其他图示：

![2024-11-28_16-02-00.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/28/2024-11-28_16-02-00.png)

### **3.3.3 deque常用API**

#### **3.3.3.1 deque构造函数**

```cpp
deque<T> deqT;//默认构造形式
deque(beg, end);//构造函数将[beg, end)区间中的元素拷贝给本身。
deque(n, elem);//构造函数将n个elem拷贝给本身。
deque(const deque &deq);//拷贝构造函数。
```

#### **3.3.3.2 deque赋值操作**

```cpp
assign(beg, end);//将[beg, end)区间中的数据拷贝赋值给本身。
assign(n, elem);//将n个elem拷贝赋值给本身。
deque& operator=(const deque &deq); //重载等号操作符 
swap(deq);// 将deq与本身的元素互换
```

#### **3.3.3.3 deque大小操作**

```cpp
deque.size();//返回容器中元素的个数
deque.empty();//判断容器是否为空
deque.resize(num);//重新指定容器的长度为num,若容器变长，则以默认值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。
deque.resize(num, elem); //重新指定容器的长度为num,若容器变长，则以elem值填充新位置,如果容器变短，则末尾超出容器长度的元素被删除。
```

#### **3.3.3.4 deque双端插入和删除操作**

```cpp
push_back(elem);//在容器尾部添加一个数据
push_front(elem);//在容器头部插入一个数据
pop_back();//删除容器最后一个数据
pop_front();//删除容器第一个数据
```

#### **3.3.3.5 deque数据存取**

```cpp
at(idx);//返回索引idx所指的数据，如果idx越界，抛出out_of_range。
operator[];//返回索引idx所指的数据，如果idx越界，不抛出异常，直接出错。
front();//返回第一个数据。
back();//返回最后一个数据
```

#### **3.3.3.6 deque插入操作**

```cpp
insert(pos,elem);//在pos位置插入一个elem元素的拷贝，返回新数据的位置。
insert(pos,n,elem);//在pos位置插入n个elem数据，无返回值。
insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据，无返回值。
```

#### **3.3.3.7 deque删除操作**

```cpp
clear();//移除容器的所有数据
erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置。
erase(pos);//删除pos位置的数据，返回下一个数据的位置。
```

## **3.4 stack容器**

### **3.4.1 stack容器基本概念**

stack是一种先进后出(First In Last Out,FILO)的数据结构，它只有一个出口，形式如图所示。stack容器允许新增元素，移除元素，取得栈顶元素，但是除了最顶端外，没有任何其他方法可以存取stack的其他元素。换言之，stack不允许有遍历行为。

有元素推入栈的操作称为:push,将元素推出stack的操作称为pop。

![2024-11-26_17-18-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-18-23.png.png)

![2024-11-26_17-19-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-19-23.png.png)

![2024-11-26_17-20-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-20-23.png.png)

### **3.4.2 stack没有迭代器**

Stack所有元素的进出都必须符合"先进后出"的条件，只有stack顶端的元素，才有机会被外界取用。Stack不提供遍历功能，也不提供迭代器。

### **3.4.3 stack常用API**

#### **3.4.3.1 stack构造函数**

```cpp
stack<T> stkT;//stack采用模板类实现， stack对象的默认构造形式： 
stack(const stack &stk);//拷贝构造函数
```

#### **3.4.3.2 stack赋值操作**

```cpp
stack& operator=(const stack &stk);//重载等号操作符
```

#### **3.4.3.3 stack数据存取操作**

```cpp
push(elem);//向栈顶添加元素
pop();//从栈顶移除第一个元素
top();//返回栈顶元素
```

#### **3.4.3.4 stack大小操作**

```cpp
empty();//判断堆栈是否为空
size();//返回堆栈的大小
```

## **3.5 queue容器**

### **3.5.1 queue容器基本概念**

Queue是一种先进先出(First In First Out,FIFO)的数据结构，它有两个出口，queue容器允许从一端新增元素，从另一端移除元素。

![2024-11-26_17-21-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-21-23.png.png)

![2024-11-26_17-22-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-22-23.png.png)

### **3.5.2 queue没有迭代器**

Queue所有元素的进出都必须符合"先进先出"的条件，只有queue的顶端元素，才有机会被外界取用。Queue不提供遍历功能，也不提供迭代器。

### **3.5.3 queue常用API**

#### **3.5.3.1 queue构造函数**

```cpp
queue<T> queT;//queue采用模板类实现，queue对象的默认构造形式：
queue(const queue &que);//拷贝构造函数
```

#### **3.5.3.2 queue存取、插入和删除操作**

```cpp
push(elem);//往队尾添加元素
pop();//从队头移除第一个元素
back();//返回最后一个元素
front();//返回第一个元素
```

#### **3.5.3.3 queue赋值操作**

```cpp
queue& operator=(const queue &que);//重载等号操作符
```

#### **3.5.3.4 queue大小操作**

```cpp
empty();//判断队列是否为空
size();//返回队列的大小
```

## **3.6 list容器**

### **3.6.1 list容器基本概念**

链表是一种物理存储单元上非连续、非顺序的存储结构，数据元素的逻辑顺序是通过链表中的指针链接次序实现的。链表由一系列结点（链表中每一个元素称为结点）组成，结点可以在运行时动态生成。每个结点包括两个部分：一个是存储数据元素的数据域，另一个是存储下一个结点地址的指针域。

相较于vector的连续线性空间，list就显得负责许多，它的好处是每次插入或者删除一个元素，就是配置或者释放一个元素的空间。因此，list对于空间的运用有绝对的精准，一点也不浪费。而且，对于任何位置的元素插入或元素的移除，list永远是常数时间。

List和vector是两个最常被使用的容器。

List容器是一个双向链表。

![2024-11-26_17-23-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-23-23.png.png)

- 采用动态存储分配，不会造成内存浪费和溢出

- 链表执行插入和删除操作十分方便，修改指针即可，不需要移动大量元素
- 链表灵活，但是空间和时间额外耗费较大

### **3.6.2 list容器的迭代器**

List容器不能像vector一样以普通指针作为迭代器，因为其节点不能保证在同一块连续的内存空间上。List迭代器必须有能力指向list的节点，并有能力进行正确的递增、递减、取值、成员存取操作。所谓"list正确的递增，递减、取值、成员取用"是指，递增时指向下一个节点，递减时指向上一个节点，取值时取的是节点的数据值，成员取用时取的是节点的成员。

由于list是一个双向链表，迭代器必须能够具备前移、后移的能力，所以list容器提供的是Bidirectional Iterators.

List有一个重要的性质，插入操作和删除操作都不会造成原有list迭代器的失效。这在vector是不成立的，因为vector的插入操作可能造成记忆体重新配置，导致原有的迭代器全部失效，甚至List元素的删除，也只有被删除的那个元素的迭代器失效，其他迭代器不受任何影响。

### **3.6.3 list容器的数据结构**

list容器不仅是一个双向链表，而且还是一个循环的双向链表。

### **3.6.4 list常用API**

#### **3.6.4.1 list构造函数**

```cpp
list<T> lstT;//list采用采用模板类实现,对象的默认构造形式：
list(beg,end);//构造函数将[beg, end)区间中的元素拷贝给本身。
list(n,elem);//构造函数将n个elem拷贝给本身。
list(const list &lst);//拷贝构造函数。
```

#### **3.6.4.2 list数据元素插入和删除操作**

```cpp
push_back(elem);//在容器尾部加入一个元素
pop_back();//删除容器中最后一个元素
push_front(elem);//在容器开头插入一个元素
pop_front();//从容器开头移除第一个元素
insert(pos,elem);//在pos位置插elem元素的拷贝，返回新数据的位置。
insert(pos,n,elem);//在pos位置插入n个elem数据，无返回值。
insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据，无返回值。
clear();//移除容器的所有数据
erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置。
erase(pos);//删除pos位置的数据，返回下一个数据的位置。
remove(elem);//删除容器中所有与elem值匹配的元素。
```

#### **3.6.4.3 list大小操作**

```cpp
size();//返回容器中元素的个数
empty();//判断容器是否为空
resize(num);//重新指定容器的长度为num，
若容器变长，则以默认值填充新位置。
如果容器变短，则末尾超出容器长度的元素被删除。
resize(num, elem);//重新指定容器的长度为num，
若容器变长，则以elem值填充新位置。
如果容器变短，则末尾超出容器长度的元素被删除。
```

#### **3.6.4.4 list赋值操作**

```cpp
assign(beg, end);//将[beg, end)区间中的数据拷贝赋值给本身。
assign(n, elem);//将n个elem拷贝赋值给本身。
list& operator=(const list &lst);//重载等号操作符
swap(lst);//将lst与本身的元素互换。
```

#### **3.6.4.5 list数据的存取**

```cpp
front();//返回第一个元素。
back();//返回最后一个元素。
```

#### **3.6.4.6 list反转排序**

```cpp
reverse();//反转链表，比如lst包含1,3,5元素，运行此方法后，lst就包含5,3,1元素。
sort(); //list排序
```

## **3.7 set/multiset容器**

### **3.7.1 set/multiset容器基本概念**

#### **3.7.1.1 set容器基本概念**

Set的特性是。所有元素都会根据元素的键值自动被排序。Set的元素不像map那样可以同时拥有实值和键值，set的元素即是键值又是实值。Set不允许两个元素有相同的键值。

我们可以通过set的迭代器改变set元素的值吗？不行，因为set元素值就是其键值，关系到set元素的排序规则。如果任意改变set元素值，会严重破坏set组织。换句话说，set的iterator是一种const_iterator.

set拥有和list某些相同的性质，当对容器中的元素进行插入操作或者删除操作的时候，操作之前所有的迭代器，在操作完成之后依然有效，被删除的那个元素的迭代器必然是一个例外。

#### **3.7.1.2 multiset容器基本概念**

multiset特性及用法和set完全相同，唯一的差别在于它允许键值重复。set和multiset的底层实现是红黑树，红黑树为平衡二叉树的一种。

树的简单知识：

二叉树就是任何节点最多只允许有两个字节点。分别是左子结点和右子节点。

![2024-11-26_17-24-23.png.jpeg](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-24-23.png.jpeg)

**二叉树示意图**

二叉搜索树，是指二叉树中的节点按照一定的规则进行排序，使得对二叉树中元素访问更加高效。二叉搜索树的放置规则是：任何节点的元素值一定大于其左子树中的每一个节点的元素值，并且小于其右子树的值。因此从根节点一直向左走，一直到无路可走，即得到最小值，一直向右走，直至无路可走，可得到最大值。那么在搜索树中找到最大元素和最小元素是非常简单的事情。下图为二叉搜索树：

![2024-11-26_17-25-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-25-23.png.png)

上面我们介绍了二叉搜索树，那么当一个二叉搜索树的左子树和右子树不平衡的时候，那么搜索依据上图表示，搜索9所花费的时间要比搜索17所花费的时间要多，由于我们的输入或者经过我们插入或者删除操作，二叉树失去平衡，造成搜索效率降低。

所以我们有了一个平衡二叉树的概念，所谓的平衡不是指的完全平衡。

![2024-11-26_17-26-23.png.png](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/26/2024-11-26_17-26-23.png.png)

RB-tree(红黑树)为二叉树的一种。

### **3.7.2 set常用API**

#### **3.7.2.1 set构造函数**

```cpp
mulitset<T> mst; //multiset默认构造函数: 
set(const set &st);//拷贝构造函数
```

#### **3.7.2.2 set赋值操作**

```cpp
set& operator=(const set &st);//重载等号操作符
swap(st);//交换两个集合容器
```

#### **3.7.2.3 set大小操作**

```cpp
size();//返回容器中元素的数目
empty();//判断容器是否为空
```

#### **3.7.2.4 set插入和删除操作**

```cpp
insert(elem);//在容器中插入元素。
clear();//清除所有元素
erase(pos);//删除pos迭代器所指的元素，返回下一个元素的迭代器。
erase(beg, end);//删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。
erase(elem);//删除容器中值为elem的元素。
```

#### **3.7.2.5 set查找操作**

```cpp
find(key);//查找键key是否存在,若存在，返回该键的元素的迭代器；若不存在，返回set.end();
count(key);//查找键key的元素个数
lower_bound(keyElem);//返回第一个key>=keyElem元素的迭代器。
upper_bound(keyElem);//返回第一个key>keyElem元素的迭代器。
equal_range(keyElem);//返回容器中key与keyElem相等的上下限的两个迭代器。
```

**set的返回值 指定set排序规则:**

```cpp
//插入操作返回值
void test01(){
    set<int> s;
    pair<set<int>::iterator,bool> ret = s.insert(10);
    if (ret.second){
        cout << "插入成功:" << *ret.first << endl;
    }
    else{
        cout << "插入失败:" << *ret.first << endl;
    }
    ret = s.insert(10);
    if(ret.second){
        cout << "插入成功:" << *ret.first << endl;
    }
    else{
        cout << "插入失败:" << *ret.first << endl;
    }
}

struct MyCompare02{
    bool operator()(int v1,int v2){
        return v1 > v2;
    }
};//仿函数

//set从大到小
void test02(){

    srand((unsigned int)time(NULL));
    //我们发现set容器的第二个模板参数可以设置排序规则，默认规则是less<_Kty>
    set<int, MyCompare02> s;
    for (int i = 0; i < 10;i++){
        s.insert(rand() % 100);
    }

    for (set<int, MyCompare02>::iterator it = s.begin(); it != s.end(); it++){
        cout << *it << " ";
    }
    cout << endl;
}

//set容器中存放对象
class Person{
public:
    Person(string name,int age){
        this->mName = name;
        this->mAge = age;
    }
public:
    string mName;
    int mAge;
};


struct MyCompare03{
    bool operator()(const Person& p1,const Person& p2){
        return p1.mAge > p2.mAge;
    }
};

void test03(){

    set<Person, MyCompare03> s;

    Person p1("aaa", 20);
    Person p2("bbb", 30);
    Person p3("ccc", 40);
    Person p4("ddd", 50);

    s.insert(p1);
    s.insert(p2);
    s.insert(p3);
    s.insert(p4);

    for (set<Person, MyCompare03>::iterator it = s.begin(); it != s.end(); it++){
        cout << "Name:" << it->mName << " Age:" << it->mAge << endl;
    }
}
```

> 说明：
>
> **test01():**
>
> ```
> pair<set<int>::iterator, bool> ret = s.insert(10);
> ```
>
> - 使用 `insert` 方法尝试向集合 `s` 中插入整数 `10`。
> - 返回值是一个 `std::pair`：
>   - `ret.first` 是一个指向插入元素的迭代器。
>   - `ret.second` 是一个布尔值，表示插入是否成功。
>     - 如果插入成功，则为 `true`。
>     - 如果插入失败（即集合中已经存在该元素），则为 `false`。
>
> **test02():**
>
> `srand((unsigned int)time(NULL));` 的作用是为随机数生成器设置一个动态的种子值，以确保每次运行程序时生成的随机数序列不同。以下是具体解释：
>
> ------
>
> **1.** `srand` **函数**
>
> - **原型**：
>
>   ```cpp
>   void srand(unsigned int seed);
>   ```
>
> - `srand` 用于设置随机数生成器的种子值。
>
> - **随机数生成依赖种子**：
>
>   - 如果种子固定，`rand()` 函数生成的随机数序列也是固定的。
>   - 如果种子变化，`rand()` 函数生成的随机数序列也会变化。
>
> ------
>
> **2.** `time(NULL)`
>
> - `time` **函数原型**：
>
>   ```cpp
>   time_t time(time_t *timer);
>   ```
>
> - **返回值**：
>   返回从**1970年1月1日0时0分0秒**（Unix 时间起点）到当前时间的秒数。
>
> - `time(NULL)`：
>   表示不需要存储返回值，直接获取当前时间对应的秒数。
>
> ------
>
> **3.** `(unsigned int)` **类型转换**
>
> - `time(NULL)` 的返回值类型是 `time_t`，具体实现可能是 `long` 或 `unsigned long`。
> - 为确保类型与 `srand` 的参数一致，将其显式转换为 `unsigned int`。
>
> ------
>
> **4. 作用总结** 将当前时间的秒数作为种子值传递给 `srand`，使得 `rand()` 生成的随机数序列基于当前时间变化。这样，程序每次运行时，随机数序列不同。
>
> ------
>
> **例子**
>
> ```cpp
> #include <iostream>
> #include <cstdlib>
> #include <ctime>
> 
> int main() {
>     srand((unsigned int)time(NULL)); // 设置种子值
> 
>     for (int i = 0; i < 5; i++) {
>         std::cout << rand() % 100 << " "; // 生成 0-99 的随机数
>     }
>     return 0;
> }
> ```
>
> **输出示例**（每次运行可能不同）：
>
> ```
> 42 87 56 73 19
> ```
>
> **固定种子情况下**： 如果改为 `srand(100);`，则每次运行都会生成相同的随机数序列。
>
> 如果写成 `srand(100);`，会固定种子值为 `100`，使得程序每次运行时，`rand()` 函数生成的随机数序列完全一致。这是因为随机数生成器的行为完全由种子值决定。
>
> **示例代码**
>
> ```cpp
> #include <iostream>
> #include <cstdlib>
> 
> int main() {
>     srand(100); // 固定种子值为 100
> 
>     for (int i = 0; i < 5; i++) {
>         std::cout << rand() % 100 << " "; // 生成 0-99 的随机数
>     }
>     return 0;
> }
> ```
>
> **多次运行输出结果**：
>
> ```cpp
> 72 69 57 11 2
> ```
>
> 不论运行多少次，或者在哪台计算机上运行，只要种子值固定为 `100`，输出的随机数序列始终相同。这样可以在调试或验证程序时重现同样的随机数结果。
>
> **注意rand() 的使用：**
>
> 1. **伪随机性**：
>    `rand()` 生成的是伪随机数，序列由一个种子值（默认为 `1`）决定。这里说明`rand()` 可以不搭配`srand()`直接使用，但种子默认为1。
> 2. **可预测性**：
>    如果程序多次运行且种子值不变，`rand()` 会生成相同的随机序列。
> 3. **种子控制**：
>    可以使用 `srand()` 设置种子值，改变随机数序列。

### **3.7.3 对组(pair)**

对组(pair)将一对值组合成一个值，这一对值可以具有不同的数据类型，两个值可以分别用pair的两个公有属性first和second访问。

类模板：template <class T1, class T2> struct pair.

如何创建对组?

```cpp
//第一种方法创建一个对组
    pair<string, int> pair1(string("name"), 20);//这里string("name")直接写成"name"效果相同。
    cout << pair1.first << endl; //访问pair第一个值
    cout << pair1.second << endl;//访问pair第二个值
//第二种
    pair<string, int> pair2 = make_pair("name", 30);
    cout << pair2.first << endl;
    cout << pair2.second << endl;
//pair=赋值
    pair<string, int> pair3 = pair2;
    cout << pair3.first << endl;
    cout << pair3.second << endl;
```

## **3.8 map/multimap容器**

### **3.8.1 map/multimap基本概念**

Map的特性是，所有元素都会根据元素的键值自动排序。Map所有的元素都是pair,同时拥有实值和键值，pair的第一元素被视为键值，第二元素被视为实值，map不允许两个元素有相同的键值。

我们可以通过map的迭代器改变map的键值吗？答案是不行，因为map的键值关系到map元素的排列规则，任意改变map键值将会严重破坏map组织。如果想要修改元素的实值，那么是可以的。

Map和list拥有相同的某些性质，当对它的容器元素进行新增操作或者删除操作时，操作之前的所有迭代器，在操作完成之后依然有效，当然被删除的那个元素的迭代器必然是个例外。

Multimap和map的操作类似，唯一区别multimap键值可重复。

Map和multimap都是以红黑树为底层实现机制。

### **3.8.2 map/multimap常用API**

#### **3.8.2.1 map构造函数**

```cpp
map<T1, T2> mapTT;//map默认构造函数: 
map(const map &mp);//拷贝构造函数
```

#### **3.8.2.2 map赋值操作**

```cpp
map& operator=(const map &mp);//重载等号操作符
swap(mp);//交换两个集合容器
```

#### **3.8.2.3 map大小操作**

```cpp
size();//返回容器中元素的数目
empty();//判断容器是否为空
```

#### **3.8.2.4 map插入数据元素操作**

```cpp
map.insert(...); //往容器插入元素，返回pair<iterator,bool>
map<int, string> mapStu;
// 第一种 通过pair的方式插入对象
mapStu.insert(pair<int, string>(3, "小张"));
// 第二种 通过pair的方式插入对象
mapStu.inset(make_pair(-1, "校长"));
// 第三种 通过value_type的方式插入对象
mapStu.insert(map<int, string>::value_type(1, "小李"));
// 第四种 通过数组的方式插入值
mapStu[3] = "小刘";
mapStu[5] = "小王";
```

#### **3.8.2.5 map删除操作**

```cpp
clear();//删除所有元素
erase(pos);//删除pos迭代器所指的元素，返回下一个元素的迭代器。
erase(beg,end);//删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。
erase(keyElem);//删除容器中key为keyElem的对组。
```

#### **3.8.2.6 map查找操作**

```cpp
find(key);//查找键key是否存在,若存在，返回该键的元素的迭代器；/若不存在，返回map.end();
count(keyElem);//返回容器中key为keyElem的对组个数。对map来说，要么是0，要么是1。对multimap来说，值可能大于1。
lower_bound(keyElem);//返回第一个key>=keyElem元素的迭代器。
upper_bound(keyElem);//返回第一个key>keyElem元素的迭代器。
equal_range(keyElem);//返回容器中key与keyElem相等的上下限的两个迭代器。
```

## **3.9 STL容器使用时机**

| **容器类型** | **内存结构**              | **可随机存取** | **元素搜寻速度**     | **插入/删除位置及效率**                                      | **适用场景**                                         |
| :----------- | :------------------------ | :------------- | :------------------- | :----------------------------------------------------------- | :--------------------------------------------------- |
| `vector`     | 单端数组                  | 是，`O(1)`     | 线性搜索，`O(n)`     | - **头部**：慢，`O(n)` - **尾部**：快，摊销`O(1)` - **中间**：`O(n)` | 动态数组，适合需要频繁随机访问或尾部插入删除的场景   |
| `deque`      | 双端数组                  | 是，接近`O(1)` | 线性搜索，`O(n)`     | - **头尾**：快，`O(1)` - **中间**：`O(n)`                    | 双端队列，适合需要频繁头尾操作的场景                 |
| `list`       | 双向链表，分散存储        | 否，不支持     | 线性搜索，`O(n)`     | - **任意位置**：快，`O(1)`，需要迭代器定位                   | 双向链表，适合频繁插入删除，但随机访问需求较低的场景 |
| `set`        | 红黑树（有序）            | 否，不支持     | 快速查找，`O(log n)` | - **任意位置**：`O(log n)`                                   | 有序集合，适合需要快速查找、不允许重复元素的场景     |
| `multiset`   | 红黑树（有序）            | 否，不支持     | 快速查找，`O(log n)` | - **任意位置**：`O(log n)`                                   | 有序集合，适合需要快速查找、允许重复元素的场景       |
| `map`        | 红黑树（有序）            | 否，不支持     | 快速查找，`O(log n)` | - **任意位置**：`O(log n)`                                   | 键值对存储，适合需要快速查找键值对、按键排序的场景   |
| `multimap`   | 红黑树（有序）            | 否，不支持     | 快速查找，`O(log n)` | - **任意位置**：`O(log n)`                                   | 键值对存储，适合需要快速查找、允许重复键值对的场景   |
| `stack`      | 基于`deque`或`vector`实现 | 否，仅访问顶部 | 不适用               | - **顶部操作**：快，`O(1)`                                   | 栈，适合后进先出（LIFO）操作                         |
| `queue`      | 基于`deque`实现           | 否，仅访问头尾 | 不适用               | - **头尾操作**：快，`O(1)`                                   | 队列，适合先进先出（FIFO）操作                       |

- vector的使用场景：比如软件历史操作记录的存储，我们经常要查看历史记录，比如上一次的记录，上上次的记录，但却不会去删除记录，因为记录是事实的描述。
- deque的使用场景：比如排队购票系统，对排队者的存储可以采用deque，支持头端的快速移除，尾端的快速添加。如果采用vector，则头端移除时，会移动大量的数据，速度慢。

vector与deque的比较：

一：vector.at()比deque.at()效率高，比如vector.at(0)是固定的，deque的开始位置却是不固定的。（deque 的首元素可能位于任意块中的任意位置，查找需要先定位块，再定位块内的具体位置）

二：如果有大量释放操作的话，vector花的时间更少，这跟二者的内部实现有关。

三：deque支持头部的快速插入与快速移除，这是deque的优点。

- list的使用场景：比如公交车乘客的存储，随时可能有乘客下车，支持频繁的不确实位置元素的移除插入。
- set的使用场景：比如对手机游戏的个人得分记录的存储，存储要求从高分到低分的顺序排列。 
- map的使用场景：比如按ID号存储十万个用户，想要快速要通过ID查找对应的用户。二叉树的查找效率，这时就体现出来了。如果是vector容器，最坏的情况下可能要遍历完整个容器才能找到该用户。

# **4. 常用算法**

## **4.1 函数对象**

重载函数调用操作符的类，其对象常称为函数对象（function object），即它们是行为类似函数的对象，也叫仿函数(functor),其实就是重载“()”操作符，使得类对象可以像函数那样调用。

注意:

1. 函数对象(仿函数)是一个类，不是一个函数。
2. 函数对象(仿函数)重载了”() ”操作符使得它可以像函数一样调用。

分类:假定某个类有一个重载的operator()，而且重载的operator()要求获取一个参数，我们就将这个类称为“一元仿函数”（unary functor）；相反，如果重载的operator()要求获取两个参数，就将这个类称为“二元仿函数”（binary functor）。

函数对象的作用主要是什么？STL提供的算法往往都有两个版本，其中一个版本表现出最常用的某种运算，另一版本则允许用户通过template参数的形式来指定所要采取的策略。

```cpp
//函数对象是重载了函数调用符号的类
class MyPrint
{
public:
    MyPrint()
    {
        m_Num = 0;
    }
    int m_Num;

public:
    void operator() (int num)
    {
        cout << num << endl;
        m_Num++;
    }
};

//函数对象
//重载了()操作符的类实例化的对象，可以像普通函数那样调用,可以有参数 ，可以有返回值
void test01()
{
    MyPrint myPrint;
    myPrint(20);

}
// 函数对象超出了普通函数的概念，可以保存函数的调用状态
void test02()
{
    MyPrint myPrint;
    myPrint(20);
    myPrint(20);
    myPrint(20);
    cout << myPrint.m_Num << endl;
}

void doBusiness(MyPrint print,int num)
{
    print(num);
}

//函数对象作为参数
void test03()
{
    //参数1：匿名函数对象
    doBusiness(MyPrint(),30);
}
```

总结：

1、函数对象通常不定义构造函数和析构函数，所以在构造和析构时不会发生任何问题，避免了函数调用的运行时问题。

2、函数对象超出普通函数的概念，函数对象可以有自己的状态

3、函数对象可内联编译，性能好。用函数指针几乎不可能

4、模版函数对象使函数对象具有通用性，这也是它的优势之一

> 函数对象可内联编译，性能好。用函数指针几乎不可能->解析：
>
> - 函数对象可内联的关键在于其静态多态特性，使得目标函数在编译期确定。
> - 函数指针因动态特性无法在编译期确定目标函数，通常不能被内联优化。
> - 在追求性能的场景中，优先选择函数对象或模板，而非函数指针。

## **4.2 谓词**

谓词是指普通函数或重载的operator()返回值是bool类型的函数对象(仿函数)。如果operator接受一个参数，那么叫做一元谓词,如果接受两个参数，那么叫做二元谓词，谓词可作为一个判断式。

```cpp
class GreaterThenFive
{
public:
    bool operator()(int num)
    {
        return num > 5;
    }

};
//一元谓词
void test01()
{
    vector<int> v;
    for (int i = 0; i < 10;i ++)
    {
        v.push_back(i);
    }

    vector<int>::iterator it =  find_if(v.begin(), v.end(), GreaterThenFive());
    if (it == v.end())
    {
        cout << "没有找到" << endl;
    }
    else
    {
        cout << "找到了: " << *it << endl;
    }
}

//二元谓词
class MyCompare
{
public:
    bool operator()(int num1, int num2)
    {
        return num1 > num2;
    }

};

void test02()
{
    vector<int> v;
    v.push_back(10);
    v.push_back(40);
    v.push_back(20);
    v.push_back(90);
    v.push_back(60);

    //默认从小到大
    sort(v.begin(), v.end());
    for (vector<int>::iterator it = v.begin(); it != v.end();it++)
    {
        cout << *it << " ";
    }
    cout << endl;
    cout << "----------------------------" << endl;
    //使用函数对象改变算法策略，排序从大到小
    sort(v.begin(), v.end(),MyCompare());
    for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;
}
```

## **4.3 内建函数对象**

STL内建了一些函数对象。分为:算数类函数对象,关系运算类函数对象，逻辑运算类仿函数。这些仿函数所产生的对象，用法和一般函数完全相同，当然我们还可以产生无名的临时对象来履行函数功能。使用内建函数对象，需要引入头文件` #include<functional>`。

- 6个算数类函数对象,除了negate是一元运算，其他都是二元运算。

```cpp
template<class T> T plus<T>//加法仿函数
template<class T> T minus<T>//减法仿函数
template<class T> T multiplies<T>//乘法仿函数
template<class T> T divides<T>//除法仿函数
template<class T> T modulus<T>//取模仿函数
template<class T> T negate<T>//取反仿函数
```

- 6个关系运算类函数对象,每一种都是二元运算。

```cpp
template<class T> bool equal_to<T>//等于
template<class T> bool not_equal_to<T>//不等于
template<class T> bool greater<T>//大于
template<class T> bool greater_equal<T>//大于等于
template<class T> bool less<T>//小于
template<class T> bool less_equal<T>//小于等于
```

- 逻辑运算类运算函数,not为一元运算，其余为二元运算。

```cpp
template<class T> bool logical_and<T>//逻辑与
template<class T> bool logical_or<T>//逻辑或
template<class T> bool logical_not<T>//逻辑非
```

内建函数对象举例：

```cpp
//取反仿函数
void test01()
{
    negate<int> n;
    cout << n(50) << endl;
}

//加法仿函数
void test02()
{
    plus<int> p;
    cout << p(10, 20) << endl;
}

//大于仿函数
void test03()
{
    vector<int> v;
    srand((unsigned int)time(NULL));
    for (int i = 0; i < 10; i++){
        v.push_back(rand() % 100);
    }

    for (vector<int>::iterator it = v.begin(); it != v.end(); it++){
        cout << *it << " ";
    }
    cout << endl;
    sort(v.begin(), v.end(), greater<int>());

    for (vector<int>::iterator it = v.begin(); it != v.end(); it++){
        cout << *it << " ";
    }
    cout << endl;

}
```

## **4.4 函数对象适配器**

如果我们想使用绑定适配器,需要我们自己的函数对象继承binary_function 或者 unary_function

- unary_function表示一个一元函数对象，即接受单个参数的函数。
- binary_function表示一个二元函数对象，即接受两个参数的函数。

`bind1st` 和 `bind2nd` 是 C++ 中的函数适配器，用于对二元函数对象的某一个参数进行绑定，使其转换为一元函数对象。

- `bind1st`：绑定第一个参数。
- `bind2nd`：绑定第二个参数。

示例：

```cpp
class MyPrint :public binary_function<int,int,void>
{
public:
    void operator()(int v1,int v2) const
    {
        cout << "v1 = : " << v1 << " v2 = :" <<v2  << " v1+v2 = :" << (v1 + v2) << endl;
    }
};
//1、函数适配器
void test01()
{
    vector<int>v;
    for (int i = 0; i < 10; i++)
    {
        v.push_back(i);
    }
    cout << "请输入起始值：" << endl;
    int x;
    cin >> x;
    for_each(v.begin(), v.end(), bind1st(MyPrint(), x));
    for_each(v.begin(), v.end(), bind2nd( MyPrint(),x ));
}
/*请输入起始值：
10
v1 = : 10 v2 = :0 v1+v2 = :10
v1 = : 10 v2 = :1 v1+v2 = :11
v1 = : 10 v2 = :2 v1+v2 = :12
v1 = : 10 v2 = :3 v1+v2 = :13
v1 = : 10 v2 = :4 v1+v2 = :14
v1 = : 10 v2 = :5 v1+v2 = :15
v1 = : 10 v2 = :6 v1+v2 = :16
v1 = : 10 v2 = :7 v1+v2 = :17
v1 = : 10 v2 = :8 v1+v2 = :18
v1 = : 10 v2 = :9 v1+v2 = :19
v1 = : 0 v2 = :10 v1+v2 = :10
v1 = : 1 v2 = :10 v1+v2 = :11
v1 = : 2 v2 = :10 v1+v2 = :12
v1 = : 3 v2 = :10 v1+v2 = :13
v1 = : 4 v2 = :10 v1+v2 = :14
v1 = : 5 v2 = :10 v1+v2 = :15
v1 = : 6 v2 = :10 v1+v2 = :16
v1 = : 7 v2 = :10 v1+v2 = :17
v1 = : 8 v2 = :10 v1+v2 = :18
v1 = : 9 v2 = :10 v1+v2 = :19*/
//总结：  bind1st和bind2nd区别?
//bind1st ： 将参数绑定为函数对象的第一个参数
//bind2nd ： 将参数绑定为函数对象的第二个参数
//bind1st bind2nd将二元函数对象转为一元函数对象
```

`not1 `对一元函数对象取反，`not2` 对二元函数对象取反

示例：

```cpp
class GreaterThenFive:public unary_function<int,bool>
{
public:
    bool operator ()(int v) const
    {
        return v > 5;
    }
};

//2、取反适配器
void test02()
{
    vector <int> v;
    for (int i = 0; i < 10;i++)
    {
        v.push_back(i);
    }

// 	vector<int>::iterator it =  find_if(v.begin(), v.end(), GreaterThenFive()); //返回第一个大于5的迭代器
//	vector<int>::iterator it = find_if(v.begin(), v.end(),  not1(GreaterThenFive())); //返回第一个小于5迭代器
    //自定义输入
    vector<int>::iterator it = find_if(v.begin(), v.end(), not1 ( bind2nd(greater<int>(),5)));
    if (it == v.end())
    {
        cout << "没找到" << endl;
    }
    else
    {
        cout << "找到" << *it << endl;

    }

    //排序  二元函数对象
    sort(v.begin(), v.end(), not2(less<int>()));
    for_each(v.begin(), v.end(), [](int val){cout << val << " "; });

}
/*找到0
9 8 7 6 5 4 3 2 1 0*/
//not1 对一元函数对象取反
//not2 对二元函数对象取反
```

> `[](int val) { std::cout << val << " "; }` 使用了 C++11 引入的 Lambda 表达式，下面是对其的解释：
>
> - `[]`：表示这是一个 Lambda 表达式。
> - `(int val)`：Lambda 的参数列表，表示接收一个 `int` 类型的参数。
> - `{ std::cout << val << " "; }`：Lambda 的函数体，表示对每个传入的参数执行 `std::cout` 操作，将值打印到控制台，并在每个值后加一个空格。
>
> 这段 Lambda 表达式的作用是将输入的每个整数打印出来。

`std::ptr_fun` 是 C++ 标准库中的一个函数适配器（位于头文件 `<functional>` 中），主要用于将普通的函数指针适配为函数对象，以便可以与泛型算法（如 `std::for_each`、`std::transform` 等）一起使用。

示例：

```cpp
void MyPrint03(int v,int v2)
{
    cout << v + v2<< " ";
}

//3、函数指针适配器   ptr_fun
void test03()
{
    vector <int> v;
    for (int i = 0; i < 10; i++)
    {
        v.push_back(i);
    }
    // ptr_fun( )把一个普通的函数指针适配成函数对象
    for_each(v.begin(), v.end(), bind2nd( ptr_fun( MyPrint03 ), 100));
}
/*
100 101 102 103 104 105 106 107 108 109
*/
```

`std::mem_fun` 和 `std::mem_fun_ref` 是 C++ 标准库中的函数适配器，用于将成员函数指针转换为可调用的函数对象，使其能够与泛型算法（如 `std::for_each`）配合使用。

- `std::mem_fun` : 适用于指针类型的容器。

- `std::mem_fun_ref` : 适用于对象类型的容器。

- **区别**

  | 特性         | `std::mem_fun`                 | `std::mem_fun_ref`            |
  | ------------ | ------------------------------ | ----------------------------- |
  | **容器类型** | 容器存储的是指针 (`T*`)        | 容器存储的是对象 (`T`)        |
  | **调用形式** | 使用指针调用成员函数           | 使用对象调用成员函数          |
  | **适配对象** | 指针类型，如 `std::vector<T*>` | 对象类型，如 `std::vector<T>` |

示例：

```cpp
//4、成员函数适配器
class Person
{
public:
    Person(string name, int age)
    {
        m_Name = name;
        m_Age = age;
    }

    //打印函数
    void ShowPerson(){
        cout << "成员函数:" << "Name:" << m_Name << " Age:" << m_Age << endl;
    }
    void Plus100()
    {
        m_Age += 100;
    }
public:
    string m_Name;
    int m_Age;
};

void MyPrint04(Person &p)
{
    cout << "姓名：" <<  p.m_Name << " 年龄：" << p.m_Age << endl;

};

void test04()
{
    vector <Person>v;
    Person p1("aaa", 10);
    Person p2("bbb", 20);
    Person p3("ccc", 30);
    Person p4("ddd", 40);
    v.push_back(p1);
    v.push_back(p2);
    v.push_back(p3);
    v.push_back(p4);

    for_each(v.begin(), v.end(), MyPrint04);
    //利用 mem_fun_ref 将Person内部成员函数适配
    for_each(v.begin(), v.end(), mem_fun_ref(&Person::ShowPerson));
 	for_each(v.begin(), v.end(), mem_fun_ref(&Person::Plus100));
 	for_each(v.begin(), v.end(), mem_fun_ref(&Person::ShowPerson));
}
/*姓名：aaa 年龄：10
姓名：bbb 年龄：20
姓名：ccc 年龄：30
姓名：ddd 年龄：40
成员函数:Name:aaa Age:10
成员函数:Name:bbb Age:20
成员函数:Name:ccc Age:30
成员函数:Name:ddd Age:40
成员函数:Name:aaa Age:110
成员函数:Name:bbb Age:120
成员函数:Name:ccc Age:130
成员函数:Name:ddd Age:140*/

void test05(){

    vector<Person*> v1;
    //创建数据
    Person p1("aaa", 10);
    Person p2("bbb", 20);
    Person p3("ccc", 30);
    Person p4("ddd", 40);

    v1.push_back(&p1);
    v1.push_back(&p2);
    v1.push_back(&p3);
    v1.push_back(&p4);

    for_each(v1.begin(), v1.end(), mem_fun(&Person::ShowPerson));
}
/*成员函数:Name:aaa Age:10
成员函数:Name:bbb Age:20
成员函数:Name:ccc Age:30
成员函数:Name:ddd Age:40*/
//如果容器存放的是对象指针，  那么用mem_fun
//如果容器中存放的是对象实体，那么用mem_fun_ref
```

> `vector<Person>`和`vector<Person*>` 的区别：
>
> **1. 存储内容**
>
> **第一种：**`std::vector<Person>`
>
> - 容器 `v` 存储的是 `Person` 类型的**对象副本**。
> - 在 `push_back` 时，`Person` 对象会被拷贝到 `vector` 中。
>
> **第二种：**`std::vector<Person*>`
>
> - 容器 `v1` 存储的是指向 `Person` 类型的**指针**。
> - 在 `push_back` 时，仅存储对象的地址，而不会拷贝对象本身。
>
> ------
>
> **2. 内存管理**
>
> **第一种：**`std::vector<Person>`
>
> - `vector` 自行管理存储的对象的生命周期。
> - 当 `vector` 被销毁时，内部对象会自动调用析构函数。
>
> **第二种：**`std::vector<Person*>`
>
> - `vector` 不管理指针指向对象的生命周期。
> - 如果 `Person` 的对象是局部变量，则在离开作用域后被释放，`vector` 中的指针可能变成**悬空指针**。
> - 需要开发者手动管理 `Person` 对象的内存（例如使用 `new` 动态分配内存并确保释放）。
>
> ------
>
> **3. 访问方式**
>
> **第一种：**`std::vector<Person>` 访问容器元素时，直接得到 `Person` 对象的副本或引用：
>
> ```cpp
> for (const Person& person : v) {
>     std::cout << person.name << " " << person.age << std::endl;
> }
> ```
>
> **第二种：**`std::vector<Person*>` 访问容器元素时，需要通过指针解引用操作：
>
> ```cpp
> for (const Person* person : v1) {
>     std::cout << person->name << " " << person->age << std::endl;
> }
> ```
>
> ------
>
> **4. 性能差异**
>
> **第一种：**`std::vector<Person>`
>
> - 每次 `push_back` 时，都会拷贝 `Person` 对象（可能涉及拷贝构造函数）。
> - 如果 `Person` 类的成员较多或有复杂的动态分配，拷贝会有一定的开销。
>
> **第二种：**`std::vector<Person*>`
>
> - 存储的是指针，`push_back` 时只拷贝指针本身（通常是 8 字节），效率更高。
> - 但是，由于对象实际存储在其他地方，访问时可能会有一定的间接寻址开销。
>
> ------
>
> **5. 注意事项**
>
> **第一种：**`std::vector<Person>`
>
> - **优点**：简单安全，不需要手动管理内存。
> - **缺点**：拷贝可能导致性能开销较大，特别是对于复杂对象。
>
> **第二种：**`std::vector<Person*>`
>
> - **优点**：避免了对象的拷贝，提高了性能。
> - **缺点**：
>   - 内存管理复杂，容易产生内存泄漏或悬空指针。
>   - 需要特别注意指针指向对象的生命周期。

## **4.5 算法概述**

算法主要是由头文件<algorithm> <functional> <numeric>组成。

<algorithm>是所有STL头文件中最大的一个,其中常用的功能涉及到比较，交换，查找,遍历，复制，修改，反转，排序，合并等...

<numeric>体积很小，只包括在几个序列容器上进行的简单运算的模板函数.

<functional> 定义了一些模板类,用以声明函数对象。

## **4.6 常用遍历算法**

```cpp
/*
    遍历算法 遍历容器元素
	@param beg 开始迭代器
	@param end 结束迭代器
	@param _callback  函数回调或者函数对象
	@return 函数对象
*/
for_each(iterator beg, iterator end, _callback);
/*
	transform算法 将指定容器区间元素搬运到另一容器中
	注意 : transform 不会给目标容器分配内存，所以需要我们提前分配好内存
	@param beg1 源容器开始迭代器
	@param end1 源容器结束迭代器
	@param beg2 目标容器开始迭代器
	@param _cakkback 回调函数或者函数对象
	@return 返回目标容器迭代器
*/
transform(iterator beg1, iterator end1, iterator beg2, _callbakc)
```

for_each:

源码：

```cpp
 template<typename _InputIterator, typename _Function>
    _GLIBCXX20_CONSTEXPR
    _Function for_each(_InputIterator __first, _InputIterator __last, _Function __f)
    {
      // concept requirements
      __glibcxx_function_requires(_InputIteratorConcept<_InputIterator>)
      __glibcxx_requires_valid_range(__first, __last);
      for (; __first != __last; ++__first)
	      __f(*__first);
      return __f; // N.B. [alg.foreach] says std::move(f) but it's redundant.
    }
```

> **1. 函数模板声明**
>
> ```cpp
> template<typename _InputIterator, typename _Function>
> _GLIBCXX20_CONSTEXPR
> _Function for_each(_InputIterator __first, _InputIterator __last, _Function __f)
> ```
>
> - `template<typename _InputIterator, typename _Function>`
>   - 声明这是一个函数模板，其中有两个模板参数：
>     - `_InputIterator`：一个输入迭代器类型。
>     - `_Function`：一个函数对象类型，表示对容器元素进行操作的函数或仿函数。
> - `_GLIBCXX20_CONSTEXPR`
>   - 一个宏，表示该函数可以在编译时求值（如果满足 constexpr 的条件）。它确保在 C++20 中符合 constexpr 的约束。
> - **返回值类型为** `_Function`
>   - 该函数返回传入的 `_Function` 对象。
>
> ```cpp
> __glibcxx_function_requires(_InputIteratorConcept<_InputIterator>)
> __glibcxx_requires_valid_range(__first, __last);
> ```
>
> - `__glibcxx_function_requires(_InputIteratorConcept<_InputIterator>)`
>   - 检查 `_InputIterator` 类型是否满足输入迭代器的概念要求。例如，它必须支持解引用操作（`*`）、递增操作（`++`），并能与结束迭代器比较。
>   - 这是一个在 GCC 标准库实现中常见的宏，用于概念验证或类型约束。
> - `__glibcxx_requires_valid_range(__first, __last)`
>   - 检查 `[__first, __last)` 是否是一个有效范围：
>     - `__first` 和 `__last` 必须来自同一个容器。
>     - `__first` 必须在逻辑上出现在 `__last` 前面或相等。

示例：

```cpp
//普通函数
void print01(int val){
    cout << val << " ";
}
//函数对象
struct print001{
    void operator()(int val){
        cout << val << " ";
    }
};

//for_each算法基本用法
void test01(){

    vector<int> v;
    for (int i = 0; i < 10;i++){
        v.push_back(i);
    }

    //遍历算法
    for_each(v.begin(), v.end(), print01);
    cout << endl;

    for_each(v.begin(), v.end(), print001());
    cout << endl;

}

struct print02{
    print02(){
        mCount = 0;
    }
    void operator()(int val){
        cout << val << " ";
        mCount++;
    }
    int mCount;
};

//for_each返回值
void test02(){
       vector<int> v;
    for (int i = 0; i < 10; i++){
        v.push_back(i);
    }

    print02 p = for_each(v.begin(), v.end(), print02());//这里只需要使用一个括号。
    cout << endl;
    cout << p.mCount << endl;
}

struct print03 : public binary_function<int, int, void>{
    void operator()(int val,int bindParam) const{
        cout << val + bindParam << " ";
    }
};

//for_each绑定参数输出
void test03(){

    vector<int> v;
    for (int i = 0; i < 10; i++){
        v.push_back(i);
    }

    for_each(v.begin(), v.end(), bind2nd(print03(),100));
}
int main(){
    test01();
    test02();
    test03();
    system("pause");
    return EXIT_SUCCESS;
}
/*
0 1 2 3 4 5 6 7 8 9
0 1 2 3 4 5 6 7 8 9
0 1 2 3 4 5 6 7 8 9
10
100 101 102 103 104 105 106 107 108 109*/
```

transform:

源码：

```cpp
template<typename _InputIterator, typename _OutputIterator, typename _UnaryOperation>
    _GLIBCXX20_CONSTEXPR
    _OutputIterator transform(_InputIterator __first, _InputIterator __last,_OutputIterator __result, _UnaryOperation __unary_op)
    {
      __glibcxx_function_requires(_InputIteratorConcept<_InputIterator>)
      __glibcxx_function_requires(_OutputIteratorConcept<_OutputIterator,__typeof__(__unary_op(*__first))>)
      __glibcxx_requires_valid_range(__first, __last);
      for (; __first != __last; ++__first, (void)++__result)
	      *__result = __unary_op(*__first);
      return __result;
    }
```

> **1. 函数模板声明**
>
> ```cpp
> template<typename _InputIterator, typename _OutputIterator,typename _UnaryOperation>
> _GLIBCXX20_CONSTEXPR
> _OutputIterator transform(_InputIterator __first, _InputIterator __last,_OutputIterator __result, _UnaryOperation __unary_op)
> ```
>
> - **模板参数：**
>   - `_InputIterator`：输入迭代器的类型，用于遍历输入范围。
>   - `_OutputIterator`：输出迭代器的类型，用于存储结果。
>   - `_UnaryOperation`：一元操作的函数或仿函数，用于对输入范围的每个元素进行处理。
> - `_GLIBCXX20_CONSTEXPR`
>   - 表示该函数可以在编译时执行（在满足 constexpr 要求的情况下）。
> - **返回值类型为** `_OutputIterator`
>   - 返回经过处理后指向结果范围末尾的输出迭代器。
>
> ------
>
> ### **2. 函数体**
>
> #### **(1) 概念和约束**
>
> ```cpp
> __glibcxx_function_requires(_InputIteratorConcept<_InputIterator>)
> __glibcxx_function_requires(_OutputIteratorConcept<_OutputIterator,__typeof__(__unary_op(*__first))>)
> __glibcxx_requires_valid_range(__first, __last);
> ```
>
> - **输入迭代器约束：**
>   `__glibcxx_function_requires(_InputIteratorConcept<_InputIterator>)`
>   确保 `_InputIterator` 满足输入迭代器的概念要求。例如，支持解引用操作（`*`）和递增操作（`++`）。
> - **输出迭代器约束：**
>   `__glibcxx_function_requires(_OutputIteratorConcept<_OutputIterator, __typeof__(__unary_op(*__first))>)`
>   确保 `_OutputIterator` 能存储 `__unary_op` 返回的值，即输出迭代器需要支持将处理后的元素写入。
> - **范围约束：**
>   `__glibcxx_requires_valid_range(__first, __last)`
>   检查输入范围 `[__first, __last)` 的有效性，确保迭代器来自同一容器，且范围逻辑上合法。
>
> ------
>
> #### **(2) 主循环逻辑**
>
> ```cpp
> for (; __first != __last; ++__first, (void)++__result)
>     *__result = __unary_op(*__first);
> ```
>
> - **循环条件：**
>   `__first != __last` 确保输入范围尚未遍历完。
> - **迭代器更新：**
>   - `++__first`：移动到输入范围的下一个元素。
>   - `(void)++__result`：移动到输出范围的下一个位置。
>     - `(void)` 强制将表达式忽略为纯计算语句，无需保留返回值。
> - **核心操作：**
>   `*__result = __unary_op(*__first);`
>   - `*__first`：解引用输入迭代器，获取当前输入元素。
>   - `__unary_op(*__first)`：对当前输入元素应用一元操作。
>   - `*__result`：将结果存储到输出迭代器指向的位置。
>
> ------
>
> #### **(3) 返回值**
>
> ```cpp
> return __result;
> ```
>
> - 返回输出范围末尾的迭代器，指向最后一个存储的元素的下一个位置。
> - 这允许调用者使用返回值继续处理后续输出。

示例：

```cpp
struct transformTest01{
    int operator()(int val){
        return val + 100;
    }
};
struct print01{
    void operator()(int val){
        cout << val << " ";
    }
};
void test01(){

    vector<int> vSource;
    for (int i = 0; i < 10;i ++){
        vSource.push_back(i + 1);
    }

    //目标容器
    vector<int> vTarget;
    //给vTarget开辟空间
    vTarget.resize(vSource.size());
    //将vSource中的元素搬运到vTarget
    vector<int>::iterator it = transform(vSource.begin(), vSource.end(), vTarget.begin(), transformTest01());
    //打印
    for_each(vTarget.begin(), vTarget.end(), print01()); cout << endl;

}

//将容器1和容器2中的元素相加放入到第三个容器中
struct transformTest02{
    int operator()(int v1,int v2){
        return v1 + v2;
    }
};
void test02(){

    vector<int> vSource1;
    vector<int> vSource2;
    for (int i = 0; i < 10; i++){
        vSource1.push_back(i + 1);
    }
    for (int i = 0; i < 10; i++){
        vSource2.push_back(i + 1);
    }
    //目标容器
    vector<int> vTarget;
    //给vTarget开辟空间
    vTarget.resize(vSource1.size());
    transform(vSource1.begin(), vSource1.end(), vSource2.begin(),vTarget.begin(), transformTest02());
    //打印
    for_each(vTarget.begin(), vTarget.end(), print01()); cout << endl;
}
int main(){
    test01();
    test02();
    system("pause");
    return EXIT_SUCCESS;
}
/*101 102 103 104 105 106 107 108 109 110
2 4 6 8 10 12 14 16 18 20*/
```

## **4.7 常用查找算法**

```cpp
/*
	find算法 查找元素
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param value 查找的元素
	@return 返回查找元素的位置
*/
find(iterator beg, iterator end, value)
/*
	find_if算法 条件查找
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param  callback 回调函数或者谓词(返回bool类型的函数对象)
	@return bool 查找返回true 否则false
*/
find_if(iterator beg, iterator end, _callback);
/*
	adjacent_find算法 查找相邻重复元素
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param  _callback 回调函数或者谓词(返回bool类型的函数对象)
	@return 返回相邻元素的第一个位置的迭代器
*/
adjacent_find(iterator beg, iterator end, _callback);
/*
	binary_search算法 二分查找法
	注意: 在无序序列中不可用
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param value 查找的元素
	@return bool 查找返回true 否则false
*/
bool binary_search(iterator beg, iterator end, value);
/*
	count算法 统计元素出现次数
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param  value 统计的元素
	@return int返回元素个数
*/
count(iterator beg, iterator end, value);
/*
	count_if算法 统计满足要求的元素出现的次数
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param  callback 回调函数或者谓词(返回bool类型的函数对象)
	@return int返回元素个数
*/
count_if(iterator beg, iterator end, _callback);
```

## **4.8 常用排序算法**

```cpp
/*
	merge算法 容器元素合并，并存储到另一容器中
	@param beg1 容器1开始迭代器
	@param end1 容器1结束迭代器
	@param beg2 容器2开始迭代器
	@param end2 容器2结束迭代器
	@param dest  目标容器开始迭代器
*/
merge(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest)
/*
	sort算法 容器元素排序
	注意:两个容器必须是有序的
	@param beg 容器1开始迭代器
	@param end 容器1结束迭代器
	@param _callback 回调函数或者谓词(返回bool类型的函数对象)
*/
sort(iterator beg, iterator end, _callback)
/*
	random_shuffle算法 对指定范围内的元素随机调整次序
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
*/
random_shuffle(iterator beg, iterator end)
/*
	reverse算法 反转指定范围的元素
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
*/
reverse(iterator beg, iterator end)
```

## **4.9 常用拷贝和替换算法**

```cpp
/*
	copy算法 将容器内指定范围的元素拷贝到另一容器中
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param dest 目标起始迭代器
*/
copy(iterator beg, iterator end, iterator dest)
/*
	replace算法 将容器内指定范围的旧元素修改为新元素
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param oldvalue 旧元素
	@param oldvalue 新元素
*/
replace(iterator beg, iterator end, oldvalue, newvalue)
/*
	replace_if算法 将容器内指定范围满足条件的元素替换为新元素
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param callback函数回调或者谓词(返回Bool类型的函数对象)
	@param oldvalue 新元素
*/
replace_if(iterator beg, iterator end, _callback, newvalue)
/*
	swap算法 互换两个容器的元素
	@param c1容器1
	@param c2容器2
*/
swap(container c1, container c2)
```

## **4.10 常用算数生成算法**

```cpp
/*
	accumulate算法 计算容器元素累计总和
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param value累加值
*/
accumulate(iterator beg, iterator end, value)
/*
	fill算法 将指定范围 [beg, end) 内的所有元素设置为给定的值
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param value 想要设置的值
*/
fill(iterator beg, iterator end, value)
```

## **4.11 常用集合算法**

```cpp
/*
	set_intersection算法 求两个set集合的交集
	注意:两个集合必须是有序序列
	@param beg1 容器1开始迭代器
	@param end1 容器1结束迭代器
	@param beg2 容器2开始迭代器
	@param end2 容器2结束迭代器
	@param dest  目标容器开始迭代器
	@return 目标容器的最后一个元素的迭代器地址
*/
set_intersection(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest)
/*
	set_union算法 求两个set集合的并集
	注意:两个集合必须是有序序列
	@param beg1 容器1开始迭代器
	@param end1 容器1结束迭代器
	@param beg2 容器2开始迭代器
	@param end2 容器2结束迭代器
	@param dest  目标容器开始迭代器
	@return 目标容器的最后一个元素的迭代器地址
*/
set_union(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest)
/*
	set_difference算法 求两个set集合的差集
	注意:两个集合必须是有序序列
	@param beg1 容器1开始迭代器
	@param end1 容器1结束迭代器
	@param beg2 容器2开始迭代器
	@param end2 容器2结束迭代器
	@param dest  目标容器开始迭代器
	@return 目标容器的最后一个元素的迭代器地址
*/
set_difference(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest)
```

ps：参考：[STL基础教程.doc](https://blog-halo.oss-cn-guangzhou.aliyuncs.com/halo/2024/11/28/STL基础教程.doc)（黑马2017年C++视频资料）