# DS-project

Building a multi-server system and multi-server system will:
◦ load balance client requests over the servers, using a redirection mechanism to ask clients to reconnect to another server.
◦ allow clients to register a username and secret, that can act as an authentication mechanism. Clients can login and logout as either anonymous or using a username/secret pair.
◦ allow clients to broadcast an activity object to all other clients connected at the time.

Using TCP socket communicate between Server and Client.
The format of Message is JSON.

The system contains the following commands:

1.AUTHENTICATE
Sent from one server to another always and only as the  rst message when connecting.
example:
    {
    "command" : "AUTHENTICATE",
     "secret" : 
     }
     
Receiver replies with:
• AUTHENTICATION_FAIL if the secret is incorrect
• INVALID_MESSAGE if anything is incorrect about the message, or if the server had already successfully authenticated
No reply if the authentication succeeded.
If anything other than authentication succeeded, then the connection is closed immediately after sending the response.

2.INVALID_MESSAGE
A general message used as a reply if there is anything incorrect about the message that was received. This can be used by both clients and servers.
example:
   "command" : "INVALID_MESSAGE",
   "info" : "the received message did not contain a command"

   
3.LOGIN
Sent from a client to a server.
example:
    {
    "command" : "LOGIN",
    "username" : "ABC",
     "secret" : 
    }
4.ACTIVITY_MESSAGE
Sent from client to server when publishing an activity object.
example:
    {
     "command" : "ACTIVITY_MESSAGE",
    "username" : "ABC",
     "secret" : ,
     "activity" :"..."
    }
5.REGISTER
Sent from client to server when the client wishes to register a new username.
example:
    {
    "command" : "REGISTER",
    "username" : "ABC",
     "secret" : "123"
    }
