---
layout: post
statement: A man used to play dominoes with some friends in a small town. Some families have left the town andat present the only residents in the town are the man and his wife. This man would like to continue playing dominoes, but his wife does not like plaing. He has invented a game to play alone. Two pieces are picked out and are put at the two extremes of a row with a number (n) of spaces. After that, other pieces (m) are picked out to fill the spaces. The number of pieces is greater than or equal to the number of spaces (m < n), and the number of pieces is less than or equal to 14 (m < 14). The spaces are filled by putting one piece in each space, according to the rules of dominoes :the number of adjacent dots on two different dominoes must coincide. Pieces with repeated values are placed in the same way as the other pieces, and not at right angels.The problem consists in the design of a program which, given a number of spaces (n), a number ofpieces (m), the two initial pieces (i1; i2) and (d1; d2), and the m pieces (p1; q1), (p2; q2), . . . , (pm; qm),decides if it is possible to  fill the n spaces between the two initial pieces using the m pieces and withthe rules of dominoes. For example, with n= 3,m= 4, initial pieces (0,1) and (3,4), and pieces (2,1),(5,6), (2,2) and (3,2), the answer is `YES', because there is a solution :(0,1), (1,2), (2,2), (2,3), (3,4).With n= 2,m= 4, pieces in the extremes (0,1) and (3,4), and (1,4), (4,4), (3,2) and (5,6), the answer is `NO'.
input: The input will consist of a series of problems, with each problem described in a series of lines :in the rst line the number of spaces (n) is indicated, in the second line the number of pieces (m) used to  llthe spaces, in the next line the piece to be placed on the left, with the two values in the piece separated by a space and in the same way that the numbers appear in the row, in the following lines the piece tobe placed on the right, with the two values in the piece separated by a space and in the same way thatthe numbers appear in the row, and the other m pieces appear in consecutive lines, one in each line,with the two values separated by a space. Different problems appear in the input successively without separation, and the input  nishes when `0' appears as the number of spaces.
Output: For each problem in the input a line is written, with `YES' if the problem has a solution, and `NO' if ithas no solution.
explanation: The problem is solvable with backtracking.Starting from the left domino piece we iterate over all the possible pieces that can be concatinated and for each of them do the same process until all the n places are filled, at that point we check if the last piece is compatible with the right extreme, if it is then set the 'possible' boolean to true;
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=1444
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

#include <bits/stdc++.h>
using namespace std;

int N;
map<int,vector<int>> adj;
bool possible;
int visited[20][20];

void backtrack(int m,int k,int end){
	
	if(k==N){
		for(auto cell : adj[m]){
			if(cell==end&&!(visited[cell][m]||visited[m][cell]))possible=true;
			}
		}
	else{
		for(auto cell : adj[m]){
			if(visited[m][cell]||visited[cell][m])continue;
			visited[cell][m] = 1;
			backtrack(cell,k+1,end);
			visited[cell][m]=0;
			
			}
		}
	}

int main(int argc, char **argv)
{
	for(int i = 0;i<20;i++){
		for(int j = 0;j<20;j++)visited[i][j]=0;
		}
	int M;
	while(scanf("%d %d",&N,&M)&&N){
		adj.clear();
		possible=false;
		int start1,start2,end1,end2;
		cin>>start1>>start2>>end1>>end2;
		while(M--){
			int k,v;
			cin>>k>>v;
			adj[k].push_back(v);
			adj[v].push_back(k);
			}
		
		backtrack(start2,1,end1);
		cout<<(possible?"YES":"NO")<<endl;
		}
	
	return 0;
}
{%endhighlight%}