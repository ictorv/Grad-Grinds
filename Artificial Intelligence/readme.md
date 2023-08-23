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
### Q3. Consider the following facts & rules:
Facts are:  
a) Hardware is easy course    
b) Books for hardware are available  
c) Logic is not easy course   
d) Graphics is easy course  
e) Graphics has 8 credits   
f) Graphics has a lab component  
g) Books for Database are available   
h) Mary takes compiler  
Rules are:  
Rule1: X takes Y, if Y is easy course and books for Y are available  
Rule2: X takes Y, if Y has 8 credits and Y has lab component

Write Prolog Program to answer the following queries:
1. Does Mary take graphics course?
2. Which courses Mary take?
3. Who takes Graphics course?

```prolog
takes(X,Y):-
    student(X),
    easy(Y),
    books(Y);
    student(X),
    credits(Y,8),
    lab(Y).
takes(john,compiler).
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

### Q4.
Write a Prolog program to check whether a given element is a member of a given list
#### Code
```prolog
mem(X,[X|_]).
mem(X,[_|T]):-
    mem(X,T).
```
### Q5.
Write a Prolog Program to check whether the given list represents a set or not
#### Code
```prolog 
ordered([X]).
ordered([Head|[Head1|Tail]]) :-
    Head <= Head1,
    ordered([Head1|Tail]).
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
### Q4.
Write a Prolog program to insert an element at the Kth position of a given list

### Code
```prolog
ins(E,1,L,[E|L]).
ins(E,Pos,[X|L],[X|L1]):-
    Pos>1,
    P1 is Pos-1,
    insert(E,P1,L,L1).
```
### Q5.
Write a Prolog Program to remove duplicates from a list.

### Code
```prolog
dup([],[]).
dup([X|T],R):-member(X,T), dup(T,R).
dup([X|T],[X|T1]):-not(member(X,T)),dup(T,T1).
```
### Q6.
Write a Prolog program to delete an element of a list

### Code

```prolog
delE(H,[H|L],L).
delE(E,[X|L],[X|L1]):- 
    delE(E,L,L1).
```
### Q7.
Write a Prolog program to delete an element from the Kth position of a list

### Code

```prolog
delPos(1,[H|L],L).
delPos(K,[X|L],[X|L1]):-
    K>1,
    K1 is K-1, 
    delPos(K1,L,L1).
```
### Q8.
Write a Prolog program to sum only positive numbers of a list
### Code
```prolog
sumPos([],0).
sumPos([H|T],S):-
    H>0,
    sum1(T,S1),
    S is S1+H.
sumPos([H|T],S):-
    H=<0,
    sumPos(T,S).
```

### Q9.
Write a Prolog program to check whether a given list is ordered or not
### Code
```prolog
ordered([]).
ordered([_]).
ordered([X, Y | Rest]) :-
    X =< Y,
    ordered([Y | Rest]).
```
### Q10.
Write a Prolog program to find the last & last-but-one element of a list
### Code
```prolog
last([E]):-write(E).
last([H|L]):-last(L).
last([E,_]):-write(E). 
last([H|L]):-last(L).
```

### Q11.
Write a Prolog program to find the sum of the squares of the elements of a list
### Code
```prolog
sumsq([], 0).
sumsq([X | Rest], Sum) :-
    sumsq(Rest, RestSum),
    Sum is RestSum + X * X.
```
### Q12.
Write a Prolog Program to check whether a given list is Palindrome or not.

```prolog
palin(L1):-
    rev1(L1,[],L2),
    comp(L1,L2).
rev1([],L1,L1).
rev1([X|T],L1,L2):-
    rev1(T,[X|L1],L2).
comp([],[]):-
    writeln('List is Palindrome').
comp([X|L1],[X|L2]):-
    comp(L1,L2).
comp([X|L1],[Y|L2]):-
    writeln('List is not Palindrome').
```
### Q13.
Write a Prolog Program to find the permutation of N elements present in a list

### Code
```prolog
per([],[]).
per([X|L],P):-
    per(L,P1),
    add(X,P1,P).
add(X,L,[X|L]).
add(X,[L|H],[L|H1]):-
    add(X,H,H1).
```
# Day 7.
### Q1.
A. if X<3, Y=0  
B. if X>=3 & X<6, Y=2  
C. if X>6, Y=4  

### Code
```prolog
f(X,0):-
    X<3,!.
f(X,2):-
    X>=3, X<6,!.
f(X,4).
```

### Q2.
Write a Prolog program to implement syntax checker of identifier of a programming language.   

