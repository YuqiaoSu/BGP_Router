##### Higher Approach: 

This program follows the routing protocols given on the website (mixed version of inter-domain and intradomain). First of all, the all program is based on the ROUTER class that contains all functions and processes the data transmitted and forwarding table. When all routers are set up, they will first send their handshake message and then start to update. The update mechanism is based on the local preference and AS Path. By utilizing the given information, they will figure out their path to another router. Each router will broadcast its information and rebroadcast information from other routers (except the sending port). Each time a router receives the updated information, the forwarding table will be updated. When dealing with the withdrawing message of some routers, the forwarding table of this router will be updated also and rebroadcast this withdrawing information. For dealing with data redirecting routing, the forwarding table will be used. When receiving data from a peer or a provider, the packet will be dropped as received. If receiving from customers, figure the output in the forwarding table (if cannot be found in the forwarding table, send it back to the source). Besides using the forwarding table, the table's queries will be aggregated if it is possible with all local preferences, self-origin, as path, origin, and source are all the same with subnet mask and IP address on those subnet masks. At last, when receiving the dump message, the program will send the forward table to the source to check the correctness of the forward table. 

##### Challenges Faced:

Figuring out the correct forwarding table that has aggregation functionality is the hardest part of this project. Since the logic is very clear and a little bit complex, the debugging process is much harder as each part is nesting with the other. It took us a long time to figure out the place of the bug and how to solve it without changing other parts' functionality. The forwarding result will be mixed after aggregating which means harder in finding the part that causes the problem. 

What's more, the CIDR aggregation check is complicated. It requires multiple indexes' check on different things, like some indexes should be all the same and some indexes should be partly the same (like subnet mask place). A small mistake will cause the whole forwarding mechanism to fail. 

##### Good Design:

Since this program builds on methods inside the ROUTER class, it makes all methods distinct with their functions without mixing. The mechanism of creating the forwarding table is straightforward and efficient, especially on the CIDR aggregation check part. 

##### How We Test:

Print out the message and our forwarding table to figure out the mistake made during making the forwarding table (mainly as using the log as the debug tool). Also, use the given configs to test each of them for different conditions. 
