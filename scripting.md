#current shell, pid, flag
#incomplete
$SHELL
$$

#current-user
whoami

#working directory
pwd

#location where command is located
which java

#create file
touch file.txt
#create multiple file
touch 1.txt 2.txt
#copy file
cp file.txt file2.txt
#copy file content from file1 to file2
cp file1.txt file2.txt
#move file
mv file.txt dir2/filemv.txt
#remove file
rm file2.txt
#remove multiple files
rm file1.txt file2.txt
#create directory
mkdir dir1
#create multiple directory
mkdir dir1 dir2
#move directory
mv dir1 dir2
#remove directory
rm -rf dir2
#remove multiple directory
rm -rf dir1 dir2

#list all the files
ls
#list all the files w. permissions and other-info
ls -l
#list all the files + hidden files with all details
ls -la

#permissions
#symbolic method
# r/w/x u/g/o +/-
# execute permission to all
chmod +x file1.txt
# execute permission from group & others
chmod go-x file1.txt

#numerical method
#4-read, 2-write, 1-execute
chmod 655 1.txt

#status code
#0 - success #127- command not found
$?

#if-condition
#-eq is equal operator
if [ $? -eq 0 ]
then
 echo "success"
 exit 0
else
 echo "command not found"
 exit 127
fi

#log output to file
echo "over-write" > file.txt
echo "append" >> file.txt

#lines count
wc -l file.txt

#tee (append) command
wc -l file.txt | tee -a file.txt

#count files
ls | wc -l

#count files and directories inside directory
ls -RA | wc -l

#read from top (n-lines)
head -n 5 file1.txt

#read from bottom (n-lines)
tail -n 5 file1.txt

#count/read from multiple files
cat file1.txt file2.txt | wc -l

#use head-tail together
head -n 2 file1.txt | tail -n 1

#grep
#find lines in the file with word
grep "word" file.txt

#find lines in the file without word
grep -v "word" file.txt

#find recursively in files
grep -r "word" file.txt

#case-insensitive
-i

#no of occurences
-c

#file-name of the occurences
-l

#line-number of the occurence
-n

#start&end
"^$"

#for multiple search
-e "search1" -e "search2"

#search using file
grep -f pattern.txt 1.txt

Examples:
check if user has read perms:
if [[ $(ls -l $1 | grep -e "-r--------*") ]]
then
 echo "yes"
fi

if two args is provided, add else return Error
if [ $# != 2 ]
then
 echo Error
fi
if [ $# = 2 ]
then
 echo $(($1+$2))
fi