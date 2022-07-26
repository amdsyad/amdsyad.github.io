---
layout: default
---
26/07/2022

# From Unknown to Have Something (OSWE)

Hi all here i will share my journey to become an “OSWE” certified holder

![oswe](/images/oswe/offsec-awae.png)

Hi everyone, Today i received that i passed the oswe exam, ok let's jump into the what is my approach and how i tackle the oswe module and lab.


## Pre OSWE

Before i enroll, i also know the oswe design to identify vulnerability on source code level and also need to automated the exploitation process. you can view the course prerequisites here.

![oswe-pre](/images/oswe/oswe-pre.png)

The prerequisites look like we need to know atleas one programming language to automated our exploitation process.

## My approach and Journey

### 1st approach

Before enroll i starting to learn programming language like PHP (Object-oriented programming) OOP i learn from [Edvin Diaz](https://www.udemy.com/course/oop-php-object-oriented-programing-with-project-1-course/). This course will teach you how to create a web application using oop style and also include the CRUD part.


### 2nd approach

I completed my learning, then what i'm doing started to create one vulnerable web application for practice my writing code skill and also i created containts vulnerability like below.

- SQL Injection
- File Upload
- Cross site scripting (XSS)
- Open Redirect

### 3rd approach 

I understand the code and how the function call inside the function and outside the function and also i know the sql query how work. Then i try to learn http request in python3 from here
[python3 request](https://requests.readthedocs.io/en/latest/). After i learn the python requests i try to create one scripting code to perform Authentication like below :). 

My first script 

`proxies = {"http": "http://127.0.0.1:8080", "https": "https://127.0.0.1:8080"}

print("[*] Exploit For BOX Kopi ")

def login_admin(ip,username,password):
    target = {'username': str(username),'password': password,'submit':'submit'}
    x = sess.post('http://%s/kopi/login.php' % str(ip), target, proxies=proxies)
    if 'Welcome User3' in x.text:
        print("[+] Success Login And Bypass")
    else:
        print("[+] Failed To Login")
`