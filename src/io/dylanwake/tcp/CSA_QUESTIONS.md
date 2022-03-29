# CSA QUESTIONS

----

```java
/**
 * @author Dylan Sun
 * @brief There are 10 mcqs and 1 frq in this document
 *        which I found been major issues in real production
 *        coding.
 *        
 *        Note: All code under the annotation "//call from main()"
 *        means that these code segments are wrapped by a 
 *        public static void main(String[] args){} method in
 *        a trivial java class.
 *        
 *        ANSWERS : DEECE EEAEE
 */
```
### 1: 
Consider the following code:
```java
//method definition
public static void method(int value){
    value = anotherMethod(value);
}

public static int anotherMethod(int value){
    return 25/value;
}

//call from main():
int var = 15;
method(var);  //final line
```
If we run an inspection on the code, what will be the final value of var on `//final line`?
```
A: 2.5;
B: 2;
C: 3;
D: 15;
E: The code will not compile;
```

### 2:
Consider the following code: 
```java
//class definition
class A{ /*...*/ }
class B extends A{ /*...*/ }

//call from main():
A obj1 = new A();
A obj2 = new B();

B obj3 = (B)obj2; //line l1
B obj4 = (B)obj1; //line l2
```
What will be the result of executing this code segment?
```java
A: The code executes properly
B: A compile error is returned at line l1 
C: A compile error is returned at line l2
D: A runtime exception is throwed at line l1
E: A runtime exception is throwed at line l2
```
### 3:
Consider the following class definition:
```java
//defined in file Tensor.java 
public class Tensor{
    public int dimension;
    public float[] elements;
    
    public Tensor(){}
    
    public Tensor(int dimension, float[] elements){
        this.dimension = dimension;
        this.elements = elements;
    }
}
```
The class is called as follow:
```java 
Tensor mat = new Tensor();
method1(mat.dimension);  //line l1
method2(mat.elements);   //line l2
```
What will be the result of executing this code segment?
```
A: A NullPointerException is thrown at line l1 because "dimension" is not initialized
B: A NullPointerException is thrown at line l2 because "elements" is not initialized
C: The code executes properly since "dimension" and "elements" are initialized to default 
   values automatically while the Tensor object is created
D: Whether an NullPointerException is thrown depends on the implementation of method1()
e: Whether an NullPointerException is thrown depends on the implementation of method2()
```

### 4:
Consider the following code segment:
```java
float threshold = 220f;
//generate a dataset with at most 1,000,000 elements
float[] dataset = generateDataset();
int target = catchIndex(dataset, threshold, 0); //to be implemented
```
The goal of method `catchIndex()` is to find the first index of the element from a given index in the dataset
that are above the threshold value. The followings are prompted implementations of `catchIndex()`
by an auto code completion tool:
```java
//TODO: AUTO GENERATED IMPLEMENTATION 1:
public static int catchIndex(float[] dataset, float threshold, int index){
    for(int i = index; i < dataset.length; i++){
        if(dataset[i] > threshold){
            return i;
        }
    }
    return -1;
}

//TODO: AUTO GENERATED IMPLEMENTATION 2:
public static int catchIndex(float[] dataset, float threshold, int index){
    if(dataset[index] > threshold)  {
        return index;
    }
    
    if(index >= dataset.length - 1){
        return -1;
    }
    
    return catchIndex(dataset, threshold, index + 1);
}

//TODO: AUTO GENERATED IMPLEMENTATION 3:
public static int catchIndex(float[] dataset, float threshold, int index){
    int proc = index;
    for(float current : dataset){
        if(current > threshold){
            return index;
        }    
        index++;
    }
    return -1;
}
```
which of the above implementations will produce proper output given any dataset?
```java
A: 1 only
B: 2 only
C: 1 and 3 only
D: 1 and 2 only
E: 1, 2 and 3
```
### 5:
Consider the following code segment:
```java
//class definition
class A{
    public void method1(){
        method2();
        System.out.println("A.method1()");
    }
    
    public static void method2(){
        System.out.println("A.method2()");
    }
}

class B extends A{
    @Override
    public void method1(){
        System.out.println("B.method1()");
        super.method1();
    }
    
    @Override
    public static void method2(){
        System.out.println("B.method2()");
    }
}
```
The classes are called in the following code:
```java
A obj1 = new B();
obj1.method1(); //line l1
```
What is printed as the result of execution?
```
A: B.method1()
   A.method1()
   A.method2()
        
B: A.method1()
   A.method2()
        
C: B.method1()
   A.method1()
   B.method2()

D: B.method1()
   B.method2()

E: The code does not compile. 
```
### 6:
Consider the following code segment:

