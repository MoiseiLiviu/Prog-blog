---
layout: post
title: Uva 1062 Containers
categories: Stack
statement: A seaport container terminal stores large containers that are eventually loaded on seagoing ships for transport abroad. Containers coming to the terminal by road and rail are stacked at the terminal as they arrive.Seagoing ships carry large numbers of containers. The time to load a ship depends in part on the locations of its containers. The loading time increases when the containers are not on the top of the stacks, but can be fetched only after removing other containers that are on top of them.The container terminal needs a plan for stacking containers in order to decrease loading time.The plan must allow each ship to be loaded by accessing only topmost containers on the stacks, and minimizing the total number of stacks needed.For this problem, we know the order in which ships must be loaded and the order in which containers arrive. Each ship is represented by a capital letter between A and Z (inclusive), and the ships will beloaded in alphabetical order. Each container is labeled with a capital letter representing the ship onto which it needs to be loaded. There is no limit on the number of containers that can be placed in asingle stack.
input:  The input file contains multiple test cases. Each test case consists of a single line conOlderp A, then ship B, and so on.A line containing the word end follows the last test case.
Output: For each input case, print the case number (beginning with 1) and the minimum number of stacks needed to store the containers before loading starts. Your output format should be similar to the one shown here.
explanation: This problem can be solved by using disjoint sets as a custom data structure or use a lazy aproach as i did.For the container to be picked without any trouble it should be on top of its stack or be the only element of its stack,thus the only time we should create a new stack is when all the stacks have on top chars smaller than the given container.Ex if the tops are  'A','B','C' then container 'Z' should be placed in a new stack or otherwise it will block the others.If there is a smaller char container we choose the smallest stack top which is bigger than the giver container and we override this ending with the new character.
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=3503
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{% highlight c++ linenos%}

#include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	string in;
	int t = 1;
	while(cin>>in){
		if(in=="end")break;
		vector<char> endings;
		for(const char ch : in){
			char minCh = 'z';
			int index = 0,minIndex = 0;
			for(const char ch1 : endings){
				if(ch1>ch){
					if(minCh>ch1){
						minIndex = index;
						minCh = ch1;
						}
					}
				    if(ch==ch1){
					minCh = 'e';
					break;
					}
				    index++;
				}
				if(minCh == 'z')endings.push_back(ch);
				else if(minCh=='e')continue;
				else endings[minIndex] = ch;
			}
			cout<<"Case "<<t<<": "<<endings.size()<<endl;
			t++;
		}
	
	return 0;
}

{% endhighlight %}