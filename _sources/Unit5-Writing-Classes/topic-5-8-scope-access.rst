.. qnum::
   :prefix: 5-8-
   :start: 1

.. |CodingEx| image:: ../../_static/codingExercise.png
    :width: 30px
    :align: middle
    :alt: coding exercise
    
    
.. |Exercise| image:: ../../_static/exercise.png
    :width: 35
    :align: middle
    :alt: exercise
    
    
.. |Groupwork| image:: ../../_static/groupwork.png
    :width: 35
    :align: middle
    :alt: groupwork
    
    
Scope and Access
=================

The **scope** of a variable is defined as where a variable is accessible or can be used. The scope is determined by where you declare the variable when you write your programs. When you declare a variable, look for the closest enclosing curly brackets { } -- this is its scope.  

Java has 3 levels of scope that correspond to different types of variables:

- **Class Level Scope** for **instance variables** inside a class.

- **Method Level Scope** for **local variables** (including **parameter variables**) inside a method.

- **Block Level Scope** for **loop variables** and other local variables defined inside of blocks of code with { }.

The image below shows these 3 levels of scope. 

.. figure:: Figures/scopeDiagram.png
    :width: 500px
    :align: center
    :alt: Scope Levels
    :figclass: align-center

    Figure 1: Class, Method, and Block Level Scope
    
|Exercise| Check Your Understanding

.. clickablearea:: name_class_scope
    :question: Click on all the variable declarations that are at Class Level Scope.
    :iscode:
    :feedback: Remember that the instance variables declared at the top of the class have Class Scope.

    :click-incorrect:public class Name {:endclick:
    
        :click-correct:private String first;:endclick:
        :click-correct:public String last;:endclick:
        
        :click-incorrect:public Name(String theFirst, String theLast) {:endclick:
            :click-incorrect:String firstName = theFirst;:endclick:
            :click-incorrect:first = firstName;:endclick:
            :click-incorrect:last = theLast;:endclick:
         :click-incorrect:}:endclick:
    :click-incorrect:}:endclick:    
    
.. clickablearea:: name_method_scope
    :question: Click on all the variable declarations that are at Method Level Scope.
    :iscode:
    :feedback: Remember that the parameter variables and the local variables declared inside a method have Method Level Scope.

    :click-incorrect:public class Name {:endclick:
    
        :click-incorrect:private String first;:endclick:
        :click-incorrect:public String last;:endclick:
        
        :click-correct:public Name(String theFirst, String theLast) {:endclick:
            :click-correct:String firstName = theFirst;:endclick:
            :click-incorrect:first = firstName;:endclick:
            :click-incorrect:last = theLast;:endclick:
         :click-incorrect:}:endclick:
    :click-incorrect:}:endclick:        

**Local variables** are variables that are declared inside a method, usually at the top of the method. These variables can only be used within the method and do not exist outside of the method. Parameter variables are also considered local variables that only exist for that method. It's good practice to keep any variables that are used by just one method as local variables in that method. 

Instance variables at class scope are shared by all the methods in the class and can be marked as public or private with respect to their access outside of the class. They have Class scope regardless of whether they are public or private.

Another way to look at scope is that a variable's scope is where it lives and exists. You cannot use the variable in code outside of its scope. The variable does not exist outside of its scope.

|CodingEx| **Coding Exercise**

Try the following code to see that you cannot access the variables outside of their scope levels in the toString() method. Explain to someone sitting next to you why you can't access these. Try to fix the errors by either using variables that are in scope or moving the variable declarations so that the variables have larger scope. 


.. activecode:: PersonScope
  :language: java

  public class Person 
  {
     private String name;
     private String email;
    
     public Person(String initName, String initEmail)
     {
        name = initName;
        email = initEmail;
     }
     
     public String toString() 
     { 
       for (int i=0; i < 5; i++) {
          int id = i;
       } 
       // Can you access the blockScope variables i or id?
       System.out.prtinln("i at the end of the loop is " + i);
       System.out.println("The last id is " + id);
       
       // Can toString() access parameter variables in Person()?
       return  initName + ": " + initEmail;
     }
     
     // main method for testing
     public static void main(String[] args)
     {
        // call the constructor to create a new person
        Person p1 = new Person("Sana", "sana@gmail.com");
        System.out.println(p1);
     }
  }

If there is a local variable with the same name as an instance variable, the variable name will refer to the local variable instead of the instance variable, as seen below. We'll see in the next lesson, that we can distinguish between the local variable and the instance variable using the keyword this to refer to this object's instance variables.

.. activecode:: PersonLocalVar
  :language: java

  public class Person 
  {
     private String name;
     private String email;
    
     public Person(String initName, String initEmail)
     {
        name = initName;
        email = initEmail;
     }
     
     public String toString() 
     { 
       String name = "unknown";
       // The local variable name here will be used,
       //  not the instance variable name.
       return  name + ": " + email;
     }
     
     // main method for testing
     public static void main(String[] args)
     {
        // call the constructor to create a new person
        Person p1 = new Person("Sana", "sana@gmail.com");
        System.out.println(p1);
     }
  }

|Groupwork| Programming Challenge : Debugging
------------------------------------------------------------

Debug the following program that has scope violations. Then, add comments that label the variable declarations as class, method, or block scope.

.. activecode:: challenge-5-8-Debug
  :language: java

  public class TesterClass 
  {
     public static void main(String[] args)
     {
        Fraction f1 = new Fraction();
        Fraction f2 = new Fraction(1,2);
        System.out.println(f1);
        System.out.println(f2.numerator / f2.denominator);
     }   
   }
   
  /** Class Fraction */
  class Fraction
  {
     //  instance variables
     private int numerator;
     private int denominator;
     
     // constructor: set instance variables to default values
     public Fraction()
     {
        int d = 1;
        numerator = d;
        denominator = d;
     }
     
     // constructor: set instance variables to init parameters
     public Fraction(int initNumerator, int initDenominator)
     {
        numerator = initNumerator;
        denominator = initDenominator;
     }
     
     public String toString()
     {
       // if the denominator is 1, then just return the numerator
       if (denominator == d) {
          int newNumerator = 1;
       }
       return newNumerator + "/" + denominator;
     }
  }

Summary
-------

- **Scope** is defined as where a variable is accessible or can be used.

- Local variables can be declared in the body of constructors and methods. These variables may only be used within the constructor or method and cannot be declared to be public or private.

- When there is a local variable with the same name as an instance variable, the variable name will refer to the local variable instead of the instance variable.

- Formal parameters and variables declared in a method or constructor can only be used within that method or constructor.



