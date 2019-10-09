---
title: Security
author: rxcontributorone
category: rxwebcore core
---

Security measures right from the initial stage of developement are much necessary in web development for maintaining a level of confidentiality and preventing the resources and corporate data from attacks like XSS(Cross-site scripting) and SQl injection, providing better access control using authentication and authorization in the application for identifying the user and give access accordingly.

rxwebcore follows top OWASP security standards. OWASP(Open Web Application Security Project) is an organization with focuses on software security.

According to it, there are application security verification standards which provide a basis of testing web application technical security controls and also provides list of requirements for secure development. Some of them are listed below:

# Injection:
1) SQL Injection:
It is done by using parameterized query while using Entity framework where a direct sql query must be used. 

2) OS Injection: 
Operation system injection is prevented using `System.Diagnostics.Process` to start process.

# Broken Authentication:
It is prevented by using secure password hashes having salt key and setting cookie policy.

# Sensitive Data Exposure
It prefers using store hash to store password, allow SSL and ensure http headers doesn't disclose any information.

# Broken access control
1) Weak account management
Ensure that cookies are sent via HTTPs, reduce session timeOut, protect logIn, Registration methods from bruteforce attack and use reCaptcha.

2) Missing function level access control
Implementing Authorization using access in controllers.

# Security Misconfiguration
1) Debug and Stack trace
Http redirection, debug and trace are off in production.

# Using components with known vulnerablities
Keeping the .NET framwork updated with latest patches, NuGet updates


