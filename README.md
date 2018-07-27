# DS-project

<p>Building a multi-server system and multi-server system will:</p>
<ul>
	<li>load balance client requests over the servers, using a redirection mechanism to ask clients to reconnect to another server.</li>
	<li> allow clients to register a username and secret, that can act as an authentication mechanism. Clients can login and logout as either anonymous or using a username/secret pair.</li>
	<li>allow clients to broadcast an activity object to all other clients connected at the time.
	</li>
</ul>

Using TCP socket communicate between Server and Client.
The format of Message is JSON.

The system contains the following commands:

<ol>
<li>AUTHENTICATE</li>
Sent from one server to another always and only as the  rst message when connecting. <br>
example:
    {
    "command" : "AUTHENTICATE",
     "secret" : 
     }
     
Receiver replies with:
<ul>
	<li>AUTHENTICATION_FAIL if the secret is incorrect</li>
	<li>INVALID_MESSAGE if anything is incorrect about the message, or if the server had already successfully authenticated</li>
	<li>No reply if the authentication succeeded.</li>
</ul>
If anything other than authentication succeeded, then the connection is closed immediately after sending the response.



<li>INVALID_MESSAGE</li>
A general message used as a reply if there is anything incorrect about the message that was received. This can be used by both clients and servers.<br>
example:
   "command" : "INVALID_MESSAGE",<br>
   "info" : "the received message did not contain a command"



   
<li>LOGIN</li>
Sent from a client to a server.<br>
example:
    {
    "command" : "LOGIN",
    "username" : "ABC",
     "secret" : 
    }
	
	
	
<li>ACTIVITY_MESSAGE</li>
Sent from client to server when publishing an activity object.
example:
    {
     "command" : "ACTIVITY_MESSAGE",
    "username" : "ABC",
     "secret" : ,
     "activity" :"..."
    }
	
	
	
<li>REGISTER</li>
Sent from client to server when the client wishes to register a new username.<br>
example:
    {
    "command" : "REGISTER",
    "username" : "ABC",
     "secret" : "123"
    }
</ol>
