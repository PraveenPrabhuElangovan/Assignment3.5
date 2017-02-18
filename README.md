1)High availability of Namenode:
The main motive High Availability project is to render availability to big data applications 24/7 by deploying 2  Hadoop NameNodes –One in active configuration and the other is the Standby Node in passive configuration.
Earlier there was one Hadoop NameNode for maintaining the tree hierarchy of the HDFS files and tracking the data storage in the cluster.
With Hadoop  High Availability, the complete Hadoop Stack i.e. HBase, Pig, Hive, MapReduce, Oozie are equipped to tackle the NameNode failure problem- without having to lose the job progress or any related data. Thus, any critical long running jobs that are scheduled to be completed at a specific time will not be affected by the NameNode failure.

2)Check pointing in Hadoop:
	A Checkpoint Node was introduced to solve the drawbacks of the NameNode. The changes are just written to edits and not merged to fsimage during the runtime. If the NameNode runs for a while edits gets huge and the next startup will take even longer because more changes have to be applied to the state to determine the last state of the metadata.
The Checkpoint Node fetches periodically fsimage and edits from the NameNode and merges them. The resulting state is called checkpoint. After this is uploads the result to the NameNode.
There was also a similiar type of node called “Secondary Node” but it doesn’t have the “upload to NameNode” feature. So the NameNode need to fetch the state from the Secondary NameNode. It also was confussing because the name suggests that the Secondary NameNode takes the request if the NameNode fails which isn’t the case.

3)HDFS federation:
	Let HDFS contain two sub-directories in the root directory. 
1)	/usr /share 
•	In the HDFS Federation, there are multiple NameNodes, each storing the metadata and block mapping of files and directories contained in particular sub-directories.
•	The list of sub-directories managed by a NameNode is called a namespace volume. 
•	Blocks for files belonging to a namespace is called a block pool. For example, here we can have two namenodes, one for storing the metadata and block mapping for namespace volume /usr and one for /share. 
•	This way, if one NameNode fails, a namespace volume managed by an other namenode is still accessible. So the entire cluster doesn’t become inaccessible.
4)Configurations of Hadoop: 
•	Hadoop comes up with default configurations in *-default.xml. For example: hdfs-default.xml, yarn-default.xml, etc.
•	Default configurations are overridden in *-site.xml. For example: hdfs-site.xml, yarn-site.xml, etc
Other configurations to be check:
•	dfs.replication.max 
•	dfs.namenode.replication.min 
•	dfs.blocksize 
•	dfs.heartbeat.interval 
•	dfs.hosts 
•	dfs.hosts.exclude 
•	dfs.bytes-per-checksum 
•	dfs.namenode.checkpoint.dir 
•	dfs.namenode.checkpoint.edits.dir 
•	dfs.namenode.checkpoint.period 
•	dfs.namenode.checkpoint.txns 
•	dfs.namenode.checkpoint.check.period 
•	dfs.namenode.checkpoint.max-retries 
•	dfs.namenode.num.checkpoints.retained
•	dfs_replication

