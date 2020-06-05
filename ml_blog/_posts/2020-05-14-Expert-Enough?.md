---
title: Uva 1237 - Expert enough?
layout: post
categories: Map
statement: Auto-mobile Charting & Manufacturing (ACM) is a company that specializes in manufacturing auto-mobile spare parts. Being one of the leading automotive companies in the world, ACM are sure to keepup the latest information in that world. In the 100-year anniversary of the company, ACM compiled a huge list of range of prices of any automobiles ever recorded in the history. ACM then wants to develop a program that they called Automobile Expert System or AES for short.The program receives a price P as an input, and searches through the database for a car maker in which P falls in their range of lowest price L and highest price H of car they ever made. The program then output the car maker name. If the database contains no or more than one car maker that satis esthe query, the program produce output `UNDETERMINED' (without quotes). Not so expert, huh? You are about to develop that program for ACM.
input: The input begins with a line containing an integerT(T < 10), the number of test cases follow. Eachcase begins with the size of the database D (D < 10000). The next each ofDlines contains M,Land H(0 < L < H < 1000000) which are the name of the maker (contains no whitespace and will never exceeds 20 characters), the car's lowest price the maker ever made, and the car's highest price the maker ever made respectively. Then there is the number of query Q(Q < 1000) follows. Each ofthe next Q lines contains an integer P(0 < P < 1000000), the query price.
Output: Output for each query should be one line containing the name of the maker, or the string `UNDETERMINED'(without quotes) if there is no maker or more than one maker that satisfies the query. You should separate output for different case by one empty line.
explanation: Considering that there are <=10000 companies names for maximum 10 test cases with 1000 companies, the complexity of simply looping through all the companies comes at 10^8 which is not ideal but viable for a 3 seconds time limit so using a vector<pair<string<int,int>>> is a way of solving this problem.
link: https://onlinejudge.org/index.php?option=onlinejudge&page=show_problem&problem=3678
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	vector<pair<string,pair<int,int>>>types;
	int t;
	cin>>t;
	while(t--){
		
		int D,L,H,Q,P;
		string name;
		cin>>D;
		while(D--){
			cin>>name>>L>>H;
			types.push_back(make_pair(name,make_pair(L,H)));
			}
		cin>>Q;
		while(Q--){
			cin>>P;int cnt = 0;string singular;
			for(const auto cell : types){
				if(cell.second.first<=P&&cell.second.second>=P){cnt++;singular = cell.first;}
				}
			if(cnt == 1)cout<<singular<<endl;
			else cout<<"UNDETERMINED"<<endl;
			}
		}
	
	return 0;
}
{%endhighlight%}