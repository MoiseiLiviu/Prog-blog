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

int row[8];
vector<int> v;
int MIN;

bool place(int c,int r){
	for(int i = 0;i<c;i++){
		if(row[i]==r||abs(c-i)==abs(row[i]-r))return false;
		}
	return true;
	}
void backtracking(int c){
	if(c==8){
		int delta = 0;
		for(int i = 0;i<8;i++){
			cout<<row[i]<<" ";
			if(v[i]!=row[i])delta++;
			}
			cout<<endl;
			MIN=min(MIN,delta);
		}
	else{
		for(int r = 0;r<8;r++){
			if(place(c,r)){
				row[c]=r;
				backtracking(c+1);
				}
			}
		}
	}
int main(int argc, char **argv)
{
	int k,tc=1;
	while(cin>>k){
		MIN = 100;
        v.clear();
		v.push_back(k-1);
		for(int i = 0;i<7;i++){
			cin>>k;
			v.push_back(k-1);
			}
			for(auto cell : v)cout<<cell<<" ";
			cout<<endl;
		backtracking(0);
		printf("Case %d: %d\n",tc++,MIN);
		}
	return 0;
}
{%endhighlight%}