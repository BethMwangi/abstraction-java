<h1>Understanding Abstraction in Java</h1>
<p>In computer science, abstraction is the process by which data and programs are defined with a representation similar in form to its meaning (semantics), while hiding away the implementation details.</p>

<p>In <a href="http://harrisonkamau.github.io/code-ninja/Object-Oriented-Programming/">object-oriented programming</a> theory, abstraction involves the facility to define objects that represent abstract “actors” that can perform work, report on and change their state, and “communicate” with other objects in the system.</p>

<p>Abstraction in any programming language works in many ways. It can be seen from creating subroutines to defining interfaces for making low level language calls. Some abstractions try to limit the breadth of concepts a programmer needs, by completely hiding the abstractions they in turn are built on, e.g. design patterns.</p>

<h2>Abstract class in Java</h2>
<p>A class that is declared as abstract is known as abstract class. It needs to be extended and its method implemented. It cannot be instantiated.</p>

<h2>Example of abstract class</h2>

~~~Java
  abstract class A{}  
~~~

<h2>Example of abstract method</h2>
<h2>Example of abstract class</h2>

~~~Java
abstract void printStatus();//no body and abstract   
~~~

<h2>Example</h2>

~~~Java
abstract class Bank{    
abstract int getRateOfInterest();    
}    

class SBI extends Bank{    
int getRateOfInterest(){return 7;}    
}    
class PNB extends Bank{    
int getRateOfInterest(){return 7;}    
}    

class TestBank{    
public static void main(String args[]){    
Bank b=new SBI();//if object is PNB, method of PNB will be invoked    
int interest=b.getRateOfInterest();    
System.out.println("Rate of Interest is: "+interest+" %");

~~~

<p>Output:</p>
~~~Java
run:
Rate of Interest is: 7 %
BUILD SUCCESSFUL (total time: 0 seconds)
~~~

<h1>Abstract Data Types</h1>
<p>In computer science, an abstract data type (ADT) is a mathematical model for a certain class of data structures that have similar behavior; or for certain data types of one or more programming languages that have similar semantics. An abstract data type is defined indirectly, only by the operations that may be performed on it and by mathematical constraints on the effects (and possibly cost) of those operations.</p>

<h2>Representation Independence</h2>
<p>Critically, a good abstract data type should be representation independent. This means that the use of an abstract type is independent of its representation (the actual data structure or data fields used to implement it), so that changes in representation have no effect on code outside the abstract type itself. For example, the operations offered by List are independent of whether the list is represented as a linked list or as an array.</p>

<p>You won’t be able to change the representation of an ADT at all unless its operations are fully specified with preconditions and postconditions, so that clients know what to depend on, and you know what you can safely change.</p>

<h2>Example: Different Representations for Strings</h2>
<p>Let’s look at a simple abstract data type to see what representation independence means and why it’s useful. The MyString type below has far fewer operations than the real Java String, and their specs are a little different, but it’s still illustrative. Here are the specs for the ADT:</p>

~~~Java
/** String represents an immutable sequence of characters. */
public class MyString {

    //////////////////// Example of a creator operation ///////////////
    /** @param b a boolean value
      * @return string representation of b, either "true" or "false" */
    public static MyString valueOf(boolean b) { ... }

    //////////////////// Examples of observer operations ///////////////
    /** @return number of characters in this string */
    public int length() { ... }

    /** @param i character position (requires 0 <= i < string length)
      * @return character at position i
      */
    public char charAt(int i) { ... }

    //////////////////// Example of a producer operation ///////////////    
    /** Get the substring between start (inclusive) and end (exclusive).
     * @param start starting index
     * @param end ending index.  Requires 0 <= start <= end <= string length.
     * @return string consisting of charAt(start)...charAt(end-1)
     */
    public MyString substring (int start, int end) { ... }
}
~~~
