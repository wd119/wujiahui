# STL标准模板库

容器 算法 迭代器

六大组件 容器 算法 迭代器 仿函数 适配器 空间配置器

迭代器：容器和算法之间桥梁相当于指针

仿函数：行为类似函数，可作为算法的某种策略

算法分为质变算法非质变算法

容器分为序列式容器和关联式容器

### vector

~~~c++
//创建一个vector容器
vector<int>v;
//向容器中插入数据
v.push_back(10);
//通过迭代器访问容器中的数据
vector<int>::iterator itbegin=v.begin();//起始迭代器 指向容器中第一个元素
vector<int>::iterator itend=v.end();//结束迭代器 指向容器中最后一个元素的下一关位置
while(itbegin!=itend){
    cout<<*itbegin<<endl;
    itbegin++;
}
//法二
for(vector<int>::iterator it =v.begin();it!=v.end;it++){
    cout<<*it<<endl;
}
//法三
#include<algorithm>
for_each(v.begin(),v.end(),myprint);
~~~

| 函数                | 功能描述                                           |
| ------------------- | -------------------------------------------------- |
| `size()`            | 返回当前元素数量                                   |
| `capacity()`        | 返回当前容量（最多可容纳的元素数，不扩容情况下）   |
| `empty()`           | 判断是否为空（`size() == 0` 时返回 `true`）        |
| `push_back(val)`    | 在尾部添加元素                                     |
| `pop_back()`        | 删除尾部元素                                       |
| `clear()`           | 清空所有元素（`size()` 变为 0，`capacity()` 不变） |
| `reserve(n)`        | 预先分配容量为 `n`（避免多次扩容的性能损耗）       |
| `resize(n)`         | 调整大小为 `n`（多余元素被删除，不足则补默认值）   |
| `begin()` / `end()` | 返回指向首元素 / 尾元素后一位的迭代器              |

（*it）的数据类型与<>里的数据类型相同

#### vector容器的赋值

1. operator=

~~~c++
vector<int>v1;
for(int i=0;i<10;i++){
v1.push_back(i);
}
vector v2;
v2=v1;
~~~

2. assign

~~~c++
vector<int>v3;
v3.assign(v1.begin(),v1.end());//左闭右开
~~~

3. n个elem方式赋值

~~~c++
vector<int>v4;
v4.assign(10,100);
~~~

#### vetor容量和大小

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-09%20101550.png)

capacity>=size

指定更长用0来填充

第二个重载的resize可任意填充

#### 插入和删除

1. 尾插push_back
1. 尾删pop_back
1. 插入

~~~c++
v.insert(v1.begin(),2,100)//(迭代器，个数，插入值)
~~~

4. 删除

~~~c++
v.erase(v1.begin(),v1.end())
~~~

#### 数据存取

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-09%20104248.png)

#### 互换容器

~~~c++
v.swap(v1)
~~~

可以用这个方法释放多余内存

~~~c++
vector<int>(v).swap(v);
~~~

vector<int>(v) 根据v的大小初始化这个匿名对象的大小

swap交换容器 v指向更改后的容器 匿名对象被回收

#### 容器嵌套容器

类似于二维数组

~~~c++
vector<vector<int>>v
~~~

#### 预留空间

reserve(int len)预留len个元素长度，预留位置不初始化，*元素不可访问*

不需要总换新空间 数据量较大时可以用

## string

其实是个类 本质就是char*

### string的构造函数

1. string();默认构造 eg: string str;
1. 使用字符串S初始化 string(const char*s);
1. 使用一个string对象初始化另一个string对象  string(const string&str)
1. 使用n个字符c初始化

~~~c++
string s(10,'a');
//输出aaaaaaaaaa
~~~

###  赋值操作

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-04%20145317.png)

### 字符串拼接

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-04%20150008.png)

### string查找和替换

~~~c++
//查找
string str1="avsfsaf";
int pos=str1.find("vs");
~~~

rfind是从右往左查找 find从左往右查找

返回索引 找不见返回-1

替换：

~~~c++
string str="abcdefg";
str.replace(1,3,"1111");
//从一号位置起到3个字符，替换为“1111”
~~~

### 字符串比较

逐个字符的ASCLL码进行比较

= 返回0

/   >返回1 < 返回-1

~~~c++
string str1="hello";
string str2="hello";
if(str1.compare(str2)==0){
    cout<<"二者相等"<<endl;
}
~~~

### 字符存取

1. 通过[]访问单个字符
1. 通过at方式访问单个字符

~~~c++
str.at(t)==str[t]
~~~

