---
layout: post
title: 11991 - Easy Problem from Rujia Liu?
statement: Though Rujia Liu usually sets hard problems for contests (for example, regional contests likeXi'an 2006, Beijing 2007 and Wuhan 2009, or UVa OJ contests like Rujia Liu's Presents 1and 2), he occasionally sets easy problem (for example, `the Coco-Cola Store' in UVa OJ),to encourage more people to solve his problems :D Given an array, your task is to find the k-th occurrence (from left to right) of an integer v. To make the problem more difficult (and interesting!), you'll have to answer m such queries.
input: There are several test cases. The first line of each test case contains two integers n, m (1 <= n;m <= 100;000), the number of elements in the array, and the number of queries. The next line contains n positive integers not larger than 1,000,000. Each of the following m lines contains two integer k and v (1 < k < n, 1 <= v <= 1.000.000). The input is terminated by end-of-file (EOF).
Output: For each query, print the 1-based location of the occurrence. If there is no such element, output `0'instead.
explanation: The input is to big to just iterate and mantain a counter for each querry, so a better way is maintaining the index for each encounter in a map where the key is a number from the array and the value is another map where the key is the k occurence of the number and the value is the coresponding index.So after reading the input we can fetch the indeces map[v][k].
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=3142
categories: Map
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	int n,m;
	while(!(cin>>n>>m).eof()){
		map<int,map<int,int>> occ;
		int value,k,v;
		for(int i = 0;i<n;i++){
			cin>>value;
			occ[value][occ[value].size()+1]=i;
			}
	    while(m--){
			cin>>k>>v;
			int ind = occ[v][k];
			ind = ind==0?0:ind+1;
			cout<<ind<<endl;
			}
		}
	
	return 0;
}
{%endhighlight%}