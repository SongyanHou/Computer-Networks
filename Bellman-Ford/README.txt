PA3: Distributed Bellman-Ford Algorithm Implementation
Author: Songyan Hou (sh3348)
Date: 12/11/2014

INVOKING FORMAT
This program should be invoked as the format given in the assignment specification.
Sample:
java bfclient 129.236.228.53 4000 3 129.236.228.54 5000 4.0 129.236.228.50 6000 3.0 (client A)
java bfclient 129.236.228.54 5000 6 129.236.228.53 4000 4.0 129.236.228.50 6000 7.0 (client B)
java bfclient 129.236.228.50 6000 4 129.236.228.53 4000 3.0 129.236.228.54 5000 7.0 (client C)

The result is:
      4.0 
    A-----B
    |    /
 3.0|   /7.0
    |  /
    | /
     C



ENCODING FORMAT

Each datagram packet is just for one specific receiver. When sending updated DV information, the client will make a list of different datagram packets and send each of them to corresponding neighbors.

The encoding format of each DV UPDATE message is as follows:

[byte 0--byte 3]: the listening port number of the sender, which acts like sender's ID. It is necessary since the receiver could only get the IP address but not the listening port number of the sender .
[byte 4--byte 7]: the actual cost of the direct link between the sender and the receiver, which is used to recover the real cost between two clients after network condition is changed. (Here is where one packet is different from others in the same client's packet list)

From byte 8: the real distance-vector data, each tuple in the DV table is 20 bytes long.
[byte 0--byte 3]: the IP address of the destination
[byte 4--byte 7]: the port number of the destination
[byte 8--byte 11]: the current estimated cost to the destination
[byte 12--byte 15]: the IP address of the first-hop from the client to this destination
[byte 16--byte 20]: the port number of the first-hop from the client to this destination


Specifically, for LINKDOWN and LINKUP message, the length is just 5 bytes.
[byte 0--byte 3]: the listening port number of the sender, which acts like sender's ID.
[byte 4]: 0 if it is a LINKDOWN message, and 1 if it is a LINKUP message.



ADDITIONAL FEATURES
Besides the basic functions, there are three additional features could be invoked as command in this program:

1. NEIGHBOR
command: "NEIGHBOR" would display all neighbors connected to this client at invoking time, including the IP address, port number and actual cost between two nodes.
2. ADDLINK
command: "ADDLINK IP port cost" would add a new link between the client and the node already in the client's DV table (specified by the arguments of the command). If these two nodes have already been connected as a neighbor to each other, there would be a prompt line declaring this fault and nothing would happen.
3. CHANGECOST
command: "CHANGECOST IP port cost" would change the actual link cost between the client and the neighbor node(specified by the arguments of the command). If this node is not a directly linked neighbor, there would be a prompt line declaring this fault and nothing would happen.
Note: since we are not required to concern about the counting to infinity problem, the CHANGECOST command only takes effects when you decrease the link cost.

For feature 2 and 3, if these commands really take effects, the client would also send DV to all neighbors.