% atom_chars(S,L).convert word S to list L.  
% char_type(X,alpha) or char_type(X,digit)  
``` 
<identifier>::<letter><rest>   
<rest>::<optional_underscore><letter|digit><rest>  
<optional_underscore>::'_'.  
<letter or digit>::<letter>|<digit>  
```
### Code
```prolog
isLetter(H):-
    char_type(H,alpha).
isDigit(H):-
    char_type(H,digit).
underscore(H):-
    H = '_'.
rest([]).
rest([H,X|T]):-
    (underscore(H),!,(isLetter(X),!;isDigit(X),!)),rest(T).
rest([H|T]):-
    (isLetter(H),!;isDigit(H),!),rest(T).
syntax(X):-
    atom_chars(X,[H|T]),isLetter(H),rest(T).
```
### Q3.
Define a relation Setdiff(Set1, Set2, Result), where all the three sets are represented as lists. Find the Result set that is the difference between Set1 & Set2 using CUT.
```
```
### Q4.
Define a relation Split which splits a list into 2 sub lists, one of them contains all the positive elements (including 0) in the original list, and the second one contains thenegative elements. (Do it using CUT).
### Code
```prolog
sp([H],[H],[]):-H>=0,!.
sp([H],[],[H]).
sp([H|T],[H|T1],T2):-H>0,!,sp(T,T1,T2),!.
sp([H|T],T1,[H|T2]):-sp(T,T1,T2),!.
```
_____________Structured Object_____________
### Q5.
Consider a structured object representing a course, where there is a relationship between 4 objects – a course name, time, a lecturer and a location. Let’s define the following predicates:

```
teacher_course (L,L1,C) – L teachers F. name,L1 L.name,course C
teacher_on_day (L, D, C) – L teachers L.name, course C on day D
duration (C, D):-course C of duration D
```
### Code
```prolog
course(logic,time(monday,9,11),teacher(s,saha),location(ict,b07)).
course(ds,time(friday,2,5),teacher(p,choudhury),location(ict,b12)).
teacher_course(L1,L2,C):-
    course(C,_,teacher(L1,L2),_).
teacher_on_day(L,Day,C):-
    course(C,time(Day,_,_),teacher(_,L),_).
duration(C,D):-
    course(C,time(_,Start,Finish),_,_),D is Finish-Start.
```

Now answer the following queries:  
a) Who teaches the course ‘logic’?     
```
teacher_course(L,L1,logic).
```  

b) Which course does Prof. saha teach?  
```
teacher_course(_,saha,C).
```   

c) Which day does Prof. saha teach the course on ‘Logic’?  
```
teacher_on_day(saha,Day,logic).
```

d) What is the duration of each course?  
```
duration(C,D).
```
### Q6 a).
Write a prolog program to create a binary tree and then print the tree in pre-order, in-order & post-order.
```plaintext
         30
        /  \
      25   60
     /     /
   10     70
```

### Code
```prolog
tree(30,tree(25,tree(10,void,void),void),tree(60,void,tree(70,void,void))).
in_tree(tree(X,L,R),Y):-in_tree(L,L1),in_tree(R,R1),append(L1,[X|R1], Y).
pre_tree(tree(X,L,R),Y):-pre_tree(L,L1),pre_tree(R,R1),append([X|L1],R1,Y).
```

### Q6 b).
Write a program to check whether a given element belongs to the binary tree or not.
### Code
```prolog 
tree(empty, void, void).
tree(node(Value, Left, Right), Left, Right).

belongs_to_tree(Element, tree(node(Element, _, _), _, _)).

belongs_to_tree(Element, tree(node(Value, Left, _), _, _)) :-
    Element < Value,
    belongs_to_tree(Element, Left).

belongs_to_tree(Element, tree(node(Value, _, Right), _, _)) :-
    Element > Value,
    belongs_to_tree(Element, Right).
```
# Day 8
### Q1.
Define a relation Split which splits a list into 2 sub lists, one of them contains all the positive elements (including 0) in the original list, and the second one contains thenegative elements. (Do it using CUT).
```prolog
```
### Q2.
Write a Prolog program to find the length of a list using Accumulator.
### Code
```prolog
% Normal Case
length1([],0).
Length1([X|Y],N):- length1(Y,L1), L is L1+1.

% Using Accumulator
acclength(L,N):-acclength(L,0,N).
acclength([],N,N1):-N1 is N.
acclength([X|Y],L,N):-L1 is L+1,acclength(Y,L1,N).
```
### Q5.
Rewrite the program of reverse of a list using Accumulator
### Code
```prolog
%Normal
rev1([],L1,L1).
rev1([X|T],L1,L2):-rev1(T,[X|L1],L2).

%Using Accumulator
rev1(L,LR):-
    accrev1(L,[],LR).
accrev1([],L,L).
accrev1([X|T],L,LR):-
    accrev1(T,[X|L],LR).
```
### Q3.
Write a Prolog program to find the sum of all the numbers of a list using Accumulator.
```prolog
```
### Q4.
Write a Prolog program to find the factorial of a number using Accumulator.
```prolog
```

