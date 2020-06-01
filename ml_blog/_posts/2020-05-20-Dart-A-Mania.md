---
layout: post
title: Uva 735 Dart-A-Mania
categories: Brute_force
statement:  In each test case an integer is given.For each positive integer in the input file, 2 or 3 line(s) will be written to the output file.If the score can be reduced to zero, your program should write the lines:NUMBER OF COMBINATIONS THAT SCORESxISc.NUMBER OF PERMUTATIONS THAT SCORESxISp.wherexis the value of the player’s score whilecandpare the total number of combinations andpermutations possible, respectively.If it is impossible to reduce the player’s score to zero, write the line:THE SCORE OFxCANNOT BE MADE WITH THREE DARTS.After the line(s) above are printed, your program should write a line of 70 asterisks to separateoutput for different scores. The message ‘END OF OUTPUT’ should appear at the end of the output file.
input: The input file contains a list of integers (each<999), one per line, that represent several players’current scores. A value of zero or less will signify the end of the input file.
Output: For each positive integer in the input file, 2 or 3 line(s) will be written to the output file.If the score can be reduced to zero, your program should write the lines:NUMBER OF COMBINATIONS THAT SCORESxISc.NUMBER OF PERMUTATIONS THAT SCORESxISp.wherexis the value of the player’s score whilecandpare the total number of combinations andpermutations possible, respectively.If it is impossible to reduce the player’s score to zero, write the line:THE SCORE OFxCANNOT BE MADE WITH THREE DARTS.After the line(s) above are printed, your program should write a line of 70 asterisks to separateoutput for different scores. The message ‘END OF OUTPUT’ should appear at the end of the output file.
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=2026
explanation: Permutations usually mean that we will need to explore all the possible cases for a given input.First we compute all the possible scores, considering the doubles and the triples, so the max score is 60 and the max score for all the 3 darts is 180, this way we can knock some input cases right away.Then we just make 3 nested for loops, each one iterating over the possible scores, and we substract this value from the input, if the result is negative we break out of the loop, if it's 0 we increment the number of permutations and we check if its a unique combination by using a three dimensional bool array.
---

  <span style='font-size:20px;font-weight:bold'>Description:</span>The game of darts has many variations. One such variation is the game of301. In the game of 301 eachplayer starts with a score of 301 (hence the name). Each player, in turn, throws three darts to scorepoints which are subtracted from the player’s current score. For instance, if a player has a current scoreof 272 and scores 55 points with the three darts, the new score would be 217. Each dart that is tossedmay strike regions on the dartboard that are numbered between 1 and 20. (A value of zero indicatesthat the player either missed the dartboard altogether or elected to not throw the dart.) A dart thatstrikes one of these regions will either score the number printed on the dartboard, double the numberprinted, or triple the number printed. For example, a player may score 17, 34, or 51 points with a tossof one dart that hits one of the regions marked with a 17. A third way to score points with one dartis to hit the BULLS EYE which is worth 50 points. (There is no provision for doubling or tripling thebull’s eye score.)The first player to reduce his score toexactly zerowins the game. If a player scores more pointsthan his/her current score, the player is said to have “busted” and the new score is returned to the lastcurrent score.



  <span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

  #include <bits/stdc++.h>
using namespace std;


void setUnique(int i,int j,int l,bool comb[65][65][65]){
	
	comb[i][j][l] = true;
	comb[j][i][l] = true;
	comb[l][j][i] = true;
	comb[l][i][j] = true;
	comb[i][l][j] = true;
	comb[j][l][i] = true;
	}

int main(int argc, char **argv)
{
	
	int k;
	set<int> values;
	values.insert({0,50});
	for(int i = 1;i<=20;i++){
		values.insert({i,i*2,i*3});
		}
	while(cin>>k,k>0){
		bool comb[65][65][65]= {};
		if(k>180){
			printf("THE SCORE OF %d CANNOT BE MADE WITH THREE DARTS",k);
			continue;
			}
		int p = 0,c = 0;
		for(auto i : values){
			if(i>k)break;
			int temp = k-i;
			if(temp==0){
				p++;continue;
				if(!comb[i][0][0]){c++;
				setUnique(i,0,0,comb);}}
			for(auto j : values){
				if(j>temp)break;
				int temp1 = temp - j;
				if(temp1==0){
					p++;continue;
					if(!comb[i][j][0]){
						c++;
						setUnique(i,j,0,comb);}}
				for(auto l : values){
					if(l>temp1)break;
					int temp2 = temp1 - l;
					if(temp2==0){
						p++;
						if(!comb[i][j][l]){
							c++;
							setUnique(i,j,l,comb);}
						}
					}
				}
			}
			if(p==0){
				printf("THE SCORE OF %d CANNOT BE MADE WITH THREE DARTS\n",k);
				for(int i = 0;i<70;i++)cout<<"*";
				cout<<endl;}
			else{
				printf("NUMBER OF COMBINATIONS THAT SCORES %d IS %d\n",k,c);
				printf("NUMBER OF PERMUTATIONS THAT SCORES %d IS %d\n",k,p);
				for(int i = 0;i<70;i++)cout<<"*";
				cout<<endl;
			    }
		}
		cout<<"END OF OUTPUT"<<endl;
	return 0;
}
{%endhighlight%}
