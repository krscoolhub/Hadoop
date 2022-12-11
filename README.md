# Hadoop
 # [1] HDFS:
HDFS (Hadoop Distributed File System) is a distributed, scalable, and fault-tolerant file system designed to store data on low-cost commodity hardware. It is part of the Apache Hadoop project and provides a reliable and distributed way of storing data across a cluster of machines. HDFS is designed to be highly fault-tolerant and can store very large amounts of data reliably, even in the case of individual machine failures. This makes it well-suited for use in large-scale, data-intensive applications such as data lakes and big data analytics.



 # [2] Hdfs rack Awareness:
HDFS Rack Awareness is a feature that enables HDFS to optimize data storage across a cluster of machines by taking into account the physical layout of the machines in the cluster. This is important because when data is written to HDFS, it is replicated across multiple machines for fault tolerance. With HDFS Rack Awareness, the system is able to intelligently place the replicas of a block of data on machines that are in different racks, rather than on machines that are all in the same rack. This helps to improve the overall fault tolerance and availability of the system, because if an entire rack of machines fails, the replicas of the data will still be available on machines in other racks.




# [3] HDFS write request:
When a client application wants to write data to HDFS, it sends a write request to the NameNode (the master node in an HDFS cluster). The NameNode then determines the best way to store the data based on the available space on the DataNodes (the worker nodes in an HDFS cluster), the replication factor, and other factors. The NameNode then sends instructions to the DataNodes, telling them where to store the data. The DataNodes then receive the data from the client application and store it on their local disks. The data is typically replicated across multiple DataNodes for fault tolerance. Once the data has been successfully stored on the DataNodes, the NameNode sends an acknowledgement back to the client application, indicating that the write request has been completed.



# [4] process of Data write in HDFs
The process of writing data to HDFS typically involves the following steps:
A client application generates the data that it wants to write to HDFS and sends a write request to the NameNode (the master node in an HDFS cluster).
The NameNode receives the write request and determines the best way to store the data based on the available space on the DataNodes (the worker nodes in an HDFS cluster), the replication factor, and other factors.

The NameNode sends instructions to the DataNodes, telling them where to store the data. The DataNodes then receive the data from the client application and store it on their local disks.

The data is typically replicated across multiple DataNodes for fault tolerance. This means that multiple copies of the data are stored on different DataNodes in the cluster.

Once the data has been successfully stored on the DataNodes, the NameNode sends an acknowledgement back to the client application, indicating that the write request has been completed.

This process ensures that the data is stored reliably and can be accessed by client applications even in the case of individual machine failures. It also allows for efficient storage and retrieval of large amounts of data in a distributed computing environment.





# [5] Fault tolerance in Hadoop
Fault tolerance is an important feature of the Hadoop ecosystem, including HDFS and other components. Hadoop is designed to be able to continue functioning even in the case of individual machine failures, which is essential for handling large amounts of data in a distributed computing environment.

One way that Hadoop achieves fault tolerance is through the use of data replication. In HDFS, for example, data is replicated across multiple machines in the cluster, so that if one machine fails, the data can still be accessed from another machine. This is done automatically by the system, and the number of replicas of each block of data can be configured by the user.

Another way that Hadoop achieves fault tolerance is through the use of redundant data storage and processing. For example, the MapReduce programming model allows for the same computation to be performed on multiple machines in parallel, so that if one machine fails, the computation can still be completed by the other machines.

Overall, Hadoop's fault tolerance features help to ensure that it can continue to function and provide reliable access to data even in the face of individual machine failures. This is an essential requirement for any large-scale, data-intensive distributed computing system.





# [6] How to achieve High Availibility in Hadoop
There are several ways to achieve high availability in Hadoop, including the following:

Use HDFS Rack Awareness to optimize data storage and improve fault tolerance. This feature enables HDFS to take into account the physical layout of the machines in a cluster when storing data, in order to improve data availability and reduce the impact of individual machine failures.

Use data replication to create multiple copies of data on different machines in the cluster. This helps to ensure that the data remains available even if one or more machines fail. The number of replicas can be configured by the user, and HDFS will automatically manage the replication process.

Use the MapReduce programming model to perform computations in parallel on multiple machines. This allows for redundant data processing and helps to ensure that the computation can be completed even if one or more machines fail.

Use automatic failover mechanisms to quickly and transparently recover from failures. For example, the NameNode in an HDFS cluster can be configured to have a hot standby, so that if the primary NameNode fails, the standby can take over immediately without any interruption to the system.

Overall, these strategies can help to ensure that a Hadoop cluster remains highly available and continues to provide reliable access to data even in the face of machine failures.





# [7] Difference between Secondary Name node And Standby Name node
The Secondary NameNode and the Standby NameNode are two different components in a Hadoop cluster that serve similar but distinct roles.

The Secondary NameNode is a support role for the primary NameNode (the master node in an HDFS cluster). It periodically downloads the primary NameNode's edit log and file system metadata, and builds a new in-memory merge of these into a new file system checkpoint. This helps to reduce the load on the primary NameNode and improve its performance. However, the Secondary NameNode does not take over if the primary NameNode fails.

The Standby NameNode, on the other hand, is a true hot standby for the primary NameNode. It maintains an in-memory, up-to-date copy of the file system metadata, and can take over as the active NameNode if the primary NameNode fails. This allows for transparent and automatic failover, with no interruption to the system.

Overall, the Secondary NameNode and the Standby NameNode serve different purposes, but both can be useful in ensuring the availability and reliability of an HDFS cluster.



# [8] FS image
In the context of HDFS, the term "FS image" refers to a file that contains the complete state of the file system at a given point in time. This includes the file system metadata, such as the directory structure and the file-to-block mapping, as well as the actual contents of the file system's blocks.

The FS image is created and maintained by the NameNode (the master node in an HDFS cluster), and it is used to restore the file system to a known state after a failure or other disruption. When the NameNode starts up, it loads the FS image from disk into memory, and this becomes the basis for the file system's in-memory state. The NameNode then applies any changes that have occurred since the FS image was last saved, such as new files being created or deleted, to update the in-memory state of the file system.

Overall, the FS image is an important component of HDFS that allows the file system to recover from failures and maintain a consistent and up-to-date state.




# [9] Edit logs
In the context of HDFS, the term "edit logs" refers to a log of all changes that have been made to the file system since the last checkpoint. This includes information about file and directory creations, deletions, and modifications, as well as changes to the file-to-block mapping and other metadata.

The edit logs are maintained by the NameNode (the master node in an HDFS cluster), and they are used to update the in-memory state of the file system after a failure or other disruption. When the NameNode starts up, it first loads the FS image (a file containing the complete state of the file system at a given point in time) into memory. It then applies the changes recorded in the edit logs to the in-memory state of the file system, bringing it up-to-date.

The edit logs are also used by the Secondary NameNode, which periodically downloads the edit logs from the primary NameNode and uses them to create a new FS image. This helps to reduce the load on the primary NameNode and improve its performance.

Overall, the edit logs are an important component of HDFS that help to ensure the consistency and reliability of the file system.
