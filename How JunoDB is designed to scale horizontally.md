[[Overview of JunoDB - an open source KV store by PayPal]]
[[High level architecture and System Design of JunoDB]]
- Why JunoDB needs to scale?
	- as number of microsevices increase
		- the number of inbound connection increase --->network
		- the amount of data to be stored increases ---> storage
		- the no. of reads and write increases
- scaling connections
	- to scale the number of connection JunoDB can handle, we can add more Juno Proxy. Load baalancer is scalable and so is proxy
	- [[JunoDB.excalidraw#^OpY86mPW]]
-  scaling Data
	- As data grows, it is essential to and more storage servers
	- JunoDB fixes the no. of partitions (say 1024)
	- and these are distributed across physical storage servers
- How do we know which shard is on which storage server ?
	- the mapping is stored on ETCD running on Juno Proxy
	- ETCD is a strongly consistent KV store
	- Such that each node where it is running
	- sees the same view of data
	- 