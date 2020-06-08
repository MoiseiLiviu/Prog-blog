---
title: 410 - Station Balance
layout: post
statement: The International Space Station contains many centrifuges in its labs. Each centrifuge will have some number (C) of chambers each of which can contain 0, 1, or 2 specimens. You are to write a program which assigns all S specimens to the chambers such that no chamber contains more than 2 specimens and the following expression for IMBALANCE is minimized.IMBALANCE=C∑i=1jCMi/AMj where:CMi is the Chamber Mass of chamber i and is computed by summing the masses of the specimens assigned to chamber i.AMi s the Average Mass of the chambers and is computed by dividing the sum of the masses of all specimens by the number of chambers (C).
input: Input to this program will be a file with multiple sets of input. The first line of each set will containtwo numbers. The first number (1 <= C <= 5) defines the number of chambers in the centrifuge and the second number (1 <= S <= 2C) defines the number of specimens in the input set. The second line of input will contain S integers representing the masses of the specimens in the set. Each specimen mass will be between 1 and 1000 and will be delimited by the beginning or end of the line and/or one or more blanks.
Output: For each input set, you are to print a line specifying the set number (starting with 1) in the format‘Set \#X where X is the set number.The next C lines will contain the chamber number in column 1, a colon in column number 2, and then the masses of the specimens your program has assigned to that chamber starting in column 4.The masses in your output should be separated by exactly one blank.Your program should then print IMBALANCE =X on a line by itself where X is the computed imbalance of your specimen assignments printed to 5 digits of precision to the right of the decimal.The final line of output for each set should be a blank line. (Follow the sample output format.)
explanation: Classical load balancing problem, which can be solved in a greedy manner.We know that there can be at most 2 specimens inside a chamber, this means that we can create a vector of size 2*c and after reading the weights of s specimens we just fill with zeroes the rest of the free spaces.Then we sort the resulting vector and at last we pair the elements at the same distance from the closest extremities 0 with n, 1 with n-1 and so on, this way we can combine the elements so that the imbalance is minimal.We need to iterate over c elements from the vector and output the coresponding pair for them, if it is zero we output nothing.
link: https://onlinejudge.org/index.php?option=onlinejudge&Itemid=8&page=show_problem&problem=351
categories: Greedy
---

<span style='font-size:20px;font-weight:bold'>My code:</span>

{%highlight c++ linenos%}
{%endhighlight%}

