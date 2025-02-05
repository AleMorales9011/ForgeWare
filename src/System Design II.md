# Glossary

# Basics
Client: A machine that requests data from a server.
Server: A machine that provides data.
Client-Server Model: A paradigm of data transmission.
IP: Internet protocol
IP Adress: Internet Protocol adress.
Port: Network connection channel
DNS: Domain name system.
TCP: Network protocol built on top of the IP protocol that allows data transfer through a connection.
HTTP: Hypertext transfer protocol is a network protocol based on requests and responses.

Request Schema 
host: string
port: integer
method: string ( GET, POST, PUT, DELETE, OPTIONS, PATCH)
headers: pair list ( "Content-Type" => "JSON" )
body: opaque sequence of bytes 

Response Schema
status code: inerger ( 200, 400 )
headers: pair list ( "Content-length" => 1238 )
body: opaque sequence of bytes

# Networking

IP Packet: A data package.
Databases: Data storage
Disk: A data container
RAM: Random Access Memory. Temporary data storage.
Latency: Time to complete a system operation.
Troughoutput: Number of operations that a system can handle per time unit.
Availability: Odds of as server being up and running.
Redundancy: To replicate parts of a system to make it reliable.
SLA & SLO: Service level agreement, and Service level objective.

# Caching
Cache: A data storage built for quick data retrieval. 
Cache Hit: request data is in cache
Cache Miss: request data isn't in cache.
Cache Eviction Policy: The policy by wich values are removed from cache.
CDN: 












