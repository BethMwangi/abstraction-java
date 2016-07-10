<h1>Arrays in Java</h1>
<p>Java array is an object the contains elements of similar data type. It is a data structure where we store similar elements. We can store only fixed set of elements in a java array.</p>
<p>An important feature about arrays is that arrays in java are index based, first element of the array is stored at 0 index.</p>

<h2>Types of Array in java</h2>
<p>There are two types of array.</p>
<ul>
  <li>Single Dimensional Array</li>
  <li>Multidimensional Array</li>
</ul>

<h2>Declaring Arrays in Java</h2>
~~~Java
datatype[] identifier; //preferred way
or
datatype identifier[];
~~~

<h2>Example</h2>
~~~java
char[] refVar;
int[] refVar;
short[] refVar;
long[] refVar;
int[][] refVar; //two-dimensional array
~~~

<h2>Initializing an array in java</h2>
1.By using new operator
~~~Java
int[] age = new int[5];    //5 is the size of array.
~~~

2.Initializing each element at declaration time
~~~Java
int age[5]={22,25,30,32,35};
~~~

<h2>Accessing elements in an array</h2>
~~~Java
public class Sample {

    public static void main(String args[]) {
        int[] newArray = new int[5];

        // Initializing elements of array seperately
        for (int n = 0; n < newArray.length; n++) {
            newArray[n] = n;
        }
        System.out.println(newArray[2]); // Assigning 2nd element of array value
    }
}
~~~

<p>Ouput:</p>
~~~Java
run:
2
BUILD SUCCESSFUL (total time: 0 seconds)
~~~

<h2>An example of a Multidimensional array</h2>
~~~Java
package arrayDemo;  
public class twoDimArrayDemo {  
    public static void main (String []args){  
        int twoDim [][] = new int [2][3];  
        twoDim[0][0]=1;  
        twoDim[0][1]=2;  
        twoDim[0][2]=3;  
        twoDim[1][0]=4;  
        twoDim[1][1]=5;  
        twoDim[1][2]=6;  
        System.out.println(twoDim[0][0] + " " + twoDim[0][1] + " " + twoDim[0][2]);  
        System.out.println(twoDim[1][0] + " " + twoDim[1][1] + " " + twoDim[1][2]);  
    }  
}  
~~~

<p>Output</p>
~~~Java
1 2 3
4 5 6
~~~
