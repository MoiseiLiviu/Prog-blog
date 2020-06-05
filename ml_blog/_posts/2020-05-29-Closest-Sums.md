---
layout: post
title: Uva 10487 Closest Sums
categories: Iterative Brute_force
statement: Given is a set of integers and then a sequence of queries. A query gives you a number and asks to  find a sum of two distinct numbers from the set, which is closest to the query number.
input: Input contains multiple cases.Each case starts with an integer n (1 < n < 1000), which indicates, how many numbers are in the set of integer. Next n lines contain n numbers. Of course there is only one number in a single line. The next line contains a positive integer m giving the number of queries, 0 < m < 25. The next m lines contain an integer of the query, one per line.Input is terminated by a case whose n= 0. Surely, this case needs no processing.
Output: Output should be organized as in the sample below. For each query output one line giving the query value and the closest sum in the format as in the sample. Inputs will be such that no ties will occur.
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&category=113&page=show_problem&problem=1428
explanation: Very simple problem, we just need to compute every possible pair from the set and compare for each pair the sum with the query value. 
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

  #include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	int n,m,q,tc = 1;
	while(cin>>n,n){
					printf("Case %d:\n",tc++);

		vector<int> a(n);
		for(auto &cell : a){
			cin>>cell;
			}
		cin>>m;
		while(m--){
			cin>>q;
			int minn = INT_MAX;
			int sum;
			for(int i = 0;i<n;i++){
				for(int j = 0;j<n;j++){
					if(a[i]!=a[j]){
						if(minn>abs(a[i]+a[j]-q)){
							sum=a[i]+a[j];
							minn = abs(a[i]+a[j]-q);
							}
						}
					}
				}
				printf("Closes sum to %d is %d\n",q,sum);
			  }
			}		
	
	return 0;
}
{%endhighlight%}
