# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
#OUTPUT
<img width="715" height="398" alt="1" src="https://github.com/user-attachments/assets/ebc07d0a-9c66-467d-94a6-3d529689511b" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
##  OUTPUT
<img width="1271" height="788" alt="2" src="https://github.com/user-attachments/assets/77cf1f18-e3cf-4c31-b926-63612775120d" />


Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT

<img width="995" height="917" alt="3" src="https://github.com/user-attachments/assets/e28899b8-4eaf-48b5-b8f2-98b4bfc6cf1e" />


Click on the menu Login/Register and register for an account
##  OUTPUT
<img width="1255" height="766" alt="Screenshot 2025-10-30 090346" src="https://github.com/user-attachments/assets/d03e6ca4-4ff1-46c3-ac68-7070efdca048" />


Click on the link “Please register here”
##  OUTPUT
<img width="1235" height="844" alt="7" src="https://github.com/user-attachments/assets/8f7b0757-8702-4c4d-b4e9-00db370e46b4" />



Click on “Create Account” to display the following page:
##  OUTPUT
<img width="1263" height="756" alt="6" src="https://github.com/user-attachments/assets/d31c4ed1-96b4-4358-be23-e37d4c3d0edd" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:


($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
##  OUTPUT
<img width="1235" height="844" alt="7" src="https://github.com/user-attachments/assets/a259a055-c29c-4851-bc54-78e14cf8f4ef" />



Click “Login”. The logged in page will show as below:
##  OUTPUT


<img width="992" height="917" alt="4" src="https://github.com/user-attachments/assets/72faf406-4eec-4574-b61e-0c6128b660e5" />

If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:
##  OUTPUT
<img width="1297" height="756" alt="8" src="https://github.com/user-attachments/assets/409f1b9a-8a35-4c1e-ae00-32caca20d3c1" />


Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure
##  OUTPUT




Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload
##  OUTPUT




# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.
##  OUTPUT





# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 
#OUTPUT



Now after logging out you will see the login page. In the login page give ganesh’ # (myusername). You can see the page now enters into the administrator page as before when giving the password.
#OUTPUT


Click the login button and you will see it enter into the administrator page.
#OUTPUT



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT

<img width="1254" height="626" alt="9" src="https://github.com/user-attachments/assets/66859e51-8114-4a32-99a1-bf1098a5bc0b" />


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT

<img width="1002" height="740" alt="10" src="https://github.com/user-attachments/assets/08696ce2-ba50-4a40-9fee-f0a10215ac5f" />


Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
##  OUTPUT


<img width="1002" height="710" alt="11" src="https://github.com/user-attachments/assets/4fe0ec4f-3c61-45d9-9c98-7ca9ad662340" />


After adding the order by 6 into the existing url , the following error statement will be obtained:


##  OUTPUT

<img width="1245" height="709" alt="12" src="https://github.com/user-attachments/assets/8147c1f2-9f9a-4f23-990a-0a192efea3b2" />


## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).


##  OUTPUT
<img width="1257" height="706" alt="13" src="https://github.com/user-attachments/assets/afd51a04-8490-4551-b5f2-bd17c5769d12" />


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
