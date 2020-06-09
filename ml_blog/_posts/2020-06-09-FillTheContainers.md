---
title: 11413 - Fill the Containers
layout: post
statement: A conveyor belt has a number of vessels of different capacities each filled to brim with milk. The milk from conveyor belt is to be filled into `m' containers. The constraints are :•Whenever milk from a vessel is poured into a container, the milk in the vessel must be completely poured into that container only. That is milk from same vessel can not be poured into different containers.•The milk from the vessel must be poured into the container in order which they appear in the conveyor belt. That is, you cannot randomly pick up a vessel from the conveyor belt and fill the container.•The i th container must be filled with milk only from those vessels that appear earlier to those that fill j th container, for all i < j.Given the number of containers `m', you have to fill the containers with milk from all the vessels,without leaving any milk in the vessel. The containers need not necessarily have same capacity. You are given the liberty to assign any possible capacities to them. Your job is to find out the minimal possible capacity of the container which has maximal capacity. (If this sounds confusing, read down for more explanations.)
input: A single test case consist of 2 lines. The first line specifies 1 <= n <= 1000 the number of vessels in the conveyor belt and then `m' which specifies the number of containers to which, you have to transfer the milk. (1 <= m <= 1000000). The next line contains, the capacity 1 <= c <= 1000000 of each vessel in order wich they appear in the conveyor belt. Note that, milk is filled to the brim of any vessel. So the capacity of the vessel is equal to the amount of milk in it. There are several test cases terminated by EOF.
Output: For each test case, print the minimal possible capacity of the container with maximal capacity. That is there exists a maximal capacity of the containers, below which you can not fill the containers without increasing the number of containers. You have to find such capacity and print it on a single line.Explanation of the output:Here you are given 3 vessels at your disposal, for which you are free to assign the capacity. You can transfer,f1 2 3g to the first container,f4g to the second,f5g to third. Here the maximal capacity of the container is the first one which has a capacity of 6. Note that this is optimal too. That is, you cannot have the maximal container, have a capacity, less than 6 and still use 3 containers only and fill the containers with all milk.For the second one, the optimal way is,f4 7 8g into the first container, and f9g to the second container. So the minimal value of the maximal capacity is 82. Note that f4g to first container and f78 9g to the second is not optimal as, there exists a way to have an assignement of maximal capacity to 82, as opposed to 87 in this case.
explanation: I solved the problem by binary searching the answer, by taking possible values from the input range 1 <= c <= 10^6 and checking if they meet the requirements.Binary search allows doing that in log n time so in this case it would require less than 25 iterations for each case and for each of those it would require N iterations over all the milk vessels to check if it's enough or not.Testing a capacity is done by adding all the milk vessels capacities gradually until it is more or equal than the tested capacity, if it is create a new container and continue the process.After the for loop is done we get the minimum number of containers required with that max capacity.If it is smaller than the given number from the input, try to minimize the capacity by setting the upper bound of the new allowed range to the mid of the old one and check the number of containers for the mid of the new range.Doing that 30+ time assures us that we get the correct answer.
link: https://onlinejudge.org/index.php?option=onlinejudge&page=show_problem&problem=2408
categories: Binary_search
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

#include <bits/stdc++.h>

using namespace std;

vector<int> v;
int n,m;

bool isViable(int capacity){
	    
	    int temp = 0,cnt = 1;
		for(auto cell : v){
			if(cell>capacity)return false;
			if(temp+cell>capacity){
				cnt++;
				temp = cell;
				}
			else temp+=cell;
			}
			if(cnt>m)return false;
			else return true;
		}
	
int binarySearch(){
	
	int lo = 1,hi = 1000000,mid,ans = 0;
	for(int i = 0;i<100;i++){
		mid = (lo+hi)/2;
		if(isViable(mid)){
			ans = mid;
			hi = mid;
			}
		else lo = mid;
		}
		return ans;
	}

int main(int argc, char **argv)
{
	while(cin>>n>>m){
		v.clear();
		for(int i = 0;i<n;i++){
			int k ;
			cin>>k;
			v.push_back(k);
			}
		cout<<binarySearch()<<endl;
		}
	return 0;
}
{%endhighlight%}

