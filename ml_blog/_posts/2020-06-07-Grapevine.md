---
title: 12192 - Grapevine
layout: post
statement: In Quadradonia, all rural properties are square, all have the same area, all are perfectly  at and all have the sides aligned to the North-South and West-East axes.Since properties are  at, the hills in Quadradonia look like a series of huge stairs' steps, with different heights. In a certain mountain, an interesting situation occurs in a rectangular area of NXM properties.Starting from anywhere within the region, traversing it in the West to East direction, the properties have non-descending heights. Similarly, traversing that region in the North to South direction, starting from anywhere, the properties have also non-descending heights.A large wine company in Quadradonia wants to rent some properties from that region to grow winegrapes. The company is interested in some special varieties of wine grapes, which are productive only if grown in properties whose heights are within a certain interval. That is, the company is interested in renting properties whose heights are equal to or higher than a given altitude L, and equal to or lower than a given altitude U. To make it easier for harvesting, the rented properties must form a contiguous area. And since everyone in Quadradonia likes squares, the area to be rented must have the shape of a square.The company has not yet decided which variety of grapes it will grow, and therefore it has a list of queries involving intervals, one for each grape variety. The figure below shows an area of interest of dimensions 4X5 (in number of properties) with examples of areas the company could rent to growgrapes in heights within the intervals given in the picture.You must write a program that, given the description of the rectangular area   of interest in the mountain, and a list of queries containing height intervals, determines, for each query, the largest side,in number of properties, of a contiguous square area with heights within the specified interval.
input: The input contains several test cases. The  rst line of a test case contains two integers N and M,separated by a single space, representing respectively the number of properties in the North-South direction (1 <= N <= 500) and the number of properties in the West-East direction (1 <= M <= 500) of the region of interest. Each of the next N lines contains M integers H i;j, separated by single spaces,indicating the heights of the properties in the region of interest . The next line contains an integerQindicatingthe number of queries (1 <= Q <= 10^4). Each of the next Q lines describes a query, and contains two integers Land U, separated by a single space, indicating one interval of heights (0 < L <= U <105).The heights of properties to be rented must be greater than or equal to L and less than or equal to U.The last test case is followed by a line containing two zeros separated by a single space.
Output: For each test case in the input your program must print Q+1 lines. Each of the firstQlines must contain a single integer, indicating the largest side, in number of properties, of a contiguous square area with heights within the interval specified in the respective input query. The last line to be printed for each test case is used as a separator and must contain a single character `-' (known as hyphen or minus sign).
explanation: We need to iterate over all rows and find the smallest number that is bigger than the lower bound from the query, from there we just iterate diagonally over the numbers as we are building a square, if the current number is bigger than the upper bound or we got out the grid bounds -> break out of the loop, if not increase the biggest size.
link: https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&category=0&problem=3344&mosmsg=Submission+received+with+ID+25115193
categories: Binary_search
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

#include <bits/stdc++.h>
using namespace std;

int main(int argc, char **argv)
{
	int n,m,q;
	while(cin>>n>>m&&m&&n){
		int arr[n+1][m+1];
		for(int i = 0;i<n;i++){
			for(int j = 0;j<m;j++){
				cin>>arr[i][j];
				}
			}
			cin>>q;
			while(q--){
				int lower,upper;
				cin>>lower>>upper;
				int bestSize = 0;
				for(int i = 0;i<n;i++){
					int *p = lower_bound(arr[i],arr[i]+m,lower);
					if(p!=arr[i]+m){
						int k;
						for(k = bestSize;k<n;k++){
							if(i+k>n-1||p-arr[i]+k>m-1||arr[i+k][p-arr[i]+k]>upper)break;
							}
							bestSize = max(bestSize,k);
						}
					}
					cout<<bestSize<<endl;
				}
				cout<<"-"<<endl;
		}
	
	return 0;
}
{%endhighlight%}