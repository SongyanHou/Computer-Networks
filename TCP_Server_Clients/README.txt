Author: Songyan Hou
UNI: sh3348
E-mail: sh3348@columbia.edu

a. 
There are two programs called Server.java and Client.java here, which represents the server and client separately. The core design methodology is using multi-threaded programming. 

Each time a server wants to build up a connection, the server create a new thread to communicate with this new client, and the listening server thread keeps listening other requests. All the requirements and command functions are realized in the server program.

For the client part, we just need two threads, one of which reads the information sent from the server, and another one reads the information from keyboard input and send them to the server.


b.
I built up the whole program on Mac OS 10.9.4. 
The tool I use is Eclipse(Android Developer Tools). Tests are made on terminals.
Java version "1.6.0_65"
Java(TM) SE Runtime Environment (build 1.6.0_65-b14-466.1-11M4716)
Java HotSpot(TM) 64-Bit Server VM (build 20.65-b04-466.1, mixed mode)


c.
First, type in “make”, using “Makefile” to build the whole project.
Then you will have two .class file. Run these file using command "java". Run server program first, then you could run as many client programs as you want.
(1) java Server 6066 (here 6066 is the port number on which the server socket listens)
(2) java Client 192.168.0.16 6066 (the first argument is the IP address of server, the second argument is the port on which server socket listens)
After typing in these commands, the client and server will begin to run, the user_pass.txt file would be read by server, and the connection will be made.


d.
Operated in time series:

make
Server host: java Server 4119 (IP address of the server 127.12.09.109)
Client host 1: java Client 127.12.09.109 4119
Client host 2: java Client 127.12.09.109 4119
Client host 3: java Client 127.12.09.109 4119
Client host 4: java Client 127.12.09.109 4119
......
(Note: the operations of client hosts could be parallel.)


e.
I add three additional functions into this program.

(1) Read offline messages: when a new user logs in, he could choose the command "readoffmes" to read offline message, which are sent to this user before he logged in. Just type in "readoffmes", and the client terminal will display the sender's name and the content of this message.

(2) Clear offline messages: When a logged in user has already read the offline messages, he might want to delete them to save memory space. Then he could type in "clearoffmes" to delete the offline messages sent to him. However, other offline messages which were sent to others will not be influenced.

(3) Read broadcast history: If a user wants to check what has been broadcasted before, he could type in "readbchis" to see the sender's name and the messages broadcasted.