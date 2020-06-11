---
title: UVa 507 - Jill Rides Again
layout: post
statement: Jill likes to ride her bicycle, but since the pretty city of Greenhills where she lives has grown, Jill often uses the excellent public bus system for part of her journey. She has a folding bicycle which she carries with her when she uses the bus for the  rst part of her trip. When the bus reaches some pleasant part of the city, Jill gets off and rides her bicycle. She follows the bus route until she reaches her destination or she comes to a part of the city she does not like. In the latter event she will board the bus to finish her trip.Through years of experience, Jill has rated each road on an integer scale of \niceness." Positive niceness values indicate roads Jill likes; negative values are used for roads she does not like. There are not zero values. Jill plans where to leave the bus and start bicycling, as well as where to stop bicycling and re-join the bus, so that the sum of niceness values of the roads she bicycles on is maximized. This means that she will sometimes cycle along a road she does not like, provided that it joins up two other parts of her journey involving roads she likes enough to compensate. It may be that no part of the route is suitable for cycling so that Jill takes the bus for its entire route. Conversely, it may be that the whole route is so nice Jill will not use the bus at all.Since there are many different bus routes, each with several stops at which Jill could leave or enter the bus, she feels that a computer program could help her identify the best part to cycle for each bus route.
input: The input  le contains information on several bus routes. The first line of the  le is a single integer b representing the number of route descriptions in the file.  The identifier for each route (r) is the sequence number within the data file, 1 <= r <= b. Each route description begins with the number of stops on the route :an integers, 2 <= s <= 20;000 on a line by itself. The number of stops is followed by s - 1 lines, each line i(1 <= i < s) is an integer ni representing Jill's assessment of the niceness of the road between the two stops i and i+1.
Output: For each route r in the input file, your program should identify the beginning bus stop i and the ending bus stop j that identify the segment of the route which yields the maximal sum of niceness,m=ni+ni+1+...+nj-1. If more than one segment is maximally nice, choose the one with the longest cycle ride (largest j - i). To break ties in longest maximal segments, choose the segment that begins with the earliest stop (lowest i). For each route r in the input  file, print a line in the form:The nicest part of router is between stops i and j However, if the maximal sum is not positive, your program should print:Route r has no nice parts.
explanation: My idea was to create a var which holds the state of the current range.Starting from the first element of the array, we add the value to the state.If the var becomes negative on the i-th element of the array then there is no point in increasing the range but rather annul the state and start over from the element i+1.Each time the state becomes greater than the max variable, set the start index to the current range first index and the end index to the current index.If the max value and the current state are equal check whoose delta(diff between start and end) is bigger and choose that pair(according to the output indications).
link: https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&category=24&page=show_problem&problem=448
categories: Dynamic_Programming
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

#include <bits/stdc++.h>
using namespace std;

int N,R,tc = 1;

int main(int argc, char **argv)
{
	cin>>N;
	while(N--){
		cin>>R;
		vector<int> stops(R-1);
		for(auto &cell : stops)cin>>cell;
		int start =0,end = R-1,counter = 0,max = -1,currStart=0;
		for(int i = 0;i<R-1;i++){
				counter+=stops[i];
				if(counter<0){
					currStart = i+1;
					counter=0;
					}
				else if(counter>max){
					start = currStart;
					end = i;
					max = counter;
					}
				else if(counter==max){
					if(end-start<i-currStart){
						end=i;
						start = currStart;
						}
					}
				}
                if(max!=0)
				printf("The nicest part of route %d is between stops %d and %d\n",tc++,start+1,end+2);
                else printf("Route %d has no nice parts",tc++);
			}	
	return 0;
}
{%endhighlight%}

