### Chapter 1: Sed Syntax and Basic Commands

```
$ vi employee.txt
101,John Doe,CEO
102,Jason Smith,IT Manager
103,Raj Reddy,Sysadmin
104,Anand Ram,Developer
105,Jane Miller,Sales Manager
```

**Basic sed syntax:**
```sed [options] {sed-commands} {input-file}``` Sed reads one line at a time from the {input-file} and executes the {sed-commands} on that particular line.

```sed -n 'p' /etc/passwd```


**Basic sed syntax for use with sed-command file:**
```sed [options] -f {sed-commands-in-a-file} {input-file}```

```
$ vi test-script.sed
/^root/ p
/^nobody/ p
$ sed -n -f test-script.sed /etc/passwd
```

**Basic sed syntax using -e:执行多个命令**
``` sed [options] -e {sed-command-1} -e {sed-command-2} {input-file}```

```
sed -n -e '/^root/ p' -e '/^nobody/ p' /etc/passwd # prints lines beginning with root and nobody
```

也可以分行写

```
sed -n \
-e '/^root/ p' \
-e '/^nobody/ p' \
/etc/passwd
```

也可以用大括号
```
sed [options] '{
sed-command-1
sed-command-2
}' input-file
```

比如
```
sed -n '{
/^root/ p
/^nobody/ p
}' /etc/passwd
```

注意，sed从不修改原始文件


