---
layout: post
title: "STL真香！Vector容器一遍过（1）"
date: 2019-04-07
categories: OI
tags: [OI]  [STL]  [Vector] 
---

题目来自学校OJ（XOJ 3433 测验1256, 问题H:3433: 简单数列操作）

学校OJ水题多，适合打基础，基础打好了复习。之前因为一些naive错误，但我又知识水平低，很久没在xoj上做过题目了，上个月突然回来复习巩固基础，觉得还不错

题目在下面：
```
给你一个长度不超过1000的整数数列，写一个程序要求能完成以下操作：

    Q x y 表示查询第x～y个位置上的数分别是多少（数列位置从1计,x<=y）

    I x t 表示在第x个位上插入一个值为t的数，x之后的所有数往后移一位

    D x 表示将x位置上的数删除，x之后的所有数都往前移一位

    M x 表示将x位置上的数移到最前面（即1号位置），x之前的所有数都往后移一位

Input Data

第一行，两个整数n,q(n <= 1000, q<=100)，表示初始数的个数，和如上操作的次数
第二行，n个数，表示初始整数
第三行开始共有q行，每行一个操作，格式如题所述

所有位置数据保证合法（保证是在数列里面的操作）
Output Data

对于每个Q x y查询操作，请输出一行，即[x,y]范围内的数，这些数用空格分隔
```

读到这种题目，一般来说使用普通数组是很艰难的，可能很巨的人不这么认为，但我还是坚信普通数组无法完成，即使完成复杂度也很高。这种时候，C++的stl模板就很重要了。

今天先介绍一下vector

```
 vector(向量):是一种顺序容器，事实上和数组差不多，但它比数组更优越。一般来说数组不能动态拓展，因此在程序运行的时候不是浪费内存，就是造成越界。而vector正好弥补了这个缺陷，它的特征是相当于可分配拓展的数组，它的随机访问快，在中间插入和删除慢，但在末端插入和删除快。
```

但我很懒，喜欢用万能头文件。如果不用万能头文件，你可以使用```#include <vector> ```

定义方式很简单， ```vector<typename>amd;```即可定义一个为typename数据类型的向量，如int，即等价于一个数组。

```vector<int>::iterator it;```当然我更推荐用迭代器访问。

```
v1.push_back()   //在数组的最后添加一个数据
v1.pop_back()    //去掉数组的最后一个数据 
v1.front() 　　　　//返回第一个元素(栈顶元素)
v1.begin()           //得到数组头的指针，用迭代器接受
v1.end()             //得到数组的最后一个单元+1的指针，用迭代器接受
v1.clear()        // 移除容器中所有数据
v1.empty()         //判断容器是否为空
v1.erase(pos)        //删除pos位置的数据
v1.erase(beg,end)// 左开右闭区间清除元素
v1.size()         //回容器中实际数据的个数
v1.insert(pos,data) //在pos处插入数据
'''

然后，这道题就是道大水题了

'''
#include <bits/stdc++.h>
using namespace std;
vector <int> amd;
vector <int>::iterator it;
int main(){
	
	int n,q;
	cin>>n>>q;
	for(int i=0;i<n;i++){
		int x;
		cin>>x;
		amd.push_back(x);
	}
	while(q--){
		char ch;
		cin>>ch;
		switch(ch){
			case 'Q':{
				int x,y;
				cin>>x>>y;
				for(int j=x-1;j<y;j++){
					cout<<amd[j]<<" ";
				}
				cout<<endl;
				break;
			}
			case 'I':{
				int x,y;
				cin>>y>>x;
				it=amd.begin()+y-1 ;
				amd.insert(it,x); 
				break;
			}
			case 'D':{
				int x,y;
				cin>>y;
				it=amd.begin()+y-1;
				amd.erase(it); 
				
				
				
				break;
			}
			case 'M':{
				int x,y;
				cin>>y;
				x=amd[y-1];
				it=amd.begin()+y-1;
				amd.insert(amd.begin(),*it); 
				amd.erase(it+1);
                
				
				break;
			}
			
			
		}
	}
	
	
	
	
	return 0;
}
```
