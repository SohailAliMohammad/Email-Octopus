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


Mail Filters
Global Filters
Global filters affect all maildrops. The configuration is the same for both global and local filters.

<filters>
    <!-- size filter -->
    <filter class="MailFetch.filters.SizeMailFilter" maxsize="1548576" delete="false"></filter>
    
    <!-- sender mail filter -->
    <filter class="MailFetch.filters.SenderMailFilter" delete="true" blocklist="/home/abcd/MailFetch/spool/blocklist" mda="junk"></filter>
    
    <!-- msgid filter -->
    <filter class="MailFetch.filters.MessageIDMailFilter" delete="true">
        <storage name="msgid.cache" limit="8192" destination="spool/msgid.cache"/>
    </filter>
    
    <!-- subject mail filter -->
    <filter class="MailFetch.filters.SubjectMailFilter" delete="true" blocklist="/home/abcd/MailFetch/spool/subject.blocklist" mda="junk"></filter>
</filters>

Local Filters
Local filters affect only the specific maildrop they are associated with.

<maildrop protocol="pop3" mda="smtp">
    <!-- .... standard maildrop config goes here .... -->
    <!-- filters specific to this maildrop -->
    <filters>
        <!-- sender mail filter -->
        <filter class="MailFetch.filters.SenderMailFilter" delete="true" blocklist="/home/abcd/MailFetch/spool/linuxlist" mda="linux"></filter>
    </filters>
</maildrop>

Delivery Agents
Mailbox Delivery Agent

<mda class="MailFetch.delivery.MailboxDeliveryAgent" id="junk">
    <destination>/home/abcd/Mail/junkmail</destination>
</mda>


SMTP Delivery Agent

<mda class="MailFetch.delivery.SMTPDeliveryAgent" id="smtp">
    <host>localhost.localdomain</host>
    <port>25</port>
    <localuser>abcd</localuser>
    <domain>localhost</domain>
</mda>


Null Delivery Agent

<mda class="MailFetch.delivery.NullDeliveryAgent" id="null"></mda>





