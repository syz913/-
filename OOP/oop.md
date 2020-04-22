## 目录

- [set操作](#set操作)
- [map操作](#map操作)
- [字符串操作](#字符串操作)
- [vector操作](#vector操作)
- [文件操作](#文件操作)
- [设置精度](#设置精度)
- [快捷键](#快捷键)

### set操作

> set是一种关联式容器，其特性如下：
>
> - set以RBTree作为底层容器
> - 所得元素的只有key没有value，value就是key
> - 不允许出现键值重复
> - 所有的元素都会被自动排序
> - 不能通过迭代器来改变set的值，因为set的值就是键

```C++
unordered_set代表是无序的，
set<int> numSet;
    for(int i=0;i<6;i++)
    {
        //2.1insert into set
        numSet.insert(numList[i]);
    }
    //2.travese set
    for(set<int>::iterator it=numSet.begin() ;it!=numSet.end();it++)
    {
        cout<<*it<<" occurs "<<endl;
    }
    //3.set find useage

    int findNum=1;
    if(numSet.find(findNum)!=numSet.end())
    {
        cout<<"find num "<<findNum<<" in set"<<endl;
    }else{
        cout<<"do not find num in set"<<findNum<<endl;
    }
    //set delete useage
    int eraseReturn=numSet.erase(1);
    if(1==eraseReturn)
    {
          cout<<"erase num 1 success"<<endl;
    }else{
        cout<<"erase failed,erase num not in set"<<endl;
    }
```

### 字符串操作

```c++
1.string类型的声明： 
string s;

2.string类型的初始化:    
string s="abcd";   或者   string s="a  b   cd";
这两种分别是不带空格和带空格的初始化，是都可以的。

3.string类型的读入:
cin>>s;             //不能读入空格，以空格、制表符、回车符作为结束标志
getline(cin,s);   //可以读入空格和制表符，以回车符作为结束标志

4.求string类型的长度：
int len=s.size();    或者     int len=s.length();
两种方法是等价的

5.求string类型下标为i的字符:
s[i]        或        char c=s.at(i)

6.查找t是否为s的子串:
s.find(t);
如果t是s的子串则返回首次匹配的位置，否则返回 string::npos 或 -1

7.字符数组转string类型:
s=str;
str为char数组，s为string类型

8.string类型转字符数组:
strcpy(str,s.c_str());
需要引用string.h头文件

9.两个string比较大小：
if(s1<s2);       或       s1.compare(s2);
相等时返回0；s1>s2时返回1，s1<s2时返回-1

10.两个string连接：
s1=s1+s2;        或       s1.append(s2);

11.对string类型数组排序
string s[100];
sort(s,s+n,cmp);
int cmp(string a,string b)
{
    return a<b; //或a>b;
}

12. 字符串提取
   str2 = str1.substr();
   str2 = str1.substr(pos1);
   str2 = str1.substr(pos1,len1);
   string a=s.substr(0,4);       //获得字符串s中 从第0位开始的长度为4的字
 
符串
 
13. 字符串搜索
   where = str1.find(str2);
   where = str1.find(str2,pos1); pos1是从str1的第几位开始。
   where = str1.rfind(str2); 从后往前搜。
 
14. 插入字符串
   不是赋值语句。
   str1.insert(pos1,str2);
   str1.insert(pos1,str2,pos2,len2);
   str1.insert(pos1,numchar,char);    numchar是插入次数，char是要插入的字
符。
 
15. 替换字符串
   str1.replace(pos1,str2);
   str1.replace(pos1,str2,pos2,len2);
 
16. 删除字符串
   str.erase(pos,len)
   str.clear();
 
17. 交换字符串
   swap(str1,str2);
18. 反转字符串
    reverse(s.begin(),s.end())
    
 
```

string spaces(, ' '); 生成 n个空格给spaces，其中注意必须是字符不能是字符串

### vector操作

```C++
vector<int> ret;
ret.insert(ret.end(), bottom.begin(), bottom.end());
copy(bottom.begin(), bottom.end(), back_insert(ret));

remove_copy(bottom.begin(), bottom.end(), back_insert(ret), 0);
//copy的时候把0移除

find_if()函数，它接收一个函数对象的参数作为参数， 并使用它来做更复杂的评价对象是否和给出的查找条件相符。

accumulate(ret.begin(), ret.end(), 0.0);加起来ret的所有值，初始值为0.0
```

![image-20200415122307193](C:\Users\syz\AppData\Roaming\Typora\typora-user-images\image-20200415122307193.png)

### map操作

> map以RBTree作为底层容器
>
> 所有元素都是键+值存在
>
> 不允许键重复
>
> 所有元素是通过键进行自动排序的
>
> map的键是不能修改的，但是其键对应的值是可以修改的

```c++
mapstring.insert(pair<string,string>("a","b")) // pair<string,string> 必不可少，并且里面的两个类型要与定义一致
mapstring["c"]="d";


1)find() 查找并且找出value 2）count() 确定key是否存在，存在返回1，不存在返回0
1）find形式：比较麻烦，需要借助迭代器
//定义迭代器 map<string,string>::iterator iter;
iter=mapstring.find("a")
if(iter!=mapstring.end()) //用这种方式迭代器迭代不到最后，说明键值是存在的
cout<<iter->first<<endl; //iter->first 这指的是key iter->value 指的是value
else
cout<<cant not find this key<<endl;
2） mapstring.count(key) //这种情况下直接用就可以了
    
    
    iter =mapstring.find(key); // 即使key不存在也不会报错，因为有if进行判断，存在才删除
if(iter!=mapstring.end()) //这里的iter迭代器和上面一样的，定义是一样的。
mapstring.erase(iter);


for(iter=mapstring.begin();iter!=mapstring.end;iter++) //迭代打印
cout<<iter->first<<"="<<iter->second<<" ";
```

### 文件操作

C++ 中有三个用于文件操作的文件类：

- ifstream 类，它是从 istream 类派生来的，用于支持从磁盘文件的输入。
- ofstream 类，它是从 ostream 类派生来的，用于支持向磁盘文件的输出。
- fstream 类，它是从 iostream 类派生来的，用于支持对磁盘文件的输入输出。

```C++
ofstream outfile("a.txt", ios::out);
    if (!outfile){
        cerr << "Failed to open the file!";
        return 1;
    }
    // 写入数字 1-5 到文件中
    for (int i = 1; i < 6; i++){
        outfile << i << '\n';
    }
    outfile.close();
    ifstream infile("a.txt", ios::in);
    if (!infile){
        cerr << "Failed to open the file!";
        return 1;
    }
    char data;  // 从文件中读出数字 1-5 
    for (int i = 1; i < 6; i++){
        infile >> data;
        cout << data << '\n';
    }
    infile.close();
```

https://zhuanlan.zhihu.com/p/49757495

### 设置精度

```C++
cout.setf(ios::right); // 设置对齐方式
cout.width(8); //设置输出宽度
cout.fill('0'); //将多余的空格用0填充
cout.precision(2); //设置输出精度，保留有效数字
cout.setf(ios::showpoint); //将小数精度后面的0显示出来
cout.flags(ios::fixed);//这时候precision就是保留小数点后几位

cout << setprecision(2)<<1.25 << endl;
同样的cout<<fixed<<setprecision(2)<<1.25<<endl;(在<iomanip>中)

streamsize，这样的int类型的类型来特别表达有关流的当前操作位置以及长度问题(在<ios>中)
```

排序操作

```C++
sort (myvector.begin(), myvector.begin()+4); 

bool myfunction (int i,int j) { return (i<j); }//升序排列
sort (myvector.begin()+4, myvector.end(), myfunction);

sort第三个参数中可以使用lambda表达式自定义排序
vector<A> test;
sort(test.begin(),test.end(),[](A x,A y){return x.a>y.a;});
在sort函数的第三个参数中，[]表示需要作用域的哪些参数传入，这里为空，表示不需要传入任何参数，常见的有=和&，(A x, A y)表示两个入参，{}里面表示执行的函数，这里将返回值给省略了，根据return确定是bool类型的返回值。
```

### 快捷键

```
CTRL + K CTRL + F 格式化
Ctrl + K，Ctrl + C = 注释选定行
Ctrl + K，Ctrl + U = 取消选定行的注释
Ctrl + K，Ctrl + D = 正确对齐所有代码
```

18j9bk65