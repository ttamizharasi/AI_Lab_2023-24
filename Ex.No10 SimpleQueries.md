# Ex.No: 10  Logic Programming –  Simple queries from facts and rules
### DATE:                                                                            
### REGISTER NUMBER : 212222040170
### AIM: 
To write a prolog program to find the answer of query. 
###  Algorithm:
 Step 1: Start the program <br> 
 Step 2: Convert the sentence into First order Logic  <br> 
 Step 3:  Convert the sentence into Horn clause form  <br> 
 Step 4: Add rules and predicates in a program   <br> 
 Step 5:  Pass the query to program. <br> 
 Step 6: Prolog interpreter shows the output and return answer. <br> 
 Step 8:  Stop the program.
### Program:
### Task 1:
Construct the FOL representation for the following sentences <br> 
1.	John likes all kinds of food.  <br> 
2.	Apples are food.  <br> 
3.	Chicken is a food.  <br> 
4.	Sue eats everything Bill eats. <br> 
5.	 Bill eats peanuts  <br> 
   Convert into clause form and Prove that John like Apple by using Prolog. <br> 
### Program:
```
likes(john,X):-
	food(X).
eats(bill,X):-
	eats(sue,X).
eats(Y,X):-
	food(X).
eats(bill,peanuts).
food(apple).
food(chicken).
food(peanuts).
```

### Output:

![425414197-ce4e5fd0-3eb6-42e1-aada-5b22422ac26b](https://github.com/user-attachments/assets/7aca183a-781f-4514-9594-25470645f231)


### Task 2:
Consider the following facts and represent them in predicate form: <br>              
1.	Steve likes easy courses. <br> 
2.	Science courses are hard. <br> 
3. All the courses in Have fun department are easy <br> 
4. BK301 is Have fun department course.<br> 
Convert the facts in predicate form to clauses and then prove by resolution: “Steve likes BK301 course”<br> 

### Program:
```
likes(steve, X) :-
 easy_course(X).
hard_course(science).
easy_course(X) :-
 in_department(X, have_fun).
in_department(bk301, have_fun).
```
### Output:

![425414942-9bfb12dc-8c14-4ade-9ccc-b33b2d353714](https://github.com/user-attachments/assets/0b19c818-912c-4f9f-9dc8-3f5ca00be9bc)

### Task 3:
Consider the statement <br> 
“This is a crime for an American to sell weapons to hostile nations. The Nano , enemy of America has some missiles and its missiles were sold it by Colonal West who is an American” <br> 
Convert to Clause form and prove west is criminal by using Prolog.<br> 
### Program:
```
criminal(X):-
	american(X),
	weapon(Y),
	hostile(Z),
	sells(X,Y,Z).
weapon(Y):-
    missile(Y).
hostile(Z):-
    enemy(Z,X).

sells(west,Y,nano):-
	missile(Y),
	owns(nano,Y).

missile(m).
owns(nano,m).
enemy(nano,america).
american(west).
```
### Output:

![425416467-6cbf9c6b-d487-4489-b272-224e56966a67](https://github.com/user-attachments/assets/22a7619a-310d-4073-8735-6afe0d9dcecd)


### Result:
Thus the prolog programs were executed successfully and the answer of query was found.
