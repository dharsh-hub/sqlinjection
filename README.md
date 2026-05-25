### NAME: DHARSHINI S
### REG NO: 212224100012
# EX 8
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
<img width="1658" height="853" alt="image" src="https://github.com/user-attachments/assets/633948af-794a-43cf-802a-3a8d8cbaee6b" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
Select Multidae from the menu listed as shown above. The page is displayed as below:
###  OUTPUT
<img width="1918" height="870" alt="image" src="https://github.com/user-attachments/assets/cf44ba10-1e43-43b6-a9bb-962fc9643e2f" />



Click on the menu Login/Register and register for an account
###  OUTPUT
<img width="1919" height="871" alt="image" src="https://github.com/user-attachments/assets/8073b4fe-8ca7-4ea7-801d-62c025f42073" />



Click on the link “Please register here”
###  OUTPUT
<img width="1918" height="868" alt="image" src="https://github.com/user-attachments/assets/fc817463-a841-4cf4-ac4a-04225923e58b" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:
<img width="1919" height="848" alt="image" src="https://github.com/user-attachments/assets/baad83af-4778-4ef3-bbc4-3100900d8396" />

Union-based SQL injection: UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below:
<img width="1919" height="868" alt="image" src="https://github.com/user-attachments/assets/654900af-865d-407d-b5ef-f2be0790946e" />

<img width="1655" height="854" alt="image" src="https://github.com/user-attachments/assets/ef82c328-039e-41bc-97a3-1586364a9274" />

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
<img width="1822" height="861" alt="image" src="https://github.com/user-attachments/assets/2caa702d-98d2-4de0-b9df-247af710a9cb" />

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.
<img width="1917" height="395" alt="image" src="https://github.com/user-attachments/assets/a9ea3109-a8ce-4a93-a9af-97e72043c7a3" />

The browser url of this info page need to be modified with the url as below: When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.As it is having 5 columns the query worked fine and it provides the correct resultInstead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
<img width="1919" height="868" alt="image" src="https://github.com/user-attachments/assets/dcb2bd9a-e877-42de-ab06-3db47ab30386" />


Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database. The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table. Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
<img width="1884" height="867" alt="image" src="https://github.com/user-attachments/assets/255cb57d-0d23-4886-802c-db6818b5c766" />

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
