# ConsoleChat

A simple terminal based chat program

---

The idea I have for implementing the application is as follows

```mermaid
---
title: Chat Server
config:
    look: classic
    theme: dark
---
flowchart TD
    A("`Listening thread`")
	B("`Activity thread`")
	
	A --> C["`Wait for new
	connection`"]
	C --> D["`Add connection 
to list of users`"]
	D --> E["`Check to see if a client has
 sent a msg via select`"]
	E --> F{"`No activity, 
 Msg recieved,
 Error`"}
	F -->|no activity| C
	F ---|msg Recieved| B
	F -->|Error| G[/Error handling/]
	
	B --> H["`Relay message to all clients`"]
	H --> I["`Kill the thread`"]
	
```

---

I was thinking of implementing it in a way where the client AND server are integrated into one .exe.<br>
To determine which one launches, I was thinking about using argument flags and or startup user input for it<br>
i.e. `consolechat.exe --server --port 7777 -p SuperSecretPassword` would start a server on port 7777 with the password of 'SuperSecretPassword'.<br>
Another idea I was thinking about for security is using a config file with most of the secrets inside it.<br>
For example `consolechat.exe -c path/to/some.conf` and `some.conf` would contain the flags separated by spaces or newlines.<br>
