# Lab Report 3 - Bugs and Commands (Week 5)

## Part 1: Bugs

### ListExamples Filter Method
We want the method that returns the list that has all the elements of the input list for which the StringChecker returns true.

```java
static List<String> filter(List<String> list, StringChecker sc) {
  List<String> result = new ArrayList<>();
  for(String s: list) {
    if(sc.checkString(s)) {
      result.add(0, s);
    }
  }
  return result;
}
```
---
#### Failure-inducing input
In this case, one of the failure-inducing input might be putting the list `List<String> list = Arrays.asList("a", "b");` as it will produce the output `["b", "a"]`.

```java
@Test
  public void testFilter() {
    ArrayList<String> input = new ArrayList<>(Arrays.asList("a", "b"));
    ArrayList<String> list = new ArrayList<>(Arrays.asList("a", "b"));
    L1aInterface L1a = new L1aInterface();

    assertEquals(list, ListExamples.filter(input, L1a));
  }
```
In this case, the test report failed, as we expected.

---
#### Input that doesn't induce a failure
If we put the list `List<String> list = Arrays.asList("a");` as the input, it will produce the output `["a"]` as the program intended.

```java
@Test
  public void testFilter() {
    ArrayList<String> input = new ArrayList<>(Arrays.asList("a"));
    ArrayList<String> list = new ArrayList<>(Arrays.asList("a"));
    L1aInterface L1a = new L1aInterface();

    assertEquals(list, ListExamples.filter(input, L1a));
  }
```
As we anticipated, if we run this JUnit test, it will pass the test.

---
#### The Symptom
<img width="446" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/200fc054-c547-4fa2-85df-332acaba9d17">\
<img width="200" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/3e622ad3-6355-4e28-973a-f2470832bf07">\
As we see, the first case failed, and the second case passed. The symptom is that the output was ["b", "a"] when it should be ["a", "b"], and also the fact that the first test case failed.

---
#### The bug
The bug here is that as `filter` goes through the input array, it adds the element of the list to the beginning of the output array instead of the end, as we expected. To fix the code, we can change it to add the element to the end of the output array.
``` java
static List<String> filter(List<String> list, StringChecker sc) {
  List<String> result = new ArrayList<>();
  for (String s : list) {
    if (sc.checkString(s)) {
      result.add(s);
    }
  }
  return result;
}
```
As we run this code to the same JUnit test code it passed\
<img width="200" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/dd1ba48d-4948-4d58-b72d-8a1c9e84f656">

---
### ListExamples Merge method
In this code, it looks at two lists, list1 and list2, then compares each element and makes the result list in the right order merging this two list.
``` java
static List<String> merge(List<String> list1, List<String> list2) {
  List<String> result = new ArrayList<>();
  int index1 = 0, index2 = 0;
  while (index1 < list1.size() && index2 < list2.size()) {
    if (list1.get(index1).compareTo(list2.get(index2)) < 0) {
      result.add(list1.get(index1));
      index1 += 1;
    } else {
      result.add(list2.get(index2));
      index2 += 1;
    }
  }
  while (index1 < list1.size()) {
    result.add(list1.get(index1));
    index1 += 1;
  }
  while (index2 < list2.size()) {
    result.add(list2.get(index2));
    index1 += 1;
  }
  return result;
}
```

---
#### Failure-inducing input
If the input is list1:`[]`, list2:`["a"]`, then there is no output and it enters an infinite loop.
```java
@Test
public void testMerge() {
  ArrayList<String> list1 = new ArrayList<>(Arrays.asList());
  ArrayList<String> list2 = new ArrayList<>(Arrays.asList("a"));
  assertEquals(new ArrayList<>(Arrays.asList("a")), ListExamples.merge(list1, list2));
}
```
In this case, the test report failed, as we expected.

---
#### Input that doesn't induce a failure
If the input is list1:`["a"]`, list2:`[]`, then the output will return `["a"]`.
```java
@Test
public void testMerge2() {
  ArrayList<String> list1 = new ArrayList<>(Arrays.asList("a"));
  ArrayList<String> list2 = new ArrayList<>(Arrays.asList());

  assertEquals(new ArrayList<>(Arrays.asList("a")), ListExamples.merge(list1, list2));
}
```
As we anticipated, if we run this JUnit test, it will pass the test.