### Q5.
Implement Bubble Sort & Insertion Sort using Prolog.
### Code
```prolog
%Bubble Sort
bsort(S,S).
bsort([X|L],L2):-swap([X|L],L3),!,bsort(L3,L2).
swap([X,Y|L],[Y,X|L]):-X>Y.
swap([X|L],[X|L1]):-swap(L,L1).

%Insertion Sort
insertion_sort([], []).
insertion_sort([X | Rest], Sorted) :-
    insertion_sort(Rest, SortedRest),
    insert_sorted(X, SortedRest, Sorted).

insert_sorted(X, [], [X]).
insert_sorted(X, [Y | Rest], [X, Y | Rest]) :- X =< Y.
insert_sorted(X, [Y | Rest], [Y | SortedRest]) :- X > Y, insert_sorted(X, Rest, SortedRest).
```
# Day 9
Write a Prolog Program to implement DFS & BFS
```prolog
```

# Day 10
### Q1. 
Problem: A house has six rooms & eight doors as shown in the figure below. Only room 6 has a telephone. A person is standing at position ‘entry’. He wants to reach to the telephone after going through a number of doors. Write a Prolog program to find out all the sequences according to which he should traverse the rooms along with their cost.
![Alt text](image.png)

### Code
```prolog
door(a,b).
door(b,c).
door(c,b).
door(c,d).
door(d,c).
door(b,e).
door(e,b).
door(d,e).
door(e,d).
door(d,f).
door(e,g).
door(g,e).
door(g,f).
phone(f).
mem(X,[X|_]).
mem(X,[_|T]):-mem(X,T).
path(L,R,C):-dfs(L,[L],R,0,C).
dfs(L,V,R,C1,C):-(phone(L),dfs(V,R,C1,C));(door(L,F),not(mem(F,V)),C2 is
C1+1,dfs(F,[F|V],R,C2,C)).
dfs(N,N,C,C).
```
### Q2.
Email is out of order at St. Mary's College and the teacher wants to tell Robert
something urgent. The teacher meets Craig and asks him to tell Robert she wants to speak
with him. Craig says that if he meets Robert its OK, but else he will send the message to
everyone he meets and the message will go further. Each student tells each student he
meets that the teacher waits for Robert in her office.
The students meet each other (we don't know in what order):
1) Craig meets John and Jason
2) Jason meets Kiki and Adam and David
3) Adam meets Scott and Jeremy
4) Jeremy meets John and Scott
5) Kiki meets Chris
6) Chris meets David and Adam
7) David meets Robert
Do you think the teacher will wait forever in her office? Display all the possible paths from Craig to Robert.
 ### Code
 ```prolog
 % Graph representation
edge(craig, [john, jason]).
edge(jason, [kiki, adam, david]).
edge(adam, [scott, jeremy]).
edge(jeremy, [john, scott]).
edge(kiki, [chris]).
edge(chris, [david, adam]).
edge(david, [robert]).

% Recursive path finding
find_path(Start, End, Path) :-
    find_path(Start, End, [Start], Path).

find_path(End, End, Path, Path).
find_path(Current, End, Visited, Path) :-
    edge(Current, Neighbors),
    member(Next, Neighbors),
    not(member(Next, Visited)),
    find_path(Next, End, [Next | Visited], Path).

% Find all paths from Craig to Robert
find_all_paths(Craig, Robert, Paths) :-
    findall(Path, find_path(Craig, Robert, Path), Paths).

% Display paths
display_paths([]).
display_paths([Path | Paths]) :-
    print_path(Path), nl,
    display_paths(Paths).

print_path([]).
print_path([X]) :- write(X), !.
print_path([X | Rest]) :- write(X), write(' -> '), print_path(Rest).

 ```

# Day 10
### Q1.
Write a Prolog Program to solve 8-queen problem (The objective is toplace eight queens on a chessboard so that no two queens are attackingeach other; i.e., no two queens are in the same row, the same column, or on the same diagonal. We generalize this original problem by allowing for an arbitrary dimension N of the chessboard.)

