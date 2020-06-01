---
layout: post
title: Uva 524 - Primes Ring
categories: Backtracking
statement: A ring is composed ofn(even number) circles as shown in diagram.Put natural numbers1;2;:::;ninto each circle separately, and thesum of numbers in two adjacent circles should be a prime.
input: n(0 < n < 16) .
Output: The output format is shown as sample below. Each row represents a series of circle numbers in thering beginning from 1 clockwisely and anticlockwisely. The order of numbers must satisfy the aboverequirements.You are to write a program that completes above process.
explanation: Considering the input size, this is a good case for using backtracking and simply trying all the possible pairs while mainting a vector of used numbers in the range for each observed case.So starting with 1,we simply try substracting 1 from every prime number until 31(because 15+16 are the biggest pair possible) and we check if the result of the substraction was not yet used,if it wasn't we just carry on with this current number and do the same process;
link:  https://onlinejudge.org/index.php?option=onlinejudge&page=show_problem&problem=465;
---

  <span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

  #include <bits/stdc++.h>
using namespace std;

int N;

vector<int> primes = {3, 5, 7, 11, 13, 17, 19, 23, 29, 31};

void printAll(vector<int> v,int k,int cnt){
	
	
	if(cnt==N){
		if(find(primes.begin(),primes.end(),k+1)!=primes.end()){
		for(auto cell : v)cout<<cell<<" ";
		cout<<endl;}
		}
	
	for(auto prime : primes){
		int candidate = prime-k;
		if(candidate>0&&candidate<=N&&find(v.begin(),v.end(),candidate)==v.end()){
			vector<int> r(v);
			r.push_back(candidate);
			printAll(r,candidate,cnt+1);
			}
		}
	}

int main(int argc, char **argv)
{
	int tc = 1;
	while(cin>>N){
		vector<int> v={1};
		printf("Case %d:\n",tc++);
		printAll(v,1,1);
		cout<<endl;
		}
	return 0;
}
{%endhighlight%}
