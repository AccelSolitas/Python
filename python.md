Note for Python
================

## 1、Number game
### 1.1 escape character
If the type of input is strings, then the strings should be encompassed by *""* or *''*. If the strings conlict to bif, you should add *\* as an escape character right before the conlicting character of your input to escape it from its bif function at a time. Btw *\* can also be the escape character of itself.

### 1.2 raw string
```python
str = 'C:\now'     
print(str)
```   
Which equals
`print('C:\now')`

Because "\n" is a bif，the print will automatically linefeed. If you want the strings function without using escape character, you can also use raw string. Like: `str = r'c:\now'` which equals adding escape characters to every conflicting charater automatically to get rid of conflict.

Notice:1、*“（）”* is unnecessary, 2、it's inhibted to put *"\"* at the end of the strings

### Example 1.1 basic number game
```python
print("Let's play a game!")
number = input("Please enter a random number ranged 1-10:")         #Let users to input strings（Numbers here）
guess = int(number)   #Convert strings to int and assign it to guess
while guess != 6      #Put while at the beginning of loop body,*==* means equal to ,while *!=* means not
    number = input("Please enter a random number ranged 1-10:")
    guess = int(number)   
    if guess == 6:        
      print("Bingo!")
      else:
      if guess > 6:
          print("Wrong number,lower please.")
      else:
          print("Wrong number,higher please")
print("Game Over")
```  
#### *New command*
```python
while <condition> #the loop will kepp going until the condition become False
    <loop body>
```    

The problem of this game is that the first input is only able to assign number to *guess* ,yet can not to do logical judgment. Improved version below:

### Example 1.2 number game plus
```python
print("Let's play a game!")
number = input("Please enter a random number ranged 1-10:")
guess = int(number)
if guess == 6:
    print("Bingo")
else:
    if guess > 6:
        print("Wrong number,lower please.")
        while guess != 6:
            number = input("try again:")
            guess = int(number)   
            if guess == 6:        
                print("Bingo!")
            else:
                if guess > 6:
                    print("Wrong number,lower please.")
                else:
                    print("Wrong number,higher please")
    else:
        print("Wrong number,higher please")
        while guess !=6:
            number = input("try again:")
            guess = int(number)   
            if guess == 6:        
                print("Bingo!")
            else:
                if guess > 6:
                    print("Wrong number,lower please.")
                else:
                    print("Wrong number,higher please")
print("Game Over")
```  

After the improment, it can do both assignment and logical judgment at the first input, while the cost is the increasing complexity when we put loopd body at the end of each branch of logical judgment.

### Example 1.3 number game with logical loop
```python
print("Let's play a game!")
while True:                     #Put "while True" at the head of loop body, which avoids claiming the variable "guess" at the beginning
    number = input("Please enter a random number ranged 1-10:")            
    guess = int(number)   
    if guess == 6:        
        print("Bingo!")
        break
    else:
        if guess > 6:
            print("Wrong number,lower please.")
        else:
            print("Wrong number,higher please")
print("Game Over")
```
#### *New command*
```python
while True: #the loop will end when <break> condition is met(True)
    if <condition>:
      break #<break> can be put next stair after any conditional statement
    else:   #<break> follows principle of proximity for the nearest <while True:>
      break #so the nested <while True:> and <break> won't interfere the outside
```    

The code complexity get improved when we use logical loop.

### Example 1.4 random number game with logical loop

```Python   
import random #Introduce random module
secret = random.randint(1,10) #pick up random integer at closed interval
print("Let's play a game!")
while True:
    number = input("Please enter a random number ranged 1-10:")            
    guess = int(number)   
    if guess == secret: #Make variable "secret" the logical judgment condition
        print("Bingo!")
        break
    else:
        if guess > secret: #Here also
            print("Wrong number,lower please.")
        else:
            print("Wrong number,higher please")
print("Game Over")
```
#### *New command*  
`improt random`   introduce random module  
`x = random.randit(a,b)`    x is the name of variable,randit means to pick a integer randomlly, and (a,b) is a closed interval.
### Example 1.5 Chances limited random number game with special feedback
```Python
import random
secret = random.randint(1,10)
print("Let's play a game!")
i = 0                        #Counter，should notice that this part don't get involved into loop, otherwise the variable "i" will be automatically reset zero at the beginning of every loop
while True:                  #The loop part of "while True" start with "else", if the "if" condition is met, "else" part will be skipped
    if i == 4:               #Terminate condition：chances +1 of all you can try
        print("You lose")
        break                #"break" here is loacted at the next stair of the last "if"
    else:
        number = input("Please enter a random number ranged 1-10:")            
        guess = int(number)   
        if guess == secret:  
            print("Bingo!")
            break
        else:
            if guess > secret:
                print("Wrong number,you have " + str(3-i) + " more chance(s),lower please.")  #Notice that when integer and strings are required to be printed at the same time, you should transfer the integer into strings too.
                i = i+1   #failed attempts +1
            else:
                print("Wrong number,you have " + str(3-i) + " more chance(s),higher please")  #Notice that the 4th attempt will be counted to end the game, so the acutal chances is 3 times.
                i = i+1
if i ==0:
    print("Amazing!")
print("Game Over")
```
### Example 1.6 Input number limited and chances limited random number game
```python
import random
secret = random.randint(1,10)
print("Let's play a game!")
i = 0                       
while True:
    if i == 4:               
        print("You lose")
        break                
    else:
        number = input("Please enter a random number ranged 1-10:")            
        guess = int(number)
        while True:                         #Notice the location of "While True"
            if guess >= 1 and guess <= 10:
                break
            else:
                number = input("Please enter a random number ranged 1-10:")
                guess = int(number)
        if guess == secret:                 #The stairs of logical judgments from here correspond the stairs of the former "While True", there is only order differences other than stairs differences.
            print("Bingo!")
            break
        else:
            if guess > secret:
                print("Wrong number,you have " + str(3-i) + " more chance(s),lower please.")  
                i = i+1   
            else:
                print("Wrong number,you have " + str(3-i) + " more chance(s),higher please")
                i = i+1
if i ==0:
    print("Amazing!")
print("Game Over")
```