```java
//class definition
class CLS {
    public int member1;
    public int member2;

    public CLS(int member1, int member2) {
        this.member1 = member1;
        this.member2 = member2;
    }
}

//call from main():
ArrayList<CLS> list = generateList(); //generates 20 CLS Objects
/* CODE TO BE COMPLETED */
```
The goal of the code segment is to remove any CLS objects with product of members greater than 10. Which of the 
following implementations will complete the work?
```java
//IMPLEMENTATION 1:
for(CLS element : list){
    if(element.member1 * element.member2 > 10){
        list.remove(element);
    }
}

//IMPLEMENTATION 2:
for(int i = 0; i < list.size(); i++){
    CLS element = list.get(i);
    if(element.member1 * element.member2 > 10){
        list.remove(i);
    }
}

//IMPLEMENTATION 3:
int index = 0;
while(index < list.size()){
    CLS element = list.get(index);
    if(element.member1 * element.member2 > 10){
        list.remove(index);
    }
    else{
        index++;
    }
}
```
```
A: 1 only
B: 2 only
C: 1 and 2 only
D: 1 and 3 only
E: 3 only
```

### 7:
The following is a part of file `NERV.java`

```java
import java.util.ArrayList;

public class Agent {
    public String name;
    public int clearanceLevel;

    public Agent(String name, int clearanceLevel) {
        this.name = name;
        this.clearanceLevel = clearanceLevel;
    }

    public Agent(String name) {
        this.name = name;
        this.clearanceLevel = 0;
    }
}

public class NERV {
    public ArrayList<Agent> agents = new ArrayList<>(20); //line l1
    public NERV(){
        for(int i = 0; i <= agents.size(); i++){ 
            agents.add(new Agent("Agent" + i));  //line l2
        }
    }
}
```
The designed behavior of the code is to initialize the
NERV agency with 20 Agents. However, the code does not work as intended.
What is the problem?
```
A: The code does not compile.
B: A NoSuchMethodException is thrown on line l1;
C: An ArrayIndexOutOfBoundException is thrown on line l2;
D: A NullPointerException is thrown on line l2;
E: The code initialized more than 20 Agents.
```
### 8:
Which of the following boolean expressions is equivalent to `A or not B`?
```java
A: !(!A && B)
B: !(A || B)
C: A && B
D: !(!A || B)
E: !(A && !B)
```

### 9:
Consider the following code segment:
```java
public static int controller(int value){
    if(value < 10){
        return 1;
    }
    if(value < 20){
        return 2;
    }
    else if(value < 30){
        return 3;
    }
    else{
        return 4;
    }
}
```
Which of the following statements is true?
```
A: the code will always return 4
B: The code returns 2 for any value less than 20
C: Two values are returned for values less than 10
D: The code will not compile because a return statement
   is missing outside of the if-else block
E: The code works as intended
```

### 10:
Consider the following code segment:
```java
public void method1(String val){
    val = val.substring(val.length()/2);
    method1(val);
    System.out.println(val);
}
```
What is the output of this method when the input equals `DREAMSCAPE`?
```
A: E
   PE
   APE
   SCAPE
        
B: E
   PE
   SCAPE
        
C: D
   DR
   DRE
   DREAM
        
D: D
   DR
   DREAM
   
E: java.lang.StackOverflowError
```
### 11: Free Response Question
You are climbing a stair case. It takes n steps to reach to the top.
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
Precondition: Given n will be a positive integer greater than 3.

The signature of the method have been coded for you:
```java
public static int getTotalClimbWays(int n) {
    // WRITE YOUR CODE HERE
}
```