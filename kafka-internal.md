* Cluster Membership - Every broker in a Kafka Cluster has an ID. Every broker register itself to zookeeeper as ephimeral node.
If a new broker try to register with an ID which is already existed it will receieve an error. If a broker loses connectivity
it loses membership from the cluster, howevere the details of partition, topic, replicas that used to reside in this broker
still available in some other datastructure so if a new broker is assigned the same ID and registered in clustered those partitions
will be applied to the broker again.

* Controller - A Controller is a broker that choses leader replica. When Kafka cluster comes up the first broker that gets created
becomes controller. If other brokers tries to become controller they will not become controller. If the broker goes down
other brokers again try to be controller. When a controller notices a broker left cluster and it has leader replicas it 
relect another leader and notifies this information to other brokers to reconfigure follower replicas.

* Replicas - Each partition in Kafka topic can have more than one replicas. Replicas are of two types 
      - Leader Replica
      - Follower Replica
All read and publish request go to leader replica. Follower replicas keep in sync with leader. In case of a failure of leader
replica any of the "in sync" replica can be chosen leader. Follower Replicas send Fetch command to leader replica to get
messages , if leader replica does not recieve fetch command from a follower replica for 10 sec, the follower replica becomes 
"out of sync" . This time is configurable. 
Each partition also has a preffered replics. It is the first leader replica when the partition was created.

* Producing Messages - Producing client produces messages to leader replica. Kafka has configuration to either wait for this
message to propagate to all "in-sync" replicas or only to wait for leader and send ack.

* Consuming Messages - Clients can only recieve messages which are available in all in-sync replicas. This is important for
consistency. If kafka allow only to read messages which are in leader, then if leader replica goes down and that message
hasn't replicated the message is lost. So consumer data consistency depends on replica read lag.
