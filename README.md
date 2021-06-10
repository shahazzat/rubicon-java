# rubicon-java
A bridge interface between Python and Java.

## Environment Preparation
1. Centos7

## Source Code Preparation and Build
1. Install Python
```
$ sudo yum -y update
$ sudo yum -y groupinstall "Development Tools"
$ sudo yum -y install openssl-devel bzip2-devel libffi-devel

$ gcc --version
gcc (GCC) 4.8.5 20150623 (Red Hat 4.8.5-39)
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

$ sudo yum -y install wget
$ cd /var
$ wget https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz

$ tar xvf Python-3.8.3.tgz
$ cd Python-3.8*/

$ ./configure --enable-shared
$ sudo make altinstall
$ readlink -f $(which python3.8)
/usr/local/bin/python3.8
```
**Note:** If you install python by following above process then you will face below issue. To fix this, you need to execute below command.
```
$ ./configure --enable-optimizations
```
If you use above command at the beginning then you might face below issue.
```
/bin/ld: /usr/local/lib/libpython3.8.a(abstract.o): relocation R_X86_64_32S against symbol _Py_NotImplementedStruct' can not be used when making a shared object; recompile with -fPIC
/bin/ld: /usr/local/lib/libpython3.8.a(boolobject.o): relocation R_X86_64_32 against .data' can not be used when making a shared object; recompile with -fPIC
```

Reference: [Install Python 3.8 on CentOS 7 / CentOS 8](https://computingforgeeks.com/how-to-install-python-3-on-centos/)

2. Install JAVA
```
$ yum install java-devel
$ whereis java
java: /usr/bin/java /usr/lib/java /etc/java /usr/share/java /usr/share/man/man1/java.1.gz
$ readlink -f $(which java)
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.292.b10-1.el7_9.x86_64/jre/bin/java
```

3. Get rubicon-java source
```
$ cd <project_dir>
$ git clone https://github.com/beeware/rubicon-java.git
```
4. Modify MakeFile

Check line 7 and 52 from above [MakeFile](https://github.com/shahazzat/rubicon-java/blob/master/Makefile)
```
PYTHON_CONFIG := "/usr/local/bin/python3.8-config"
JAVA_HOME := "/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.292.b10-1.el7_9.x86_64"
```
5. Build
```
$ make
```
This command will generate following files under build directory.
```
-rwxr-xr-x  1 root root 132760 Jun  9 03:27 librubicon.so
-rw-r--r--  1 root root   2423 Jun  9 03:27 rubicon.jar
-rw-r--r--  1 root root   8380 Jun  9 03:27 test.jar
```

That's all.
