# Class 05 - Linux and Bash
## 主要知识点
  - [1.Introduce to Linux](#1introduce-to-linux)
    - [1.1 Overview](#11-overview)
    - [1.2 Quickstart](#12-quickstart)
  - [2.Bash](#2background)
    - [2.1 Basic commands](#21-basic-commands)
    - [2.2 Common tools](#22-common-tools)
    - [2.3 Bash in day-to-day DevOps](#23-bash-in-day-to-day-devops)
  - [3.Regex](#3regex)
    - [3.1 Regex basic](#31-regex-basic)
    - [3.2 Regex practice](#32-regex-practice)
  - [4.Homework](#4homework)

 
# 课堂笔记
## 1.Introduce to Linux
### 1.1 Overview
Why Linux?
- Free 免费
  - you can install Linux on as many computers as you like without paying a cent for server licensing
- Highly secure 高度安全
  - almost non-vulnerable and most secure due to its inherent design 
  - does not require commercial anti-virus packages
- Flexible 很灵活
  - lets you control every aspect of the OS 
  - let you modify its source (even source code of applications)

Why Linux for DevOps?
- Tools and Platforms
  - a lot of open source projects run on Linux from the start
  - e.g. Git, Docker, Ansible, Kubernetes
- As a DevOps engineer, it’s perhaps unlikely that you’ll be working exclusively on Linux, or exclusively on Windows or Mac. In practice, you’ll probably work with a mix of operating systems. But Linux will be one important piece in your puzzle.
作为一名DevOps工程师，你可能不太可能只在Linux、Windows或Mac上工作。在实践中，你可能会使用多种操作系统。但是Linux将是您的拼图中一个重要的部分。

What is Linux?
- an operating system under an open-source license
- also one of the most popular platforms in the world
- e.g. Android is powered by Linux

Where and how did Linux start?
- 50 years ago computers are huge and expensive
- Bell Labs developers created a project “UNIX” for simple and elegant operating system, written in C
- in the 90s home PCs are powerful enough to run UNIX
- Linus from University of Helsinki developed a system based on UNIX, and named it Linux

Pros:
- free
- portable to any hardware platform
- made to keep on running without rebooting
- secure and versatile
- scalable
- short debug time

Cons
- too many different distributions
- not very user friendly and confusing for beginners
- is open source project trustworthy?

### 1.2 Quickstart
For Linux (OS X, Ubuntu etc) users
- open Terminal on your machine
- (optional) make your shell easier to use: install zsh
> https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/

For Windows users
- install Windows Subsystem for Linux (WSL)
> https://docs.microsoft.com/en-us/windows/wsl/install
- (optional) make your shell easier to use: install zsh
> https://blog.joaograssi.com/windows-subsystem-for-linux-with-oh-my-zsh-conemu/

#### 1.2.1 Directories
- checking which directory you’re in，查看你现在在哪个目录
```
    pwd
```
- checking current directory contents, 列出当前文件夹的详细信息，包括隐含文件
```
    ls -la
```
- going into a directory 进入文件夹
```
    cd
```
#### 1.2.2 Files
- create a new file in /tmp/file with content “hello world”
```
    echo “hello world” > /tmp/file
```
- check the file 打印文件
```
    cat /tmp/file
```
- change the file content，也可以查看文件，还可以编辑文件
```
    vim /tmp/file
    #退出
    :q
    #保存退出
    :wq
```
#### 1.2.3 Getting help
- read manual of vim command
```
    man vim
```
- read manual of less command
```
    man less
```
- read information of passwd command
```
    info passwd
```


## 2.Bash
### 2.1 Basic commands
See this Article:
> https://github.com/JiangRenDevOps/DevOpsLectureNotesV6/blob/master/WK5_Linux_Bash_Basics/bash_basic_commands.md

### 2.2 Common tools
- grep
    > https://www.geeksforgeeks.org/grep-command-in-unixlinux/?ref=lbp
- sed
    > https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/?ref=lbp
- awk 
    > https://www.geeksforgeeks.org/awk-command-unixlinux-examples/?ref=lbp
- sort 
    > https://www.geeksforgeeks.org/sort-command-linuxunix-examples/?ref=lbp
- diff 
    > https://www.geeksforgeeks.org/diff-command-linux-examples/?ref=lbp
- uniq 
    > https://www.geeksforgeeks.org/uniq-command-in-linux-with-examples/?ref=lbp

### 2.3 Bash in day-to-day DevOps
- Scenario 1: Securely connect to a remote Linux machine and check the logs
> https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/launching-instance.html
> https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html
> https://docs.aws.amazon.com/managedservices/latest/userguide/access-to-logs-ec2.html

- Scenario 2: Download/Upload file from/to a remote Linux server
> https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html#AccessingInstancesLinuxSCP

- Scenario 3: Check network connectivity on a linux machine
> https://geekflare.com/linux-test-network-connectivity/

- Scenario 4: Setup a daily job on a Linux machine
> https://phoenixnap.com/kb/set-up-cron-job-linux


## 3.Regex
### 3.1 Regex basic
Regular Expressions (regex or regexp) are a very useful tool to identify specific patterns in any text, which helps to extract information regardless the format of the text.
Regex can be used to validate inputs, web scrapping, finding specific strings in documents, syntax validation for compilers, and so many others examples.
Regex is widely used in multiple programming languages using almost the same syntax, so this article pretends to show the basic regex operators.
> https://github.com/JiangRenDevOps/DevOpsLectureNotesV6/blob/master/WK5_Linux_Bash_Basics/regex_basics.md

### 3.2 Regex practice
> https://github.com/JiangRenDevOps/DevOpsLectureNotesV6/blob/master/WK5_Linux_Bash_Basics/regex_practice.md
> https://regexr.com/


## 4.Homework
> https://github.com/JiangRenDevOps/DevOpsLectureNotesV6/blob/master/WK5_Linux_Bash_Basics/homework.md