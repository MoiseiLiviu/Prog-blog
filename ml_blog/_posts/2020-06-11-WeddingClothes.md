---
title: 11450 - Wedding shopping
layout: post
statement: One of our best friends is getting married and weall are nervous because he is the first of us who is doing something similar. In fact, we have never assisted to a wedding, so we have no clothes or accessories, and to solve the problem we are going to a famous department store of our city to buy all we need :a shirt, a belt, some shoes, a tie, etcetera.We are offered different models for each class of garment (for example, three shirts, two belts,four shoes, ...). We have to buy one model of each class of garment, and just one.As our budget is limited, we cannot spend more money than it, but we want to spend the maximum possible. It's possible that we cannot buy one model of each class of garment due to the short amountof money we have.
input: The first line of the input contains an integer,N, indicating the number of test cases. For each test case,some lines appear, the first one contains two integers,M and C, separated by blanks (1 <= M <= 200,and 1 <= C <= 20), where M is the available amount of money and C is the number of garments you have to buy. Following this line, there are C lines, each one with some integers separated by blanks; in each of these lines the first integer,K(1 <= K <= 20), indicates the number of different models for each garment and it is followed by K integers indicating the price of each model of that garment.
Output: For each test case, the output should consist of one integer indicating the maximum amount of money necessary to buy one element of each garment without exceeding the initial amount of money. If there is no solution, you must print `no solution'.
explanation: Considering that we should pick one element from each garment, to compute every possible combination of clothes we need 20^20 as there can be maximum 20 elements per 20 garments which is way too much.During the complete search there are many overlapping problems :starting from the first garment we should achieve the last one and not run out of money, but during the process of selection we can observe that there are many ways of achieving some gorment i with M money left by picking different elements altoghether.This means that most often we compute the same values again and again, so to stop doing that we should preserve a state, a matrix[money][g].This assures that every possible scenario(money/garment) is computed only once so the worst complexity becomes 200*20=40000.The backtraking part of the problem is simple and requires no explanation, we just return the max amount of money that can be spent if a given element of garment is chosen.
link: https://onlinejudge.org/index.php?option=onlinejudge&page=show_problem&problem=2445
categories: Dynamic_Programming
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

#include <bits/stdc++.h>
using namespace std;

int M,C,N,memo[210][25],
        price[25][25];

int backtracking(int money,int g){
	
	if(money<0)return -1000000;
	else if(g==C)return M-money;
	else if(memo[money][g]!=-1)return memo[money][g];
	else{
		int ans = -1;
		for(auto i = 1;i<=price[g][0];i++){
			ans = max(ans,backtracking(money-price[g][i],g+1));
			}
			return memo[money][g] = ans;
		}
	}

int main(int argc, char **argv)
{
	cin>>N;
	while(N--){
		cin>>M>>C;
		for(int i = 0;i<C;i++){
			cin>>price[i][0];
			for(int j = 1;j<=price[i][0];j++){
				cin>>price[i][j];
				}
			}
			memset(memo,-1,sizeof memo);
			int score = backtracking(M,0);
			if(score<0)cout<<"no solution"<<endl;
			else cout<<score<<endl;
		}
	
	return 0;
}
{%endhighlight%}
