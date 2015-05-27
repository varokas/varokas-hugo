+++
categories = []
date = "2015-05-19T23:08:36-07:00"
description = ""
keywords = []
title = "Cloud Data Architecture and CAP Theorem"
+++

I always think of Software architecture as making an energy transfer. When we are designing to gain something, we lose something else in the process. Nothing shows this better than the [CAP Theorem](http://en.wikipedia.org/wiki/CAP_theorem), which has recently been quite popular criteria for selecting NoSQL databases for storage in the cloud.
<!--more-->

## CAP Theorem

It states that all distributed system can provide _only_ two of these three properties.

__Consistency__ All nodes see the same thing

__Availability__ When we ask the system, It readily answers

__Partition Tolerance__ When parts of the system fails, it can still operates

Let's try that with data storage system.

## C and A
Example: Traditional SQL Database

![](/images/2015/database.png)

[C] Easiest way to make sure our data is consistent? Put it all in one giant centralized bucket.

[A] No wonder why we call it "database". It's a base for all our data! This implies availability in a sense that our only node are always in contact with the client.

[P] One server to do it all is well and good until we have a problem at that only node and we'll lose a few hours while we bring up the node again.

## A and P
Example: Cassandra

![](/images/2015/ap.png)

It's easy to spot an AP system. Look for "Eventually Consistent" in the documentation. Cassandra default operation is to write to one node. The data will later be replicated to other nodes in the background.

[C] If a client reads from any available node. The client can, undesirably, read before replication finishes. What is read might not be up to date.

[A] Nothing is stopping us from reading data from any nodes at any time. So the data is highly available to the client.

[P] is great here because one of replicated nodes can be taken away and others can readily step in place.

## C and P
Example: HBase

By default HBase make sure all writes are acknowledged first before sending ok back to the client.

![](/images/2015/cp.png)

[C] After the system give the client an "okay". It means the read will be consistent as all node are acknowledged of that same data.

[A] Not that great. The client cannot proceed with that node until the data is acknowledged.

[P] The nodes that are down can also taken over by other nodes.

## Look for what is missing
When designing a distributed system or storage, keep CAP theorem in mind. It will help us be aware of what is being sacrificed while pursuing other qualities. It is natural for our architecture to have a drawback. We just need to make sure it is intentional, not accidental.
