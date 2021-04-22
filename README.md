## My attempt at learning about peer to peer file system in rust

Steps to secure file data in a peer to peer system (Because everyone has access to every files)

* Encryption
* File splitting/ Sharding

#### Encryption
* If owner doesnt have their own key, generate one (CLient side encryption/ symmetric encryption)


If somebody has access to our symmetric key; file sharding is gonna prevent the access

Generate File shard unique name based on hash of content

the process goes like this:

1. Encrypt file
2. Shard file
3. Send

Use a manifest file to preserve order of file content(shards)

* write shard ids to manifest files
* also keep filename and file info (to check file integrity later)


## Distribute shards (file loads across multiple nodes)

* Maintain a list of nodes and iterate through it to share files (All nodes are master on its own(they all need a node list on their own))
* what if million nodes?

Give ids to nodes like shards

Send shards to the closest nodes id'd to the original shard id

Logical closeness = `shard id's ` *closeness* to a `node id's` **XOR distance** .

Kademlia distributed hash table[DHT]

[Rust impl](https://docs.rs/kademlia-dht/1.2.0/kademlia_dht/)

How kademila works?

We now have small node lists (Log(n sized))


End result:

* upload file through command line utility to the network
* generate shards locally
* shards are encrypted
* Delete file locally
* get manifest file path from the cli tool 
* use cli tool and manifest file to download all shards
* get the original file

References:

* [Layr project](https://layr-team.github.io/layr-project/)
* [NodeSF Talk](https://www.youtube.com/watch?v=8sN3cT5T-5g)