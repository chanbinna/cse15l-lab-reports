# Lab Report 2 - Servers and SSH Keys (Week 3)

## Part 1: Writing the web server

### code for StringServer
```java
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int counter = 0;
    String list = "";


    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return list;

        }  else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    counter++;
                    list += counter + ". " + parameters[1] + "\n";
                    return list;
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
- Class Handeler is called from the StringServer, and then it implements the interface URLHandler, which calls the method handleRequest. This is our main method (the relevant method) that makes `/add-message` work.

#### `handleRequest` Method
- If the path is `/`, then returns the whole list
- If the path contains `/add-messages`, then it makes new String array and put the information of query inside parameters[1], then add the message to the list with the index
- If any other path, returns `"404 Not Found!"`

### 1. First Screenshot
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/00e68c7a-c97b-49bf-ae42-66c6c7190833)
- `handleRequest(URI url)` is called with URI `http://localhost:4000/add-message?s=Hello`
- the relevant argument here is the url `http://localhost:4000/add-message?s=Hello`. The relevant field list's value changed to `"1. Hello"`
  - by `.split("=")`, `parameters[0]=s` and `parameters[1]="Hello"`
  - `counter`: 0, `list`: previously ""
- The relevant field changed from `""` to `"1. Hello"` after this request. It added the string that I put after `/add-message?s=` to the list with the number index. In order to make this work, I added a variable counter that could always track the index.
  - `counter`: 1
  - `list`: `"1.Hello\n"`
### 2. Second Screenshot
![image](https://github.com/chanbinna/cse15l-lab-reports/assets/91897225/6d7dd4d8-f8a1-4fb9-808d-0deceb4c3150)
- `handleRequest(URI url)` is called with URI `http://localhost:4000/add-message?s=How%20are%20you`
- the relevant argument here is the URL `http://localhost:4000/add-message?s=How%20are%20you`. The relevant field list's value changed to `"1. Hello\n2. How are you"`
  - by `.split("=")`, `parameters[0]=s` and `parameters[1]="How are you"`
  - `counter`: 1, `list`: previously `"1.Hello\n"`
- The relevant field changed from `"1. Hello"` to `"1. Hello\n2. How are you"` after this request? It added the string that I put after `/add-message?s=` to the list with the number index.
  - `counter`: 2
  - `list`: `"1. Hello\n2. How are you"`
---
## Part 2
### Path to the Private Key
```bash
Chanbins-Macbook-Pro:~ m1mac$ ls ~/.ssh/id_ed25519.pub
/Users/m1mac/.ssh/id_ed25519.pub
```
### Path to the Public Key
```bash
[cs15lfa23sq@ieng6-202]:~:27$ ls ~/.ssh/authorized_keys
/home/linux/ieng6/cs15lfa23/cs15lfa23sq/.ssh/authorized_keys
```
### log ieg6
```bash
Chanbins-Macbook-Pro:~ m1mac$ ls ~/.ssh/id_ed25519.pub
/Users/m1mac/.ssh/id_ed25519.pub
Chanbins-Macbook-Pro:~ m1mac$ ssh cs15lfa23sq@ieng6.ucsd.edu
Last login: Wed Oct 11 17:21:36 2023 from tower-us10.prod.edstem.org
============================ NOTICE =================================
Authorized use of this system is limited to password-authenticated
usernames which are issued to individuals and are for the sole use of
the person to whom they are issued.

Privacy notice: be aware that computer files, electronic mail and 
accounts are not private in an absolute sense.  You are responsible
for adhering to the ETS Acceptable Use Policies, which you can review at:
https://blink.ucsd.edu/faculty/instruction/tech-guide/policies/ets-acceptable-use-policies.html
=====================================================================

*** Problems, Suggestions, or Feedback ***
    
    For help requests, please create a ticket at:
    https://support.ucsd.edu/its 

    You may also report issues, suggestions, or feedback by e-mailing root on any system:
    mail -s "Your subject here" root
    Type your message - Ctrl+D to send
    
*** Access our Linux ssh terminals or remote desktops via a web browser at: ***
    https://linuxcloud.ucsd.edu

    All accounts must be enrolled in Duo for access. No VPN required.


-------------------------------------------------------

quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/hourly.2023-10-07_1601: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/daily.2023-10-01_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/daily.2023-10-02_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/hourly.2023-10-07_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/daily.2023-09-30_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/daily.2023-10-04_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/hourly.2023-10-08_0801: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/.snapshot/daily.2023-10-06_0010: Stale file handle
Hello cs15lfa23sq, you are currently logged into ieng6-202.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   20:30:01   16  2.53,   2.48,   1.87
ieng6-202   20:30:01   22  24.82,  24.28,  23.99
ieng6-203   20:30:01   15  16.95,  16.92,  16.82

 
Sun Oct 22, 2023  8:33pm - Prepping cs15lfa23
```
---
## Part 3
I think I learned lots of things through week 2 and week 3 materials.
- learned how to connect the remort server using `ssh` command
- learned about the details of url and port, developed better understanding on server
- learned details of debugging through class
- learned new terminal commands `mkdir` and `man`
- learned how to set the ssh key to access to server faster
I was able to deveop those skills through week 2 and 3. 
