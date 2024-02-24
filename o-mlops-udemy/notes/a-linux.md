## Linux Essentials

ls
ls -l
ll
cp
mv

* File Permissions
1) -/d -> - means file and d means directory
2) rwx -> read, write and execute permissions for super user
3) rw- -> read and write permissions for owner of the file
4) r-- -> read only permissions for others
5) chmod to update permissions r=4, w=2, x=1
we can sum . Lets say - rwx rwx rwx. That means chmod 777 file.txt
eg 
Permissions size Username Groupname 
drwxrwxr-x  2 ravi0531rp ravi0531rp 4096 Jan 30 00:19 ./

Lets break drwxrwxr-x
d -> directory
rwx for root user
rwx for groups
r-x for any other user

```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ ls -l
total 4
-rw-rw-r-- 1 ravi0531rp ravi0531rp 31 Jan 30 01:56 test.txt
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ chmod 400 test.txt 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ ls -l
total 4
-r-------- 1 ravi0531rp ravi0531rp 31 Jan 30 01:56 test.txt
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ chmod 777 test.txt 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ ls -a
.  ..  test.txt
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ ls -l
total 4
-rwxrwxrwx 1 ravi0531rp ravi0531rp 31 Jan 30 01:56 test.txt
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ 

```