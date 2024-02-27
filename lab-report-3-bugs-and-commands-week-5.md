# Lab Report 3 Bugs and Commands 

## Part 1

### Buggy program
``reversed()`` return the given array in reversed order

````
 static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
````

### Failure inducing Input
`` { 1, 2 } `` an array with a length > 0

```
  @Test
  public void testReversed() {
    int[] input1 = { 1, 2 };
    assertArrayEquals(new int[]{ 2, 1 }, ArrayExamples.reversed(input1));
  }
```
### Failure inducing Output ~ Symptom

<img width="1128" alt="Screenshot 2024-02-26 at 7 14 59 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/64d21559-52ba-4091-9f6b-bf2adf5fa22b">

### Non-Failure inducing Input
`` { } `` an array with a length of 0 ~ empty array

```
  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```
### Non-Failure inducing Output ~ Symptom

<img width="1134" alt="Screenshot 2024-02-26 at 7 16 10 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/cf722f23-59cc-4a6d-a5e7-93ecf59d8ce5">

### Fixed Program
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

Previously, the program was reversing the newArray and then swapping those values into the input array. When the input array has a length greater than zero, it would reverse the newArray which would be filled with zeros and return an incorrect array. However, when the array is empty, it would just return an empty array and the bug would not be seen. To fix this, you would need to reverse the input array into the newArray by swapping their places in the loop and then returning the newArray as shown above.

## Part 2

## ```grep``` command 

### 1. ``-r`` allows grep to recursively search directories for patterns

Example 1 (basic recursive search)
```
carloslugo@Carloss-MacBook-Air ~ % grep -r "pattern" /Users/carloslugo/Desktop/
Binary file /Users/carloslugo/Desktop//cse12-wi24-pa4-Iterator-starter-main/starter/checkstyle-10.7.0-all.jar matches
Binary file /Users/carloslugo/Desktop//cse12-wi24-pa3-LinkedList-starter-main/starter/checkstyle-10.7.0-all.jar matches
```

Example 2 (only include files with jar extension)
```
carloslugo@Carloss-MacBook-Air ~ % grep -r "pattern" --include='*.jar' ./Downloads
Binary file ./Downloads/school/wtr '24/cse 12/programing assignments/cse12-wi24-pa1-RPS-starter-main/starter/checkstyle-10.7.0-all.jar matches
Binary file ./Downloads/school/wtr '24/cse 12/programing assignments/cse12-wi24-pa2-ArrayList-starter-main/starter/checkstyle-10.7.0-all.jar matches
Binary file ./Downloads/school/wtr '24/cse 12/misc./cse-12-pa-1-test/starter/checkstyle-10.7.0-all.jar matches
```
### 2. ``-c`` displays number of matched lines
Example 1
```
carloslugo@Carloss-MacBook-Air ~ % grep -c "" ./Downloads/file.txt 
4
```
Example 2 (used with -r to search recursively)
```
carloslugo@Carloss-MacBook-Air ~ % grep -r -c "" Projects/IdeaProjects                         
Projects/IdeaProjects/HelloWorld/.DS_Store:1
Projects/IdeaProjects/HelloWorld/HelloWorld.iml:11
Projects/IdeaProjects/HelloWorld/out/production/HelloWorld/Main.class:7
Projects/IdeaProjects/HelloWorld/.gitignore:29
Projects/IdeaProjects/HelloWorld/.idea/.gitignore:8
Projects/IdeaProjects/HelloWorld/.idea/workspace.xml:52
Projects/IdeaProjects/HelloWorld/.idea/modules.xml:8
Projects/IdeaProjects/HelloWorld/.idea/misc.xml:6
Projects/IdeaProjects/HelloWorld/src/Main.java:1
Projects/IdeaProjects/HelloWorld/src/Main.class:6
```
### 3. ``-n`` shows the lines that match
Example 1
```
carloslugo@Carloss-MacBook-Air ~ % grep -n "" Downloads/file.txt
1:Hi 
2:Hi
3:Hi
4:Hi
```
Example 2 (used with -r)
```
carloslugo@Carloss-MacBook-Air ~ % grep -r -n  "Hello World" ./Downloads/school/wtr\ \'24/cse\ 12/misc.
./Downloads/school/wtr '24/cse 12/misc./week1Discussion-main/lecture1/messages/en-us.txt:1:Hello World!
Binary file ./Downloads/school/wtr '24/cse 12/misc./discussion 1/HelloWorld.class matches
./Downloads/school/wtr '24/cse 12/misc./discussion 1/HelloWorld.java:3:        System.out.println("Hello World!");
```
### 4. ``-v`` shows the lines that do not match
Example 1
```
carloslugo@Carloss-MacBook-Air ~ % grep -v  "Hi" ./Downloads/file.txt
Hello
Hello
```
Example 2
```
carloslugo@Carloss-MacBook-Air ~ %  grep -v  "Pattern" Documents/LearningJS/Main.java 
package LearningJS;

public class Main {

    public static void main(String[] args){

        System.out.println("Hello World!");
    }
}
```


source : https://www.geeksforgeeks.org/grep-command-in-unixlinux/