### Code
```prolog
% We represent the positions of the queens as a list of numbers 1..N.
% Example: [4,2,7,3,6,8,5,1] means that the queen in the first column
% is in row 4, the queen in the second column is in row 2, etc.
% By using the permutations of the numbers 1..N we guarantee that
% no two queens are in the same row. The only test that remains
% to be made is the diagonal test. A queen placed at column X and
% row Y occupies two diagonals: one of them, with number C = X-Y, goes
% from bottom-left to top-right, the other one, numbered D = X+Y, goes
% from top-left to bottom-right. In the test predicate we keep track
% of the already occupied diagonals in Cs and Ds.
% queens_1(N,Qs) :- Qs is a solution of the N-queens problem
queens_1(N,Qs):-range(1,N,Rs),permu(Rs,Qs),test(Qs).
% range(A,B,L) :- L is the list of numbers A..B
range(A,A,[A]).
range(A,B,[A|L]):-A<B,A1 is A+1,range(A1,B,L).
% permu(Xs,Zs) :- the list Zs is a permutation of the list Xspermu([],[]).
permu(Qs,[Y|Ys]):-del(Y,Qs,Rs),permu(Rs,Ys).
del(X,[X|Xs],Xs).
del(X,[Y|Ys],[Y|Zs]):-del(X,Ys,Zs).
% test(Qs) :- the list Qs represents a non-attacking queens solution.
% test(Qs,X,Cs,Ds) :- the queens in Qs, representing columns X to N, are not in
% conflict with the diagonals Cs and Ds
test(Qs):-test(Qs,1,[],[]).
test([],_,_,_).
test([Y|Ys],X,Cs,Ds):-C is X-Y,not(mem(C,Cs)),D is X+Y,not(mem(D,Ds)),X1 is
X+1,test(Ys,X1,[C|Cs],[D|Ds]).
%mem(X,T):- check that X memberexists in the list T
mem(X,[X|_]).
mem(X,[_|T]):-mem(X,T).
```
### Q2.
Write a Prolog Program to check whether a given 3x3 matrix is a magic square or not
```
-----    ------
1 5 9     1 5 9
6 7 2     8 3 4
8 3 4     6 7 2
-----     ------
```
### Code
```prolog
mat([H1|T1],[H2|T2],[H3|T3]) :- 
    P is H1+H2+H3,
    mat([H1|T1],[H2|T2],[H3|T3],0,0,0,P,0,[],[],[]).

mat([],[],[],S,S,S,S,S,L1,L2,L3):-
    rev(L1,R1), 
    write(R1),nl,
    rev(L2,R2),
    write(R2),nl,
    rev(L3,R3),
    write(R3).

mat([H1|T1],[H2|T2],[H3|T3],A,B,C,P,N,T4,T5,T6):-
    A1 is A+H1, 
    B1 is B+H2, 
    C1 is C+H3,
    N1 is H1+H2+H3,
    N1=:=P,
    mat(T1,T2,T3,A1,B1,C1,P,N1,[H1|T4],[H2|T5],[H3|T6]).

concat1([],B,B).

concat1([H|T], B, [H|T1]):-
    concat1(T,B,T1).

rev([X],[X]).

rev([H|T],L):-
    rev(T,B1),
    concat1(B1,[H],L).
```
# Day 11
### Q1.
Write a Prolog Program to implement Resolution method to get the resolvent from two given clauses
```
Example:-[not(a),b,c] and [a,not(b),c,d]-> [c,d]
```
### Code
```prolog
mem(X,[X|_]):-!.
mem(X,[_|T]):-
    mem(X,T).

conc([H1|T1],T2,[H1|T3]):-
    conc(T1,T2,T3).

conc([],H2,H2).

conc([],[],[]).

removedupli([],[]).

removedupli([X|T],R):-
    mem(X,T),
    removedupli(T,R),!.

removedupli([X|T],[X|T1]):-
    removedupli(T,T1).

resol([],_,[]).

resol([H1|T1],H2,T3):-
    (mem(not(H1),H2)),
    resol(T1,H2,T3).

resol([not(H1)|T1],H2,T3):-
    mem(H1,H2),
    resol(T1,H2,T3).

resol([H1|T1],H2,[H1|T3]):-
    not(mem(not(H1),H2)),
    resol(T1,H2,T3).

resol([not(H1)|T1],H2,[H1|T3]):-
    not(mem(H1,H2)),
    resol(T1,H2,T3).

input(H1,H2,T1):-
    resol(H1,H2,T2),
    resol(H2,H1,T3),
    conc(T2,T3,T4),
    removedupli(T4,T1),!.
```

# Day 12
### Q1.
Application of some built-in functions in LISP.
```
```

### Q2.
Write a function in LISP to find the square of a given number.
```
```
### Q3.
Write a function in both iterative & recursive way to calculate xy
```
```