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
