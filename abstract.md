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

<p>These public operations and their specifications are the only information that a client of this data type is allowed to know. Following the test-first programming paradigm, in fact, the first client we should create is a test suite that exercises these operations according to their specs. At the moment, however, writing test cases that use assertEquals directly on MyString objects wouldn’t work, because we don’t have an equality operation defined on these MyStrings. We’ll talk about how to implement equality carefully in the next reading. For now, the only operations we can perform with MyStrings are the ones we’ve defined above: valueOf, length, charAt, and substring. Our tests have to limit themselves to those operations. For example, here’s one test for the valueOf operation:</p>

~~~Java
MyString s = MyString.valueOf(true);
assertEquals(4, s.length());
assertEquals('t', s.charAt(0));
assertEquals('r', s.charAt(1));
assertEquals('u', s.charAt(2));
assertEquals('e', s.charAt(3));
~~~

<h2>Testing an Abstract Data Type</h2>
<p>We build a test suite for an abstract data type by creating tests for each of its operations. These tests inevitably interact with each other, since the only way to test creators, producers, and mutators is by calling observers on the objects that result.</p>
<p>Here’s how we might partition the input spaces of the four operations in our MyString type:</p>

~~~Java
// testing strategy for each operation of MyString:
//
// valueOf():
//    true, false
// length():
//    string len = 0, 1, n
//    string = produced by valueOf(), produced by substring()
// charAt():
//    string len = 1, n
//    i = 0, middle, len-1
//    string = produced by valueOf(), produced by substring()
// substring():
//    string len = 0, 1, n
//    start = 0, middle, len
//    end = 0, middle, len
//    end-start = 0, n
//    string = produced by valueOf(), produced by substring()
~~~
<p>Then a compact test suite that covers all these partitions might look like:</p>

~~~Java
@Test public void testValueOfTrue() {
    MyString s = MyString.valueOf(true);
    assertEquals(4, s.length());
    assertEquals('t', s.charAt(0));
    assertEquals('r', s.charAt(1));
    assertEquals('u', s.charAt(2));
    assertEquals('e', s.charAt(3));
}

@Test public void testValueOfFalse() {
    MyString s = MyString.valueOf(false);
    assertEquals(5, s.length());
    assertEquals('f', s.charAt(0));
    assertEquals('a', s.charAt(1));
    assertEquals('l', s.charAt(2));
    assertEquals('s', s.charAt(3));
    assertEquals('e', s.charAt(4));
}

@Test public void testEndSubstring() {
    MyString s = MyString.valueOf(true).substring(2, 4);
    assertEquals(2, s.length());
    assertEquals('u', s.charAt(0));
    assertEquals('e', s.charAt(1));
}

@Test public void testMiddleSubstring() {
    MyString s = MyString.valueOf(false).substring(1, 2);
    assertEquals(1, s.length());
    assertEquals('a', s.charAt(0));
}

@Test public void testSubstringIsWholeString() {
    MyString s = MyString.valueOf(false).substring(0, 5);
    assertEquals(5, s.length());
    assertEquals('f', s.charAt(0));
    assertEquals('a', s.charAt(1));
    assertEquals('l', s.charAt(2));
    assertEquals('s', s.charAt(3));
    assertEquals('e', s.charAt(4));
}

@Test public void testSubstringOfEmptySubstring() {
    MyString s = MyString.valueOf(false).substring(1, 1).substring(0, 0);
    assertEquals(0, s.length());
}
~~~

<p>Notice that each test case typically calls a few operations that make or modify objects of the type (creators, producers, mutators) and some operations that inspect objects of the type (observers). As a result, each test case covers parts of several operations.</p>
