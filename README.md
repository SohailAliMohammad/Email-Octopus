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

CODE: 
<maildrop protocol="pop3" mda="smtp"> 
<host>mail.somepopserver.com</host> 
<port>110</port> 
<user>myusername</user> 
<password>mypass</password> 
<delete>true</delete> 
<!-- filters specific to this maildrop --> 
<filters> 
</filters> 
[35] 
</maildrop> 
Mailfilters: 
5.3 Global filters 
All filters which are configured outside the maildrop elements are called global filters.These 
filters affect all the maildrops.The configuration is the same for both global and local filters. 
CODE: 
<filters> 
<!-- size filter --> 
<filter class="MailFetch.filters.SizeMailFilter" maxsize="1548576" 
delete="false"> 
</filter> 
<!-- sender mail filter --> 
<filter class="MailFetch.filters.SenderMailFilter" delete="true" 
blocklist="/home/abcd/MailFetch/spool/blocklist" 
mda="junk"> 
</filter> 
<!-- msgid filter --> 
<filter class="MailFetch.filters.MessageIDMailFilter" 
delete="true"> 
<storage name="msgid.cache" limit="8192" 
destination="spool/msgid.cache"/> 
</filter> 
<!-- subject mail filter --> 
[36] 
<filter class="MailFetch.filters.SubjectMailFilter" delete="true" 
blocklist="/home/abcd/MailFetch/spool/subject.blocklist" 
mda="junk"> 
</filter> 
</filters> 
5.4 Local filters 
All filters which are configured inside the maildrop elements are called local filters. These filters 
affect only the maildrop associated with them. The configuration is the same for both global and 
local filters. 
CODE: 
<maildrop protocol="pop3" mda="smtp"> 
<!-- .... standard maildrop config goes here .... --> 
<!-- filters specific to this maildrop --> 
<filters> 
<!-- sender mail filter --> 
<filter class="MailFetch.filters.SenderMailFilter" delete="true" 
blocklist="/home/abcd/MailFetch/spool/linuxlist" 
mda="linux"> 
</filter> 
</filters> 
</maildrop> 
5.5 All filters explained 
FILTER NAME: HeaderMailFilter 
[37] 
DESCRIPTION: Matches a header in the message. This requires the name of the header and the 
value of the header 
CLASS NAME: MailFetch.filters.HeaderMailFilter 
SAMPLE CONFIGURATION: 
<filter class="MailFetch.filters.HeaderMailFilter" delete="true" 
name="X-Spam-Rating" value="SPAM" mda="spambox" > 
</filter> 
5.6 Delivery Agents 
After passing through the filter pipeline, mail is delivered using a DeliveryAgent. Currently we 
provide two main delivery mechanisms: mailbox and smtp. SMTP is the most reliable 
mechanism although it requires that you have an MTA configured for delivery. 
DELIVERY AGENT NAME: Mailbox 
DESCRIPTION: Delivers a message to the specified mailbox. 
CLASS NAME: MailFetch.delivery.MailboxDeliveryAgent 
SAMPLE CONFIGURATION: 
<mda class="MailFetch.delivery.MailboxDeliveryAgent" 
id="junk"> 
<destination>/home/abcd/Mail/junkmail</destination> 
</mda> 
EXPLANATION: The destination element identifies the location of the box where the delivery 
is made. Some basic dot-locking functionality is provided by the mailbox provider to avoid 
multiple access to the mailbox. 
DELIVERY AGENT NAME: SMTP 
[38] 
DESCRIPTION: Deliver the message to a configured SMTP host 
CLASS NAMES: MailFetch.filters.SMTPDeliveryAgent 
SAMPLE CONFIGURATION: 
<mda class="MailFetch.delivery.SMTPDeliveryAgent" id="smtp"> 
<host>localhost.localdomain</host> 
<port>25</port> 
<localuser>abcd</localuser> 
<domain>localhost</domain> 
<user></user> 
<password></password> 
</mda> 
EXPLANATION: The local user element defines who the email is directed to. The domain is 
the domain of the local user. In this case, the email is dispatched to abcd@localhost. User and 
password are used if your server requires SMTP Authentication. 
DELIVERY AGENT NAME: NULL 
DESCRIPTION: A Null Delivery Agent does nothing. So basically equivalent to dumping 
into/dev/null. 
CLASS NAMES: MailFetch.filters.NullDeliveryAgent 
SAMPLE CONFIGURATION: None 
<mda class="MailFetch.delivery.SMTPDeliveryAgent" id="smtp"> 
</mda> 
EXPLANATION: There is no configuration for this delivery Agent. Please use with care, as 
you could very easily lose all your mails due to a misconfiguration. 
