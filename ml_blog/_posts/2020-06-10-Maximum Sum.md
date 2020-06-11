---
title: 108 - Maximum Sum
layout: post
statement: A problem that is simple to solve in one dimension is often much more difficult to solve in more than one dimension.  Consider satisfying a boolean expression in conjunctive normal form in which each conjunct consists of exactly 3 disjuncts. This problem (3-SAT) is NP-complete. The problem 2-SAT is solved quite efficiently, however.  In contrast, some problems belong to the same complexity class regardless of the dimensionality of the problem.Given a 2-dimensional array of positive and negative integers, find the subrectangle with the largest sum. The sum of a rectangle is the sum of all the elements in that rectangle. In this problem the subrectangle with the largest sum is referred to as the maximal subrectangle.A subrectangle is any contiguous subarray of size 1X1 or greater located within the whole array.
input: The input consists of an NXN array of integers.The input begins with a single positive integer N on a line by itself indicating the size of the square two dimensional array. This is followed by N^2 integers separated by white-space (newlines and spaces).These N^2 integers make up the array in row-major order (i.e., all numbers on the first row, left-to-right,then all numbers on the second row, left-to-right, etc.).N may be as large as 100. The numbers in the array will be in the range[127;127].
Output: The output is the sum of the maximal sub-rectangle.
explanation: My first idea for solving this problem was a Complete Search algorithm which would take every possible starting index(top-left corner of the subrectangle) and every possible ending index for them(bottom-right corner) and sum all the cell inside the area which would give a n^6 (n^2 for computing the starting index * n^2 for every ending index * n^2 to iterate over the entire area) which considering the max value of n=100 is too slow,the DP solution though runs in n^4 which is feasible.Instead of storing the value of the cell A[i,j] in the matrix while reading the input i stored the sum of the cells from (0,0) to (i,j).to do that add the subrectangle A[i-1,j] and A[i,j-1] if both i and j >0 then A[i,j]-=A[i-1,j-1] because the added subrectangles overlap in this area.After computing this matrix, to find out the area of a subrectangle we just substract from the area of A[k,l] where (k,l) are the coordinates of the right bot corner the subrectangle A[i-1][l] and subrectangle A[k][j-1] thus croping out this subrectangle from the preprocessed cumulative matrix.
link: https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=44
categories: Dynamic_Programming
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}
#include <bits/stdc++.h>
using namespace std;

int N;

int main(int argc, char **argv)
{
	cin>>N;
	int A[N+1][N+1];
	for(int i  = 0;i<N;i++){
		for(int j = 0;j<N;j++){
			cin>>A[i][j];
			if(i>0)A[i][j]+=A[i-1][j];
			if(j>0)A[i][j]+=A[i][j-1];
			if(j>0&&i>0)A[i][j]-=A[i-1][j-1];
			}
		}
		int maxSubRect = 127*100*100;
		for(int i = 0;i<N;i++){
			for(int j = 0;j<N;j++){
				for(int k = i;k<N;k++){
					for(int l = j;l<N;l++){
						int subRect = A[k][l];
						if(i>0)subRect-=A[i-1][j];
						if(j>0)subRect-=A[i][j];
						if(i>0&&j>0)subRect+=A[i-1][j-1];
						maxSubRect=max(maxSubRect,subRect);
						}
					}
				}
			}
			cout<<maxSubRect<<endl;
	return 0;
}
{%endhighlight%}

