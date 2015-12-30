- It is not because you installed a Name Server the Operating System knows how to use it - You have to let your O.S. know you want to use your local server
- If you use tags and just install the Bind NameServer, without further configuration, and the machine(s) is available on the internet, your system may be abused, as an 'Open Resolver'. Control who can make recursive queries to your systems.
- A TTL of Zero (0) seconds is supported, since it is described on one of DNS RFCs, but not all systems handle this well. To be safe, if you need very low TTLs, use 1 second.

