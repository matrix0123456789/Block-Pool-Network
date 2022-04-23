# Block Pool Network
It's a distributed database with permanent data storage.

Block Pool Network is simmilar to blockchain, it is also a distributed network, so anybody with computer connected to the Internet can be part of network. Like in blcokchain, there is no central authority. Like in blockchain anyone can write some data (signed by digital certificate, so you cannot impersonate someone), data is publicly available and cannot be deleted.

Main difference to blockchain is that Block Pool Network don't care about order of events. If you spend the same coin twice, it's important to tell wchich transaction is valid. But in many cases, when Web3 would be usefull, keeping order of transactions is not needed. When you don't care about order, you don';t need proof of work/proof of steak, you don't need to store all data in every node conected to network, so it allows you to store much more data with less cost.

## Sample use cases
### Web forum with no central authority
You can store messages creating open web forum, when all messages will be keept forever with no ability to censorship,

### Keeping NFT content
In standard NFT you keep in blockchain only link to your content (like image). The risk is, that even if your token is safe in blockchain, server storing your asset can stop working. Storing whole image on blockchain is expensive.

You can link your nft to file stored in Block Pool Network to be shure it wont get lost or changed.

## How it works
### Nodes
Network is made of multiple nodes. Node is server connected to the Internet that runs compatibile software. Network works on HTTPS and WebSocket, so server need to be visible from internet (NAT can be a problem). Every node keeps list of all other nodes with it's adresses and shares this list with others when new node connects.
### Blocks
Block is piece of information that is stored on network.
|Name|Type|Description|
|----|----|-----------|
|ID|SHA512|Hash of rest of the block|
|author|SHA512||
|type|string UTF-8|Mime type of data|
|Tags|array of SHA512|list of other block that are connected|
|Data|any|Accual data|
|Sign||Signature made with author's private key|

ID is created by performing SHA512 hash function on whole rest of block. Using hash serves multiple purporses
1.Prevents collision: one network can be used by multiple people to multiple applications and ID will not collide
2.Giver mostly equal distribution of data
3.Allows to check if server send you block you wanted to read.

### Reading data
You can read data by sending query to any node on the network. It's a good idea to read list of nodes and select random to distribute load.

To read data you need to know ID or one of Tags. Available requests
* GetBlockMetadata - returns block ifnormation, but without data
* GetFullBlock - returns complete block
* FindBlocksByTag - returns metadata of block by this id and all blocks, that contains this id in tags (author's id is also threated as tag)
