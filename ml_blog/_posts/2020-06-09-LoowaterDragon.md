---
title: 11292 - Dragon of Loowater
layout: post
statement: Once upon a time, in the Kingdom of Loowater, a minor nuisance turned into a major problem.The  shores  of  Rellau Creek in central Loowater had always been a prime breeding ground for geese.Due to the lack of predators,the geese population was out of control.  The people of Loowater mostly kept clear of the geese.  Occasionally,a goose would attack one of the people, and perhaps bite off a finger or two, but in general, the people tolerated the geese as a minor nuisance.One day,  a freak mutation  occurred,  and  one of  the  geese  spawned  amulti-headed   fire-breathing dragon.  When the dragon grew up, he threatened to burn the Kingdom of Loowater to a crisp.Loowater had a major problem. The king was alarmed, and called on his knights to slay the dragon and save the kingdom.The knights explained :\To slay the dragon, we must chop off all its heads. Each knight can chopoff one of the dragon's heads. The heads of the dragon are of different sizes. In order to chop off ahead, a knight must be at least as tall as the diameter of the head. The knights' union demands that for chopping off a head, a knight must be paid a wage equal to one gold coin for each centimetre of the knight's height."Would there be enough knights to defeat the dragon? The king called on his advisors to help him decide how many and which knights to hire. After having lost a lot of money building Mir Park, the king wanted to minimize the expense of slaying the dragon. As one of the advisors, your job was to help the king. You took it very seriously :if you failed, you and the whole kingdom would be burnt to a crisp! 
input: The input contains several test cases. The first line of each test case contains two integers between 1 and 20000 inclusive, indicating the number n of heads that the dragon has, and the number m of knights in the kingdom. The next n lines each contain an integer, and give the diameters of the dragon's heads,in centimetres. The following m lines each contain an integer, and specify the heights of the knights of Loowater, also in centimetres.The last test case is followed by a line containing `0 0'.
Output: For each test case, output a line containing the minimum number of gold coins that the king needs topay to slay the dragon. If it is not possible for the knights of Loowater to slay the dragon, output the line `Loowater is doomed!'.
explanation: My idea was to create 2 vectors, one for the knights height and one for the diameters and then to sort them both.After that to try to pair each diameter with a knight in increasing order of their values, so starting from dragon 0 i start my search from knight 0 and iterate over the knights vector until one with a big enough height is found, add the height to the total sum and go to the next dragon and do the same process starting from the i+1 knight where i is the last chosen knight.At each iteration inside the knights vector i check if there are enough knights remaining to slay all the dragons, if not -> break out of the loop and print 'Loowater is doomed!'.
link: https://onlinejudge.org/index.php?option=onlinejudge&page=show_problem&problem=2267
categories: Greedy
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}

#include <bits/stdc++.h>
using namespace std;

int n,m;

int main(int argc, char **argv)
{
	while((cin>>n>>m)&&n&&m){
		vector<int> v(n);
		vector<int> v1(m);
		for(auto &cell : v)cin>>cell;
		for(auto &cell : v1)cin>>cell;
		if(m<n){
			cout<<"Loowater is doomed!"<<endl;
			continue;
			}
		sort(v.begin(),v.end());
		sort(v1.begin(),v1.end());
		int j=0,ans = 0;bool possible = true;
		for(int i = 0;i<n;i++){
			if(possible)
			for(;j<m;j++){
				if(v1[j]>=v[i]){
					ans+=v1[j];
					j++;
					break;
					}
					if(m-j<=n-i){cout<<"Loowater is doomed!"<<endl;possible= false;break;}
				}
			}
			if(possible)cout<<ans<<endl;
		}
	return 0;
}

{%endhighlight%}

