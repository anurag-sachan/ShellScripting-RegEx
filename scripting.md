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

NOTE: 
#grep, awk, sed uses POSIX way [[:digit:]]
#python, js, vim uses perl-styled regex "\d"

Examples:
#\b inside grep regex marks word boundary and \w selects line with atleast 1 word, ex:
grep -e "\ba\b|\ban\b|\bthe\b" poem -v | grep -e "\w | wc -l"

#egrep is deprecated used grep -E instead
#lower array for list of files with 4 digit, 6 hexadecimal w. lowercase
lower=(`ls | grep -E "[[:digit:]]{4}[[:xdigit:]]{6}" | grep -E "[[:lower:]]"`)

check if user has read perms:
if [[ $(ls -l $1 | grep -e "-r--------*") ]]
then
 echo "yes"
fi

if two args is provided, add else return Error
#space in the if condn is also v. important
if [ $# != 2 ]
then
 echo Error
fi
if [ $# = 2 ]
then
 echo $(($1+$2))
fi

#o-flag displays only the matched 
#here -o pull off the pincode then cut -c1 exact first number
pattern instead of whole line
#from pincode.csv extract pincodes starting and ending with same number
number=`grep -E -i "$state" pincode.csv | head -1 | grep -E -o [[:digit:]]{6} | cut -c1`
grep -i "$state" pincode.csv | grep -E -o "$number[0-9]{4}$number"

#NOTE
=~ matches regex in bash

#last line num count
sed -n "\$="

#print lines btw FROM and T, then remove FROM and TO
#comma is for range
sed -n '/FROM/,/TO/p' file.txt | sed '/FROM/d' | sed '/TO/d'

#sed
#mostly use for replacing strings
sed 's/old_string/new_string' file.txt

#replace 2nd occurence, /g to replace all
#2g to replace all the occurence from 2nd, 3rd, 4th ... so on.
sed 's/old_string/new_string/2' file.txt

#restrict the command usage to line 3
sed '3 s/old/new' file.txt
#works with range of line numbers
sed '1,3 s/old/new' file.txt
#$ indicates the last line
sed '1,$ s/old/new' file.txt

#p flag prints the line twice in the terminal after execution, else once
sed 's/old/new/p' file.txt

#n flag solves this by supressing duplicated lines & prints only the replace line, but it works with /p
sed -n 's/old/new/p' file.txt

#delete w. sed
#5th line
sed '5d' file.txt

#last line
sed '$d' file.txt

#range
sed '2,5d' file.txt

#awk - manipulating data and generating reports
#similar to cat file.txt
awk '{print}' employee.txt

#search w. keyword
awk 'manager {print}' employee.txt

#print specific columns
awk '{print $1, $4}' employee.txt

#display line numbers
awk '{print NR, $0}' employee.txt

#display last fields
awk '{print $1, $NF}' employee.txt

#sum of all fields
BEGIN{
FS=",";
sum=0;
}
{
sum=sum+NF;
}
END{
print sum;
}

#function w. awk
#multi-option file analyzer
myCount(){
filename=${@: -1} #last argument

while getopts "wlns:" options; do
    case "${options}" in
        s)
            str=${OPTARG}
            grep $str $filename | awk "END{print NR}";;
        w)
            awk "BEGIN{c=0} {c+=NF} END{print c}" $filename;;
        l)
            awk "END{print NR}" $filename ;;
        n)
            awk "BEGIN{c=0} /^[[:digit:]]+\$/{c++} END{print c}" $filename ;;
        *)
            echo "ERROR" ;;
    esac
done
}