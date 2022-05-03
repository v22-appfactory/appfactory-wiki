# SMTP Server
A smtp.js module handles the sending of emails to the appropriate SMTP server.  In a development environment 
(environment variable VUE_APP_MODE === 'DEV') the email is sent to the Ethereal server and in production the email is
sent to the specified production SMTP server.
### Ethereal Server
The Ethereal [https://ethereal.email/] server is a fake SMTP service where messages are never delievered.  This is used
in a development environment and allows testing of the construction of an email allowing the email to be viewed 
the need for a real SMTP server.  After using the sendMail method it is possible to retrieve the URL for the email
and view the email on the Ethereal server.
``` javascript
const transporter = nodemailer.createTransport(mailConfig);
transporter.sendMail(emailObj)
  .then(info => {
    console.log('Message sent: %s', info.messageId);
    console.log('Preview URL: %s', nodemailer.getTestMessageUrl(info));
   }); 

Message sent: <b431f65f-041d-45f7-d959-048badffe1b3@navy.mil>
Preview URL: https://ethereal.email/message/Xac9bXdneCuiu6KVXac9b9dc9CwJd9zFAAAAAcB.pSyEJSp.CGgnHOB6y3s
```
[[/images/email/ethereal sample.png|Work Request Maintenance - Edit Mode]]   
 
### Production SMTP Server
__TBD__

