# Lab Report 1 - Remote Access and File System (Week 1)

## `cd` command with no argument 
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/75f9867e-d9ad-4824-95aa-3aa0e8a34004)
<p>The working directory right now is <code>/home</code>. </p>
<p><code>cd</code> stands for change directory. <code>cd</code> with no argument is going to home directory, so it will stay in the same directory</p>
<img width="288" alt="image" src="https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/7d933b80-f237-4bb4-b259-56bf4b81e024">
<p>The working directory here is <code>/home/lecture1</code>.</p>
<p>In this case, as the <code>cd</code> without argument result to directing to the home directory, it changes the working directory to <code>/home/</code>.</p>

---

## `cd` command with path to directory as an arguement
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/a356a282-b582-4885-a9ab-188cd78d4b94)

<p>The working directory right now is <code>/home</code>. </p>
<p>As for now, we have the directory as the argument of the command <code>cd</code>. 
As the change directory command used with directory argument properly, this works and changed the file directory from <code>/home</code> to <code>/home/lecture1</code> without any error.
So this ended up as changing directory as we intended, so, there is no error on this code. </p>

---

## `cd` command with path to a file as an argument
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/c1e19781-6e0a-4f0d-876e-a3c59fd8efeb)
<p>The working directory right now is <code>/home/lecture1</code>. </p>
<p>As I command as `cd Hello.java` as using file as an argument, terminal shows that Hello.java is not a directory. 
As we ask for change the directory, the argument must be the directory as we asked for 'change directory'. As termial directly shows that our input was wrong, this is error.</p>

---

## `ls` command with no argument
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/2654f88e-4cf5-4fb5-afc6-8c7ec3e5b239)
<p>The working directory right now is <code>/home</code>.</p>
<p><code>ls</code> command is the command that list the directory or file in working directory. 
So basically it just list down all directories and files inside the working directory. I just command ls without any argument, and it listed down all files and directories, so it was accepted and thus, it is not error.
</p>

---

## `ls` command with path to directory as an argument
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/0edaa42c-4cf0-438e-adbb-9552c0a06a31)
<p>The working directory right now is <code>/home</code>.</p>
<p>As I command <code>ls + (directory)</code>, it shows the files and directories inside the directory that I commanded. 
  For example, as I command <code>ls lecture1</code>, it showed files and directories that is inside the directory lecture1. Also, as it well shows the list of the file and direcotries, there is no error on this code.</p>

---

## `ls` command with path to a file as an argument
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/245145d9-0ab3-4a71-ab4f-1ebb51c5a99f)
<p>The working directory right now is <code>/home/lecture1</code></p>
<p>As I command <code>ls + (file)</code>, then as the above photo, it just print out the exact same file name. 
For example, as I command <code>ls Hello.java</code> asthe above photo, it doesn't show the element inside the file or other things, but only repeats the file name. 
  But I still think that it is not error as it prints something even though it is printing just it's name.</p>

---

## `cat` command with no argument
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/246e5313-db01-4ef5-b7fa-eedde0569ffc)
<p>The working directory right now is <code>/home</code>.</p>
<p>As I just command <code>cat</code> without any argument, it just keeps running without returning anything. I had to use <code>(control) + c</code>(mac) to break the code.
I think the output here is error as it just locks me in endless loop.</p>

---

## `cat` command with path to directory as an argument
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/3efd527b-d4c4-4f4b-8454-34dc8019b9b2)
<p>The working directory right now is <code>/home</code>.</p>
<p>When I command <code>cat lecture1</code> as using pathj to directory as an argument, it prints out that lecture 1 is a directory. So computer is expecting other filesystem for this command.
The output here is definitely error as the output shows that basically told you that you used different filesystem.</p>

---
## `cat` command with path to a file as an argument
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/c9c59b34-d066-40e5-8a96-465b52526531)
<p>The working directory right now is <code>/home/lecture1/messages</code></p>
<p>When I command <code>cat en-us.txt</code> in this current directory, it opens the txt. file inside the terminal and shows me the element inside it. 
The command `cat` stands for concatenate, and it is the command that is frequently used to read data from the file. As we successfuly read the file, this is not the error at all.</p>

---





