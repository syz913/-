## 目录

- [set操作](#set操作)
- [字符串操作](#字符串操作)
- [文件操作](#文件操作)

### set操作

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

```
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
```

string spaces(, ' '); 生成 n个空格给spaces，其中注意必须是字符不能是字符串

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

