![img](https://www.codingireland.ie/images/fields/GIF/artificial-intelligence.gif)
# Day 1
### Q1. 
The following facts are given for a particular family tree:

```prolog
parent (pam, bob).
parent (tom, bob).
parent (tom, liz).
parent (bob, pat).
parent (bob, ann).
parent (pat, jim).
man(bob).
man(tom).
man(jim).
woman(pam).
woman(ann).
woman(liz).
```
 1. Now formulate the relations GRANDPARENT (X,Y) & SUCCESSOR (X,Y) to find out 
who is the grandparent of whom?& who is the successor of whom respectively?
2. Formulate the SIBLINGS(X, Y) relation
#### Code

```prolog
parent(pam, bob).
parent(tom, bob). 
parent(tom, liz). 
parent(bob, pat). 
parent(bob, ann). 
parent(pat, jim).

man(bob).
man(tom).
man(jim). 
woman(pam). 
woman(ann). 
woman(liz).

grandparent(X, Y) :- parent(X, Z), parent(Z, Y).
successor(X, Y) :- parent(Y, X).

sibling(X,Y):-parent(Z,X),parent(Z,Y),X\==Y.
%what is relation between jim and liz
```
### Q2.
A person may steal Y if X is a thief, X is a man, X likes Y & Y is valuable. Given the following facts, define a predicate steal(X,Y) & determines who steals what?
```
man(john).
woman(mary).
valuable(gold).
likes(john, gold).
likes(john, mary).
thief(john).
thief(mary).
```
#### Code
```prolog
man(john). 
woman(mary). 
valuable(gold). 
likes(john, gold). 
likes(john, mary). 
thief(john). 
thief(mary).

steal(X,Y):-thief(X),man(X),likes(X,Y),valuable(Y).
```
# Day 2
### Q1.
Write a prolog program to find the maximum of 3 numbers
#### Code
```prolog
max_of_three(A, B, C, Max) :-
    A >= B,
    A >= C,
    Max is A.

max_of_three(A, B, C, Max) :-
    B >= A,
    B >= C,
    Max is B.

max_of_three(A, B, C, Max) :-
    C >= A,
    C >= B,
    Max is C.
```
### Q2.
Write a prolog program to find the factorial of a number
#### Code
```prolog
factorial(0, 1).
factorial(N, Result) :-
    N > 0,
    N1 is N - 1,
    factorial(N1, SubResult),
    Result is N * SubResult.
```
### Q3.
Write a prolog program to find the nth Fibonacci term
#### Code
```prolog
fibonacci(0, 0).
fibonacci(1, 1).
fibonacci(N, Result) :-
  N > 1,
  N1 is N - 1,
  N2 is N - 2,
  fibonacci(N1, F1),
  fibonacci(N2, F2),
  Result is F1 + F2.
```
### Q4.
Write a prolog program to find the sum of first N natural numbers
#### Code
```prolog
firstn(0,0).
firstn(N,Result):-
	N > 0,
	N1 is N-1,
	firstn(N1,Subres),
	Result is N + Subres.
```
### Q5.
Write a prolog program to find whether a number is odd or even.

#### Code
```prolog
fun(0, Num) :-
    Num = 0.

fun(A, Num) :-
    A > 0,
    A mod 2 =:= 0,
    Num = even.

fun(A, Num) :-
    A > 0,
    A mod 2 =\= 0,
    Num = odd.
```
# Day 3
### Q1.
Write a prolog program to find the cube of various numbers. The process will stop when the user wants to do. 
#### Code
```prolog
cube_program :-
    write('Enter a number or type "stop" to exit: '),
    read(Input),
    cube_handler(Input).

cube_handler(stop) :-
    write('Program stopped. Goodbye!').

cube_handler(Numbe) :-
    cube(Numbe, Cube),
    write('Cube of '), write(Numbe), write(' is '), write(Cube), nl,
    cube_program.

cube(Numbe, Cube) :-
    Cube is Numbe * Numbe * Numbe.
```
### Q2.
Write a prolog program to design a login module which asks user his login name followed by password. If password is not correct, it keeps on asking till correct password is given.
#### Code
```prolog
user_credential(victor,pass123).
user_credential(peter,wonder789).
user_credential(keran,commands111).

login:-
	write('Login Name: '),
	read(Name),
	write('Password: '),
	read(Password),
	nl,
	authentication(Name,Password).
authentication(Name,Password):-
	user_credential(Name,CorrectPass),
	Password=CorrectPass,
	write('Login Successful! Welcome '),write(Name).
authentication(_,_):-
	write('Invalid Credentials! Please try again...'),nl,
	login.
```
# Day 4
### Q1.
Write a Prolog program to find the length of a given list.
#### Code
```prolog
list_len([], 0).
list_len([_|Tail], Length) :-
    list_len(Tail, Length1),
    Length is Length1 + 1.
```
### Q2.
Write a Prolog program to find the sum of all numbers in a given list.
#### Code
```prolog
list_sum([],0).
list_sum([Head|Tail],Sum):-
	list_sum(Tail,Sum1),
	Sum is Head+Sum1.
```
### Q3.
Write a Prolog program to find the average of N numbers
#### Code
```prolog
list_avg([],0).
list_avg(Number, Average) :-
    sum_list(Number, Sum),
    length(Number, Length),
    Length > 0,
    Average is Sum / Length.
```
# Day 5
### Q1.
Write a Prolog program to find the number of vowels in a given list
#### Code
```prolog
vowel(a).
vowel(e).
vowel(i).
vowel(o).
vowel(u).
vowel_count([],0).
vowel_count([H|T],Count):-
	vowel(H),
	vowel_count(T,Count1),
	Count is 1 + Count1.

vowel_count([H|T],Count):-
	\+ vowel(H),
	vowel_count(T,Count).
```
### Q2.
Write a Prolog program to find the maximum of N numbers
#### Code
```prolog
num_max([X],X).
num_max([H|T],Max):-
	num_max(T,Num),
	(H >= Num -> Max=H ; Max=Num).
```
### Q3.
Write a Prolog program to print the sum of all odd numbers and even numbers from a given list.
#### Code
```prolog
odd_even([],0,0).
odd_even([H|T],Odd,Even):-
	odd_even(T,TailOdd,TailEven),
	(H mod 2 =:= 0-> Even is H+TailEven,Odd=TailOdd;
    Even=TailEven,Odd is TailOdd + H).
```
# Day 6
### Q1.
Write a Prolog program to concatenate two given lists
#### Code
```prolog
concat([], L, L).
concat([X|L1], L2, [X|L3]) :- concat(L1, L2, L3).
```
### Q2.
Write a Prolog program to check whether a given list is ordered or not
#### Code
```prolog
ordered([]).
ordered([_]).
ordered([X,Y|Rest]) :- X =< Y, ordered([Y|Rest]).
```
### Q3.
Write a Prolog program to find the GCD of a set of elements
#### Code
```prolog
gcd(A, B, Result) :- B = 0, Result = A.
gcd(A, B, Result) :- R is A mod B, gcd(B, R, Result).

gcd_set([], Result) :- Result = 0.
gcd_set([X|[]], Result) :- Result = X.
gcd_set([X,Y|Rest], Result) :- gcd(X, Y, G), gcd_set([G|Rest], Result).
```
# Day 7
### Q1.
Define a relation Split which splits a list into 2 sub lists, one of them contains all the positive elements (including 0) in the original list, and the second one contains thenegative elements. (Do it using CUT).
```prolog
```
### Q2.
Write a Prolog program to find the length of a list using Accumulator.
```prolog
```
### Q3.
Write a Prolog program to find the sum of all the numbers of a list using Accumulator.
```prolog
```
### Q4.
Write a Prolog program to find the factorial of a number using Accumulator.
```prolog
```