允许修改

### 插入和删除

str.insert(插入角标,”插入内容”)；

删除str.erase(插入角标,”删除内容”)

### 子串

str.substr(x,x2)从哪开始 x2截多少个

substr默认的截取到字符串末尾 string::npos



## deque容器

内部有一个中控器 维护每段缓冲区的内容 支持头插头删

### 构造函数

deque<T>d;

deque<int>d2(起始迭代器，末尾迭代器)

deque<int>d3(d2);

deque<int>d4(n,num);

赋值与vector相同

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-10%20104551.png)

deque容器没有容量

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-10%20110049.png)

插入和删除的位置提供的是迭代器

### 排序

#include<algorithm>

标准算法头文件

sort(d.begin(),d.end())

默认升序

vector也适用

## stack容器

栈 先进后出像 弹夹

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-13%20184506.png)

栈不允许有遍历元素

栈可以判断容器是否为空 empty

### 构造函数

1. stack<T>stk;
1. 拷贝构造 stack(const stack &stk)

### 常用接口

1. 增加元素.push()
1. 栈顶元素出栈  .pop();
1. 查看栈顶元素 .top();
1. 返回栈的 长度 .size();

## queue容器

队列容器   *先进先出*

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-13%20190102.png)

也不允许有遍历行为

只有对头对尾可以访问

### 构造函数

1. queue<T>que;
1. queue(const queue&que);

### 常用接口

1. 判空 .empty()
1. 添加 .push();
1. 访问队头 .front();
1. 访问队尾 .back();
1. 查看长度 .size();
1. 删除元素 .pop();

## list链表

### 存储结构

1. 链表由若干结点构成 结点分为数据域和指针域

2. 头指针指向头结点（如果有，可以不存储数据，可以存储数据元素类型相同的附加信息）

指向首元结点

3. STL为双向循环链表  

4. 插入和删除操作不会造成原有lit迭代器的失效，在vector是不成立的

### 构造函数

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-16%20190041.png)

### 赋值

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-16%20190343.png)

### 大小操作

1. size()返回元素数量
1. empty()判空
1. resize()重新指定大小

### 插入和删除

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-16%20200341.png)

### 数据存取

不支持随机访问原因list本质链表，不是连续线性空间存储数据

只有front()

end()

仅支持自增自减

if |it=it +1不报错 则不支持随机访问

### 反转与排序

1. reverse()首位对调
1. 运用算法库的sort算法排序不可行 不能随机访问的不能用全局的sort算法

自带着成员函数sort 默认升序

如果自定义排序

bool compare(){

return }

## set容器/multiset容器

关联式容器 底层结构是二叉树

所有元素在插入时自动被排序

set容器不允许有重复元素

multiset允许有重复元素

### 构造与赋值

1. 插入数据只有insert 
1. 不允许插入重复
1. 拷贝构造set<int>s(s1)
1. 赋值s=s1

### 大小和交换

不允许用resize

1. size()返回元素数目
1. empty()判空
1. swap(st);交换两个集合容器

### 插入和删除

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-19%20182656.png)

### 查找与统计

1. find(key)

查找到返回迭代器

~~~c++
set<int>::iterator pos=s.find(30);
if(pos!=s.end()){
    cout<<"找到元素"<<*pos<<endl;
}
else{
    cout<<"未找到"<<endl;
}
~~~

2. 统计

s.cout(30);对于set而言不是1就是0

### multiset和set区别

1. set 的insert方法返回pair类型，multiset返回迭代器

### pair对组

成对出现的两个数据，可卡因返回两个数据

1. 创建pair<string,int>p(x,x)

p.first()         p.second()

 pair<string,int>p2=make_pair(x,y)

### set容器排序

~~~c++
class MyCompare {
public:
	bool operator()(int v1,int v2) const{
		return v1 > v2;
	}
};
set<int, MyCompare>s2;
s2.insert(50);
s2.insert(6);
s2.insert(10);
s2.insert(5);
for (set<int,MyCompare>::iterator it = s2.begin();it != s2.end();it++) {
	cout << (*it) << " ";
}
~~~

## map容器

map元素全是pair

pair 第一个元素为key键第二个元素为值

### map构造和赋值

1. map<int>m;
1. 插入元素m.insert(pair<int>(1,10));
1. 会根据key值大小进行排序
1. 还可以进行拷贝构造 map<int,int>m2(m);

### 大小和交换

1. size()返回容器中元素的数目
1. empty()判断容器是否为空
1. swap（）交换两个集合容器

### 插入与删除

