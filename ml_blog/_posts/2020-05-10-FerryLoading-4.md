---
layout: post
title: Uva 11034 Ferry Loading IV
categories: Queue
statement:  Before bridges were common, ferries wereused to transport cars across rivers.  River ferries, unlike their larger cousins, run on a guide line and are powered by the river's current.   Cars  drive  onto  the  ferry  from one  end,  the  ferry  crosses  the  river,  and the  cars  exit  from  the  other  end  of  the ferry.There  is  an l-meter-long  ferry  that crosses the river.  A car may arrive at either river bank to be transported by the ferry to the opposite bank. The ferry travels  continuously  back  and  forth  between the banks so long as it is carrying a car or there is at least one car waiting at either bank.  Whenever the ferry arrives at oneof the banks,  it unloads its cargo and loads up cars that are waiting to cross as long as they  t onits deck.  The cars are loaded in the order of their arrival; ferry's deck accommodates only one lane ofcars.  The ferry is initially on the left bank where it broke and it took quite some time to  x it.  In the meantime, lines of cars formed on both banks that await to cross the river.
input: The first line of input contains c, the number of test cases.  Each test case begins with l,m.m lines follow describing the cars that arrive in this order to be transported.  Each line gives the length of a car (in centimeters), and the bank at which the car arrives (`left' or `right').
Output: For each test case, output one line giving the number of times the ferry has to cross the river in order to serve all waiting cars.
explanation: The problem is easily solvable with queues, we just need to simulate the process.First ,we create two queues for both banks and fill them with the length of the cars in centimetres waiting there.Then we just alternate between the banks taking as many cars as possible until there are no cars remaining on either bank.
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=1975
---


<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

#include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	
	int c;
	cin>>c;
	while(c--){
		
		queue<int> L,R;
		int l,m,l1;
		char bank[10];
		cin>>l>>m;
		l*=100;
		while(m--){
			cin>>l1>>bank;
			if(bank[0]=='l')L.push(l1);
			else R.push(l1);
			}
	    bool flag = false;int res = 0,sum;
	    while(!R.empty()||!L.empty()){
			res++;sum=0;
			if(flag){
				while(!R.empty()&&sum+R.front()<=l){
					sum+=R.front();R.pop();
					}
				}
			else{
				while(!L.empty()&&sum+L.front()<=l){
					sum+=L.front();L.pop();
					}
				}
			flag=!flag;
			}
			cout<<res<<endl;
		}
	
	return 0;
}
{%endhighlight%}
