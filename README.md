# CodePathUnit9

# Project 8 - Pentesting Live Targets
Time spent: 55 hours spent in total
> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.
The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation
Each color is vulnerable to only 2 of the 6 possible exploits. First discover which color has the specific vulnerability, then write a short description of how to exploit it, and finally demonstrate it using screenshots compiled into a GIF.
## Blue
Vulnerability #1: SQL Injection (SQLi)
Description:

Select a Salesperson, and test the URL for SQLi vulnerabilities 

When inserting a ' character after the URL

https://35.184.88.145/blue/public/salesperson.php?id=1

We see the error message 

"Database query failed."

And the new URL, 

https://35.184.88.145/blue/public/salesperson.php?id=1%27

Displaying a URL encoded representation of the ' character (%27)

To demonstrate the vulnerability, I used a UNION SELECT to retrieve data from a table in the database 

<img src="blue-vuln1.gif">

Vulnerability #2: Session Hijacking/Fixation
Description:

The blue site does not verify "user-agent" outside the bounds of a single session.
Therefore, a hacker can intercept a users active session and interact with the website using the stolen credentials ( namely the session ID stored in the cookie). 

If we login to the application with the pperson credentials, read the PHPSESSID with developer tools, and use that session id on a different browser that is still on the login page, we are able to hijack that live session. 


<img src="blue-vuln2.gif">

## Green
Vulnerability #1: Username Enumeration
Description:
When a valid  username is entered with an incorrect password, the error message is in bold text. This is no the case for the converse. As a result, a hacker can more easily brute force user credentials. 

<img src="green-vuln1.gif">

Vulnerability #2: Cross-Site Scripting (XSS)
Description:
Within the "Feedback:" field of contact.php, it is possible to execute a <script></script> to cause the page to behave unexpectedly. Unintended behavior could include initiating a popup upon clicking the "submit" button of the contact form.

<img src="green-vuln2.gif">

## Red
Vulnerability #1: Cross-Site Request Forgery (CSRF)
Description:

<img src="red-vuln1.gif">
Vulnerability #2: Insecure Direct Object Reference (IDOR)
Description:
Within salesperson.php, it is possible to manipulate the id value via developer tools in the browser, or through the url. The id value is an integer value. 

<img src="red-vuln2.gif">
## Notes
Describe any challenges encountered while doing the work
I was not able to prove that the Red site does not verify CSRF tokens and I was not able to implement a self-submitting HTML form under user login credentials. I assumed the red site was vulnerable to this attack, as it was the last on the list of vulnerabilities and all others had been found. 
Also, I had encountered three errors across multiple gif creation apps that prevented me from recording/saving gifs of the exploits. I had done the writeup and submitted because I was running out of time. ![image](https://user-images.githubusercontent.com/77745725/112708994-142d2280-8e8c-11eb-8dc9-2d1d41e2bc6c.png)
