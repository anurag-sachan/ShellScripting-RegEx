https://regex101.com/

1. format of regex 
/xyz/

2. make it global, by default it only finds 1st pattern
/xyz/g

3. case insensitive 
/xyz/gi

4. match atleast 1 e
/e+/g

5. optional
/e+w?/g

6. * = combination of ? and + i.e., if it exists it can be any in number
/ew*/g

7. match anything with period(.) except new line
/ew./g

8. how to match normal period? using backslash
/\./g

9. any word & v-v
/\w/g /\W/g

10. any whitespace & v-v
/\s/g /\S/g

11. search any word with length. ex: 2 or more
/\w{2,}/g

12. grouping. ex: anything with f or c
/[fc]at/g

13. also works with ranges
/[a-zA-Z0-9]/g

14. OR
/(z|Z)od/g

15. OR with length. ex: either L or O occur 3 or more times
/(l|o){3,}/gi

16. ^startsWith but use /m for covering multiple lines
/^I/gm

17. $ marks the end of the line but use it with /m for prior reason.
/\.$/gm

18. anything before at
/.(?=at)/

19. anything after The for ex. & ! for not
/(?<=[Tt]he)./g 


EXAMPLES:
10 digit MobNo: 
1234567890 /\d{10}/g
123-456-7890 /\d{3}-?\d{3}-?\d{4}/g
123 456 7890 /\d{3}[ -]?\d{3}[ -]?\d{4}/g

how to capture 3 sets of digits and make it to simple format, use parenthesis: () and use $1 $2 $3 for reference
/(\d{3})[ -]?(\d{3})[ -]?(\d{4})/g
$1$2$3

no capturing group(?:) : (?:(\+1)[ -])? for ex: +1 123 456 7890

