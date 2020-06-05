---
layout: post
title: Uva 11242 Tour De France
categories: Iterative
statement: A racing bicycle is driven by a chain connecting two sprockets. Sprocketsare grouped into two clusters the front cluster (typically consisting of 2 or 3 sprockets) and the rear cluster (typically consisting of between 5 and 10 sprockets). At any time the chain connects one of the front sprockets to one of the rear sprockets.The drive ratio { the ratio of the angular velocity of the pedals to thatof the wheels { is the quotient n=m where n is the number of teeth on the rear sprocket and m is the number of teeth on the front sprocket. Two driver ratios d1 < d2 are adjacent if there is no other drive ratio d1 < d3 < d2.The spread between a pair of drive ratios d1 < d2 is their quotient:d2 = d1.You are to compute the maximum spread between two adjacent drive ratios achieved by a particularpair of front and rear clusters.
input: Input consists of several test cases, followed by a line containing 0. Each test case is speci ed by the following input f the number of sprockets in the front cluster;•r the number of sprockets in the rear cluster f integers, each giving the number of teeth on one of the gears in the front cluster;r integers, each giving the number of teeth on one of the gears in the rear cluster.You may assume that no cluster has more than 10 sprockets and that no gear has fewer than 10 or more than 100 teeth.
Output: For each test case, output the maximum spread rounded to two decimal places.
explanation: Easy problem solvable with 2 nested for loops one for iterating over the first cluster and second for the second respectively, thus forming pairs and computing the drive ratio for each pair and pushing this values into a vector.After we sort this vector to obtain the adjacency list of the ratios, and then we just find the maximum spread by iterating over this vector.
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=2183
---


<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	int f,r;
	while(cin>>f,f){
		cin>>r;
		vector<int> fTeeth(f);
		vector<int> rTeeth(r);
		vector<double> ratios;
		for(auto &cell : fTeeth){
			cin>>cell;
			}
		for(auto &cell : rTeeth){
			cin>>cell;
			}
		for(auto fCell : fTeeth){
			for(auto rCell : rTeeth){
				ratios.push_back((double)rCell/fCell);
				}
			}
		sort(ratios.begin(),ratios.end());
		for(auto cell : ratios)cout<<cell<<endl;
		double maxR = -1;
		for(int i = 0;i<(int)ratios.size();i++){
			if(i!=0)maxR = max(maxR,ratios[i]/ratios[i-1]);
			if(i!=(int)ratios.size()-1)maxR = max(maxR,ratios[i+1]/ratios[i]);
			}
		printf("%.2lf\n",maxR);
		}
	
	return 0;
}
{%endhighlight%}
