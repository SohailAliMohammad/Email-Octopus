# Email-Octopus
Email Octopus is an Android-based bulk email app integrated with Mailgun for 99.9% deliverability. It processes up to 10,000 emails and supports CSV-based recipient selection for up to 5,000 addresses. The app handles various content types, supports simultaneous delivery of 4,000 emails, and enhances marketing reach efficiently.


### Security Requirements

Security systems need database storage just like many other applications. However, the special requirements of the security market mean that the database partner must be selected carefully.

- Passwords will be saved encrypted in the database to ensure the user's privacy.
- The user's IP will be logged.
- The system will be protected against vulnerabilities such as SQL injection attacks.
- Mailgun server authenticates the server using previously made credentials.

### Software Quality Attributes 
The software consists of the following elements:  
1. The SMTP server  
2. The Client application  
3. The Credential database  
4. The database should always remain consistent in case of an error.  

### CODE: 
## Maildrop Configuration

```xml
<maildrop protocol="pop3" mda="smtp"> 
    <host>mail.somepopserver.com</host> 
    <port>110</port> 
    <user>myusername</user> 
    <password>mypass</password> 
    <delete>true</delete> 
    <!-- filters specific to this maildrop --> 
    <filters> 
    </filters> 
</maildrop>
