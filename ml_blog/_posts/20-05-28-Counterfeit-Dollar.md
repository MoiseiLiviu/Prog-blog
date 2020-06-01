---
layout: post
title: Uva 608 Counterfeit Dollar
categories: Simulation
explanation: It's a tricky problem, but the solution is pretty trivial, we just simulate the process and the logic.For that we must come with an assumption for each coin given,if it's either heavy or light, suposse the coin is light and it's found in the left side first time then the left side is lighter and it must be up, in the second case it's in the right side so the ride side is up.It's a simple logical assumption that should be true for all the 3 cases if it's false at some point then the coin is normal and if the coin is found in a even case,it is again a normal coin, but if it goes through all the tests it is indeed conterfeit.
statement: Sally Jones has a dozen Voyageur silver dollars. However, only eleven of the coins are true silverdollars; one coin is counterfeit even though its color and size make it indistinguishable from the realsilver dollars. The counterfeit coin has a different weight from the other coins but Sally does not knowif it is heavier or lighter than the real coins.Happily, Sally has a friend who loans her a very accurate balance scale. The friend will permit Sallythree weighings to find the counterfeit coin. For instance, if Sally weighs two coins against each otherand the scales balance then she knows these two coins are true. Now if Sally weighs one of the truecoins against a third coin and the scales do not balance then Sally knows the third coin is counterfeitand she can tell whether it is light or heavy depending on whether the balance on which it is placedgoes up or down, respectively.By choosing her weighings carefully, Sally is able to ensure that she will find the counterfeit coinwith exactly three weighings.
input: The first line of input is an integern(n>0) specifying the number of cases to follow. Each caseconsists of three lines of input, one for each weighing. Sally has identified each of the coins with thelettersA–L. Information on a weighing will be given by two strings of letters and then one of the words“up”, “down”, or “even”. The first string of letters will represent the coins on the left balance; thesecond string, the coins on the right balance. (Sally will always place the same number of coins on theright balance as on the left balance.) The word in the third position will tell whether the right side ofthe balance goes up, down, or remains even.
Output: For each case, the output will identify the counterfeit coin by its letter and tell whether it is heavy orlight. The solution will always be uniquely determined.
link: https://onlinejudge.org/index.php?option=onlinejudge&page=show_problem&problem=549
---


<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}
#include <bits/stdc++.h>


using namespace std;

string measure[3][3];
int EVEN = 1,
    LIGHT = -50,
    HEAVY = 50;

bool isBalanced(char ch,bool isHeavy){
	int leftWeight,rightWeight;
	for(int i = 0;i<3;i++){
		leftWeight = rightWeight = 0;
	    for(const char k: measure[i][0]){
			if(k==ch)leftWeight += (isHeavy?HEAVY:LIGHT);
			}
		for(const char k:measure[i][1]){
			if(k==ch)rightWeight+=(isHeavy?HEAVY:LIGHT);
			}
		if(measure[i][2]=="even"){
			if(leftWeight!=rightWeight)return false;
			}
		else if(measure[i][2]=="up"){
			if(leftWeight<=rightWeight)return false;
			}
		else{
			if(leftWeight>=rightWeight)return false;
			}
	}
	return true;
}

int main(int argc, char **argv)
{
	for(int i = 0;i<3;i++){
		for(int j=0;j<3;j++){
			cin>>measure[i][j];
			}
		}
	for(char c = 'A';c<='L';c++){
		if(isBalanced(c,true)){
			printf("Coin %c is heavier\n",c);
			}
		if(isBalanced(c,false)){
			printf("Coin %c is lighter\n",c);
			}
		}
		return 0;

	}
{%endhighlight%}
