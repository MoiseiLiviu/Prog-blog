---
layout: post
title: Uva 11085 Back to the 8-Queens
categories: Backtracking
statement: Given an array where each index is a column number and the values in the cell is the row for the queen in that column, print the minimum number of steps(changes of rows) to make the queens positions viable(none of them threaten each other);
input: here will be multiple test cases. Each case consists of a line containing 8 integers. All these integerswill be in the range [1, 8]. Thei-th integer indicates the row position of a queen in thei-th column.
output:  For each case, output the case number followed by the required output.Constraints :Total number of test cases will be less than 1000.
explanation: This is a typical queen backtracking.We just need to check all the possible cases and get the minimum delta(difference of postions between the input and the correct postioning), and we do that by exploring each row in each column, if the position chosen is viable(no threatening queens) then we just put the queen there and go to the next column and to the same thing(iterate over all rows and check if the position is good) if it's not backtrack and go the next row in the previous loop, if the last column was achieved, check the positions.
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=2026

---

  <span style='font-size:20px;font-weight:bold'>My code:</span>
{%highlight c++ linenos%}

  #include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	
	int k;
	while(!(cin>>k).eof()){
		vector<pair<int,int>> pairs;
		double dk = k;
		for(int x = 1;x<=20000;x++){
			for(int y = 1;y<=x;y++){
				double temp = ((double)x*y)/(x+y);
				if(temp>dk)break;
				if(temp==dk)pairs.push_back(make_pair(x,y));
				}
			}
			cout<<pairs.size()<<endl;
			sort(pairs.begin(),pairs.end(),[](auto &p1,auto &p2){
				if(p1.first==p2.first)return p1.second>p2.second;
				else return p1.first>p2.first;
				});
			for(const auto cell : pairs){
				printf("1/%d = 1/%d + 1/%d\n",k,cell.first,cell.second);
				}
		}
	return 0;
}
{%endhighlight%}