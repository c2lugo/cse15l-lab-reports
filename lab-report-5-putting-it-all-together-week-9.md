# Lab Report 5 Putting It All Together

## Part 1 - Debugging Scenario 
> **Anonymous:** Hey everyone, I'm kinda stuck trying to get my grader up and running. Every time I run the grading script, it prints that there was a compile error. Not entirely sure why this is happening; maybe some classpath hiccups or script logic got a bit funky. Any ideas to help me out? Would really appreciate it! Here is the output: 
> <img width="890" alt="Screenshot 2024-03-12 at 8 05 18 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/e8c358ac-0ee0-4e17-8346-2a3b639ebe05">


> **TA:** Hi there, it appears there may be an issue with your script. To further investigate, could you kindly execute the cloned Java file along with your test separately? This will help verify if there is an actual compile error in either of the Java files. Please provide an additional screenshot with the output for closer examination. Thank you.


> **Anonymous:** Yup, they seem to compile and run properly when ran seperately from the script. What do you think the bug is then?
> <img width="1311" alt="Screenshot 2024-03-12 at 8 21 41 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/b3b1ddf6-808a-4186-97dd-d45d57fbc313">


> **TA:** Let's take a closer look at the grading script. It seems there might be an issue with your conditional statement where it prints "Compile Error". In the script, change this line:
> ```bash
> if [[ $? -eq 0 ]]; then
> ```
> to
> ```bash
> if [[ $? -ne 0 ]]; then
> ```
> This should fix the condition for checking the compilation status. The reason for the change is that in bash, an exit code of 0 indicates success, while a non-zero exit code signifies an error. Try > running the script again and see if the compilation error persists. Previously you had the condition set to when the error code equals 0 it prints a compile error.


> **Anonymous:** Thanks! I made the change to the conditional statement as you suggested, and the script now runs without a compilation error.
> 
> <img width="924" alt="Screenshot 2024-03-12 at 9 05 28 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/c22db7f0-a1d3-408f-8a1f-1cb2065d8f9c">


#### Bug Description:
The bug lies in the conditional statement of the grade.sh script where it checks for compilation errors. The original line of code is:

```bash
if [[ $? -eq 0 ]]; then
```
This condition checks if the exit code of the previous command is equal to 0, which indicates success. However, the script mistakenly considers a successful compilation (exit code 0) as an error and prints "Complilation Error" before exiting.

Fix:
To resolve this issue, the condition in the script should be modified to check if the exit code is not equal to 0, indicating a compilation error. The corrected line of code is:
```bash
if [[ $? -ne 0 ]]; then
```

This change ensures that the script correctly identifies a compilation error when the exit code is not 0 and proceeds accordingly.

By making this adjustment, the script will now function as intended, printing "Compilation Error" and exiting if there is an issue during compilation, and continuing with the grading process if compilation is successful.

#### File Directory: 
```java
List-Examples-Grader/
  |-  .vscode 
  |-  grading-area
  	|-  hamcrest-core-1.3.jar
    |-  IsMoon.class
    |-  junit-4.13.2.jar
    |-  ListExamples.class
    |-  ListExamples.java
    |-  StringChecker.class
    |-  TestListExamples.class
    |-  TestListExamples.java
  |-  lib/
  	|-  hamcrest-core-1.3.jar
  	|-  junit-4.13.2.jar
  |-student-submission/
    |-  ListExamples.class
    |-  ListExamples.java
    |-  StringChecker.class
  |-  ExecExamples.class
  |-  ExecHelpers.class
  |-  grade.sh
  |-  GradeServer.class
  |-  GradeServer.java
  |-  Handler.class
  |-  IsMoon.class
  |-  Server.class
  |-  Server.java
  |-  ServerHttpHandler.class
  |-  TestListExamples.class
  |-  TestListExamples.java
  |- URLHandler.class
  ```

### **```grade.sh```**
```bash
CPATH='.:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'


if [ -f "student-submission/ListExamples.java" ]; then 
    echo "File Found"
else 
    echo "File ListExamples.java not found!"
    exit 1
fi

cp student-submission/ListExamples.java grading-area/
cp TestListExamples.java grading-area/
cp -r lib/ grading-area/

cd grading-area
javac -cp $CPATH *.java

if [[ $? -eq 0 ]]; then
    echo "Complilation Error"
    exit 1
fi

echo "Program compiled successfully!"

set +e

test_output=$(java -cp $CPATH org.junit.runner.JUnitCore TestListExamples 2>&1)

set -e

echo "$test_output"

echo "Grading..."
if grep -q "OK (" <<< "$test_output"; then
    echo "Full marks!"
elif grep -q "Tests run: 6,  Failures: 1" <<< "$test_output"; then
    echo "Partial marks. Check the output for details."
else
    echo "Tests failed. Check the output for details."
    exit 1
fi

echo "Finished grading."

# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
```
### **```TestListExamples.java```**
```java
import org.junit.Test;
import static org.junit.Assert.*;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
    public boolean checkString(String s) {
        return s.equalsIgnoreCase("moon");
    }
}

public class TestListExamples {

    @Test(timeout = 500)
    public void testMergeRightEnd() {
        List<String> left = Arrays.asList("a", "b", "c");
        List<String> right = Arrays.asList("a", "d");
        List<String> merged = ListExamples.merge(left, right);
        List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
        assertEquals(expected, merged);
    }

    @Test
    public void testMerge() {
        List<String> list1 = Arrays.asList("apple", "banana", "cherry");
        List<String> list2 = Arrays.asList("blueberry", "grape", "orange");

        List<String> result = ListExamples.merge(list1, list2);

        List<String> expected = Arrays.asList("apple", "banana", "blueberry", "cherry", "grape", "orange");
        assertEquals(expected, result);
    }

    @Test
    public void testMergeEmptyLists() {
        List<String> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();

        List<String> result = ListExamples.merge(list1, list2);

        assertTrue(result.isEmpty());
    }

    @Test
    public void testMergeEqualStringsInBothLists() {
        List<String> list1 = Arrays.asList("apple", "banana", "cherry");
        List<String> list2 = Arrays.asList("banana", "cherry", "date");

        List<String> result = ListExamples.merge(list1, list2);

        List<String> expected = Arrays.asList("apple", "banana", "banana", "cherry", "cherry", "date");
        assertEquals(expected, result);
    }

    @Test
    public void testFilterEmptyList() {
        List<String> inputList = new ArrayList<>();

        StringChecker checker = new IsMoon();

        List<String> result = ListExamples.filter(inputList, checker);

        assertTrue(result.isEmpty());
    }

}

```
### **```ListExamples.java```**
```java
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}

```

## Part 2 – Reflection
I really enjoyed the second half of the quarter. One thing that stood out was using jdg and vim. I found learning to do everything in the terminal to be useful and convenient in some cases. I also learned how to debug which will be crucial part of my future courses and time as a programer. I also found out how gradescope autograders work which is very cool. 