1. m.insert(pair<int,int>10,10)
1. m.insert(make_pair(2,20))
1. m[4]=40;
1. 可以通过[]由key查询value值
1. m.erase(key)根据key删
1. 清空m.clear()

### 查找与统计

1. 查找find()


~~~c++
map<int,int>::iterator pos=m.find(key)
~~~

未找到返回m.end()

2. 统计 int num=m.count(key)

map不允许插入重复key元素，count统计而言 结果要么0要么1

multimap的count统计可能大于1

### 排序

与set一样创建一个仿函数

# 函数对象

## 仿函数

本质是一个类

1. 函数对象在使用时，可以像普通函数那样调用，可以有参数，也可以有返回值

eg：

~~~c++
class myadd{
public:
    int operator()(int v1,int v2){
        return v1+v2;
    }
    
}
int main(){
    myadd m;
    m(10,10);
    return 0;
}
~~~

2. 函数对象超出普通函数的概念，函数对象可以有自己的状态

~~~c++
class myprint{
public:
    myprint(){
        this->count=0;
    }
    void operator()(string test){
        cout<<test<<endl;
        this->count++;
    }
    int count;//内部自己的状态
}
~~~

3. 函数对象可以作为参数传递

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-09-25%20194758.png)

# 谓词

## 概念

1. 返回值为bool类型的仿函数为谓词
1. 如果operator（）接受一个参数，那么叫做一元谓词
1. 如果operator（）接受两个参数，那么叫做二元谓词                                       

# 内置仿函数

需要包含头文件

#include<functional>

## 算术仿函数

### 取反仿函数

negate<int>n;

n(50)

输出-50

## 加法仿函数

plus<int>p;

p(10,20);

![](https://www-h1258.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-02%20180903.png)

## 关系仿函数

~~~c++
sort(v.begin,v.end(),greater<int>());
    //大于
~~~

## 逻辑仿函数

逻辑非

logical_not<bool>

真假转换

# 算法

## 常用遍历算法

### for_each

~~~c++
//普通函数
void print01(int val){
    cout<<val<<" ";
}
//仿函数
class print02{
public:
    void operator()(int val){
        cout<<val<<" ";
    }
}
vector<int>v;
for(int i=0;i<10;i++){
    v.push_back(i);
}
for_each(v.begin(),v.end(),print01);
//普通函数只需要传递函数名（指针）
for_each(v.begin(),v.end().print02());
//仿函数传递需要创建一个匿名对象
~~~

### transfrom

交换容器

~~~c++
class Transfrom
{
public:
    int operator()(int v){
        return v;
        }
}
vector<int>v;
for(int i=0;i<10;i++){
    v.push_back(i);
}
vector<int>vtarget;//目标容器\
vtarget.resize(v.size());//目标容器提前定好大小
transfrom(v.begin,v.end(),vtarget.begin(),Transfrom);
//Transfrom可以做其他的逻辑运算
~~~

## 查找算法

### find

查找内置数据类型

find(迭代器起始位置，迭代器末尾,查找目标)

~~~c++
vector<int>v;
for(int i=0;i<10;i++){
    v.push_back(i);
}
vector<int>::iterator it=find(v.begin(),v.end(),5);
~~~

自定义类型

~~~c++
class person{
public:
    person(string name,int age){
        this->m_age=age;
        this->m_name=name;
    }
    bool operator==(const person &p){
        if(m_age==p.m_age&&m_name=p.m_name){
            return true;
        }
        else{
            return false;
        }
    }
    int m_age;
    int m_name;
}





pw("aaa",12);
vector<person>::iterator  it=find(v.begin(),v.end(),pw);
if(it==v.end()){
    cout<<"未找到"<,endl;
}
~~~

### find_if

find_if(起始迭代器，结束迭代器，谓词)；

### adjacent_find

查找相邻重复元素

返回第一个相邻重复元素的迭代器

### binary_search

查找指定元素是否存在返回true 或 flase

必须是有序对象

### cout

统计元素数量

cout(起始迭代器,结束迭代器,查找元素)

统计自定义类型需要重载==

### cout_if

cout_if(起始迭代器,结束迭代器,谓词)

## 排序算法

### sort

sort(起始迭代器,末尾迭代器,谓词)

### random_shuffle

洗牌算法 打乱顺序

random_shuffle(v.begin(),v.end())

加一个随机数种子

#include<ctime>

主函数中加

srand(unsigned int)time(NULL);

### merge

注意：两个容器必须是有序的

需要提前开辟空间

### reverse

v.reverse(起始迭代器，结束迭代器)