---
#### The Symptom
<img width="720" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/8e6769cb-d7f2-4aa8-95c4-cae6e3134e51">\
<img width="161" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/8999eadf-5f4f-4b4e-a7f4-daac509bf2f6">\
As we see, the first case failed, and the second case passed. The symptom is that there was no output, and it entered the infinite loop. And also, the fact that the first case failed could also be a symptom.

---
#### The bug
The bug here is that as the method `merge` enters into a certain condition,
```java
  while (index2 < list2.size()) {
    result.add(list2.get(index2));
    index1 += 1;
  }
```
then it adds the wrong index, which makes it stay in the infinite loop. In order to fix this code, we could change it by changing index1 to index2.
``` java
static List<String> merge(List<String> list1, List<String> list2) {
  List<String> result = new ArrayList<>();
  int index1 = 0, index2 = 0;
  while (index1 < list1.size() && index2 < list2.size()) {
    if (list1.get(index1).compareTo(list2.get(index2)) < 0) {
      result.add(list1.get(index1));
      index1 += 1;
    } else {
      result.add(list2.get(index2));
      index2 += 1;
    }
  }
  while (index1 < list1.size()) {
    result.add(list1.get(index1));
    index1 += 1;
  }
  while (index2 < list2.size()) {
    result.add(list2.get(index2));
    index2 += 1;
  }
  return result;
}
```
As we ran this code, the JUnit tests both passed.\
<img width="176" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/76bdaece-a395-455d-984a-48d71c92ada8">

## Part 2 - Research Commands
### `grep` command
`grep` command is a command that is used to search text or serach for a string in a given file or files

---
#### `grep -c`
This prints only a count of the lines that match a pattern.\
<img width="595" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/0785dac3-81b4-4ef9-8b32-c893f9088cee">\
This prints the number of the line in the file that contains the word "example" in biomed/gb-2003-4-2-r16.txt. 
<img width="561" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/6c8bfccd-fb8f-4cb2-96d2-36a934129b15">\
This prints the number of the line in the file that contains the word "apple" in 911report/chapter-8.txt.
This `grep -c` could be used to find the number of line in the file. This could be used in different cases, but it is especially useful when you want 

#### `grep -l`
This display the file that matches the pattern.\
<img width="537" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/68b7cf7b-dea2-4248-b6c6-2ab13a19e064">\
As I run the command `grep -l "medical research" biomed/*`, it search through all the file in biomed directory that contains string "medical research" and then return those files.
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/095306be-228f-4710-92fe-c44d5f280542)
As I run the command `grep -l "high-risk" <file names>`, then it search through the file names that I send as argument and return the file name that contains "high-risk" as a string.
This is useful when you want to find certain word from lots of different file. you can use it to filter out the files.

#### `grep -h`
This command display the matched line but not the file name\
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/f3152033-01dd-4af7-b97d-7fc8b463bd4e)\
As I sent the command `grep -h "apple" biomed/*`, the terminal look into all the file in biomed directory and printed the line that contains the string "apple".\
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/3353af8e-91c1-4d52-af5f-62a4efb45050)\
As I run the command `grep -h "high-risk" <file names>` it search through the file that I sent and print out the line that contains the string "high-risk" from those file.\
This is useful when you want to print the line that contains the word, but not the file name. It could be useful if you make some kind of dictionary with the first alphabet and you want to search for certain word but not returning the file name.

#### `grep -n`
This command display the matched line and also the file name\
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/a869c6f9-9d9b-40c8-868f-5133711c67f1)\
As I sent the command `grep -n "medical research" biomed/*`, it printed out the file name, line number, and the line that contains the string.\
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/e2ab8c83-5d33-4500-baec-cd0dee8397d5)\
This also works when you manually send the file like this. The command `grep -n "high-risk" biomed/gb-2003-4-9-r58.txt biomed/1472-6807-2-1.txt biomed/1471-2288-3-4.txt biomed/1472-6823-3-1.txt` searches through the files here and prints out the file name, line number, and the line that contains this string.\
This command contains all the information that we could find in other commands that I introduced before. This could be especially useful if you want all the information that it could produce. 

(I found all the source from https://www.geeksforgeeks.org/grep-command-in-unixlinux/)