### Example1.7 Complete number Game
```python
import random
secret = random.randint(1,10)
print("Let's play a game!")
i = 0                       
while True:               #Logical level1 Counter
    if i == 4:               
        print("You lose")
        break                
    else:
        number = input("Please enter a random number ranged 1-10:") #Input level 1
        while True:              #Logical lever2.1 numbers or characters
            if number.isdigit() == True:  
                break
            else:
                print("Invalid input,make sure the input has to be numbers.")
                number = input("Please enter a random number ranged 1-10:") #Input level 1-
        while True:              #Logical lever2.2 number validation
            guess = int(number)
            if guess >= 1 and guess <= 10 and number.isdigit() == True:
                break
            else:
                if number.isdigit() == True:  #Logical level2.2.1 number from the wrong interval
                    print("Invalid input:please pick numbers from the given interval.")
                    number = input("Please enter a random number ranged 1-10:") #Input level 2
                else:                         #Logical level2.2.2 not numbers
                    print("Invalid input,make sure the input has to be numbers.")
                    number = input("Please enter a random number ranged 1-10:") #Input level 2-
        if guess == secret:        #Logical lever 3 number comparison         
            print("Bingo!")
            break
        else:
            if guess > secret:
                print("Wrong number,you have " + str(3-i) + " more chance(s),lower please.")  
                i = i+1   
            else:
                print("Wrong number,you have " + str(3-i) + " more chance(s),higher please")
                i = i+1
if i ==0: #hit it at the first time
    print("Amazing!")
print("Game Over")
```

### Example1.7a Complete number game reviesed
```Python
import random
secret = random.randint(1,10)
print("Let's play a game!")
i = 0                       
while True:                       #llv.1 Counter
    if i == 4:               
        print("You lose")
        break                
    else:
        number = input("Please enter a random number ranged 1-10:")                 #ilv.1 first input
        while True:                                                                 #llv.2 number validation
            if (number.isdigit() == True) and int(number) >= 1 and int(number) <= 10:
                break
            else:
                if number.isdigit() == True:
                    print("Invalid input:please pick numbers from the given interval.")
                    number = input("Please enter a random number ranged 1-10:")         #ilv.2 wrong numbers
                else:
                    print("Invalid input,make sure the input has to be numbers.")
                    number = input("Please enter a random number ranged 1-10:")         #ilv.2- characters

        guess = int(number)
        if guess == secret:                                                        #llv.3 comparison
            print("Bingo!")
            break
        else:
            if guess > secret:
                print("Wrong number,you have " + str(3-i) + " more chance(s),lower please.")  
                i = i+1   
            else:
                print("Wrong number,you have " + str(3-i) + " more chance(s),higher please")
                i = i+1
if i ==0: #hit the answer at the first time
    print("Amazing!")
print("Game Over")
```
Using brackets can set priority for the part of code, so you can avoid using multiple lines to describe yourconditional statement. And you'd better don't do comparison between strings.

#### *New command*  
`x.isdigit()`   x is the name of variable  
`isinstance(x,y)`    x is the name of variable and y is data type including *int*, *float*, *str*, *bool*.

## 2、Mathematical operation
### 2.1 Mutiple assignment
```python
a = b = c = d = 10
```
equals
```python
a = 10
b = 10
c = 10
d = 10
```
### 2.2 Operation
#### 2.2.1  Operate and assign
```python
a = 10
a = 10 + 3
```
equals
```python
a = 10
a += 3
```
It also applys to other operators like _-_, _\*_, _/_, _//_, _**_, _%_
#### 2.2.2 */* and *//*
*/* is True division while *//* is Floor division for it will return the result in integer, like:
```python
a = 10
a // 2
```
equals
```python
a = 10
int(a / 2)
```
#### 2.2.3 _**_ and _%_
_**_ is an operator for exponentiation, like:
```python
a = 10
a **= 10
```
the result will be `a = 10^10`.  

And _%_ returns the residue in a division, like:
```python
a = 10
a %= 3
```
equals
```python
a = 10
a -= 3 * int(10 / 3)
```

### 2.3 Operation Priorities
```
1. **         #(the operator on the right side of it is prior to the one on the left)
2. +, -       #(positive and negative)
3. +, -, *, /, //
4. <, <=, >, >=, ==, !=
5. not, and, or
```
## 3. Branch and Loop
