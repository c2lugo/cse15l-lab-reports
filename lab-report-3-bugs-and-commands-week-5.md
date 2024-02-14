# Lab Report 3 Bugs and Commands 

## Part 1

### Buggy program
```reversed()```
return the given array in reversed order

```

 static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

```

### Failure inducing Input
``` { 1, 2 } ``` an array with a length > 0

```

  @Test
  public void testReversed() {
    int[] input1 = { 1, 2 };
    assertArrayEquals(new int[]{ 2, 1 }, ArrayExamples.reversed(input1));
  }

```
### Failure inducing Output ~ Symptom

<img width="680" alt="Screenshot 2024-02-13 at 7 12 02 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/63b5a45f-74b4-44d8-bcd8-8552e256f619">

### Non-Failure inducing Input
``` { } ``` an array with a length of 0 ~ empty array

```

  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }

```
### Non-Failure inducing Output ~ Symptom

<img width="184" alt="Screenshot 2024-02-13 at 7 15 57 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/aa3e9389-e805-4500-bc7e-667cd682567d">

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

