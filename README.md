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



# [10] HDFS Architecture
HDFS (Hadoop Distributed File System) is a distributed, scalable, and fault-tolerant file system designed to store data on low-cost commodity hardware. It is part of the Apache Hadoop project and provides a reliable and distributed way of storing data across a cluster of machines.

The HDFS architecture is based on a master-slave model, where a cluster consists of a single NameNode (the master node) and multiple DataNodes (the worker nodes). The NameNode is responsible for managing the file system namespace and regulating access to files by client applications. The DataNodes are responsible for storing the actual data blocks and serving read and write requests from the clients.

When a client application wants to read or write a file, it first contacts the NameNode to get information about the location of the data blocks. The NameNode then sends instructions to the appropriate DataNodes, which perform the actual read or write operations. The data is typically replicated across multiple DataNodes for fault tolerance, and the NameNode keeps track of which blocks are stored on which DataNodes.

Overall, the HDFS architecture is designed to be scalable, flexible, and fault-tolerant, allowing it to store and manage large amounts of data across a cluster of machines.





# [11] Standby Name node Architecture
The Standby NameNode is a hot standby for the primary NameNode (the master node in an HDFS cluster). It maintains an in-memory, up-to-date copy of the file system metadata, and can take over as the active NameNode if the primary NameNode fails. This allows for transparent and automatic failover, with no interruption to the system.

The Standby NameNode is typically deployed as a separate machine or set of machines, and it maintains a constant connection to the primary NameNode. The primary NameNode sends periodic updates to the Standby NameNode, which keeps its in-memory copy of the file system metadata in sync with the primary NameNode. If the primary NameNode fails, the Standby NameNode can take over immediately and continue servicing client requests without any interruption.

The Standby NameNode also acts as a Secondary NameNode, periodically downloading the primary NameNode's edit logs and building new FS images (files containing the complete state of the file system at a given point in time). This helps to reduce the load on the primary NameNode and improve its performance.

Overall, the Standby NameNode is an important component of the HDFS architecture that helps to ensure the availability and reliability of the file system.





# [12] YARN
YARN (Yet Another Resource Negotiator) is a resource management and scheduling system for distributed computing environments, such as Hadoop clusters. It is part of the Apache Hadoop project and provides a central platform for managing and coordinating the allocation of resources (such as CPU, memory, and storage) across the cluster.

YARN consists of two main components: the ResourceManager and the NodeManager. The ResourceManager is the master component, and it is responsible for managing the allocation of resources across the cluster. It receives resource requests from applications and determines the best way to satisfy those requests by allocating resources on the worker nodes (DataNodes in the case of HDFS). The NodeManager is the slave component, and it is responsible for managing the resources on each individual worker node. It reports the available resources on the node to the ResourceManager, and it is responsible for launching and managing application containers on the node.

Overall, YARN is an important component of the Hadoop ecosystem that enables efficient and flexible resource management and scheduling in distributed computing environments.





# [13] Steps for resource allocation in yarn
The steps for resource allocation in YARN (Yet Another Resource Negotiator) typically involve the following:

A client application submits a request for resources to the ResourceManager (the master component in a YARN cluster). This request specifies the amount and type of resources that the application needs, such as CPU, memory, and storage.

The ResourceManager receives the resource request and determines the best way to satisfy it by allocating resources on the worker nodes (typically DataNodes in the case of HDFS). This allocation is based on a variety of factors, such as the available resources on each node, the capacity of the cluster, and the current workload.

The ResourceManager communicates the allocation decision to the NodeManager (the slave component) on the appropriate worker node, instructing it to allocate the requested resources to the application.

The NodeManager on the worker node receives the allocation instruction and creates a container to hold the application and its allocated resources. The container is then launched, and the application is executed within it.

The NodeManager monitors the application's use of the allocated resources and reports this information back to the ResourceManager. The ResourceManager uses this information to manage the overall allocation of resources across the cluster and to ensure that the resources are used efficiently.

Overall, these steps illustrate the basic process by which YARN coordinates the allocation of resources to applications in a distributed computing environment.




# [14] Resource Manager
The ResourceManager is a key component of YARN (Yet Another Resource Negotiator), which is a resource management and scheduling system for distributed computing environments, such as Hadoop clusters. It is the master component in a YARN cluster, and it is responsible for managing the allocation of resources (such as CPU, memory, and storage) across the cluster.

The ResourceManager receives resource requests from applications and determines the best way to satisfy those requests by allocating resources on the worker nodes (DataNodes in the case of HDFS). It uses a variety of factors to make allocation decisions, such as the available resources on each node, the capacity of the cluster, and the current workload. It then communicates the allocation decisions to the NodeManagers (the slave components) on the worker nodes, instructing them to allocate the requested resources to the applications.

The ResourceManager also receives periodic updates from the NodeManagers about the usage of allocated resources, and it uses this information to manage the overall allocation of resources across the cluster. This helps to ensure that the resources are used efficiently and that applications receive the resources they need to run effectively.

Overall, the ResourceManager is a critical component of YARN that enables efficient and flexible resource management and scheduling in distributed computing environments.



 # [15] Scheduler
A scheduler is a system or component that is responsible for determining the order and timing of execution for a set of tasks or jobs. Schedulers are commonly used in computing environments to manage the allocation of resources, such as CPU and memory, and to ensure that tasks are executed efficiently and in a timely manner.

There are many different types of schedulers, and the specific characteristics and behaviors of a scheduler can vary depending on the context and the needs of the system. For example, some schedulers may prioritize tasks based on certain criteria, such as deadlines or priorities, while others may use more complex algorithms to optimize resource utilization and performance.

In the context of YARN (Yet Another Resource Negotiator), the ResourceManager includes a scheduler that is responsible for determining the allocation of resources to applications. The ResourceManager receives resource requests from applications, and the scheduler uses various factors, such as the available resources on each node and the current workload, to determine the best way to satisfy those requests. It then communicates the allocation decisions to the NodeManagers (the slave components) on the worker nodes, instructing them to allocate the requested resources to the applications.

Overall, schedulers are important components of many computing systems, as they enable the efficient and effective execution of tasks and the allocation of resources.





# [16] Application Master
In the context of YARN (Yet Another Resource Negotiator), the Application Master is a per-application component that is responsible for negotiating resources from the ResourceManager and working with the NodeManager to execute and monitor the tasks of the application.

When an application is submitted to a YARN cluster, the ResourceManager first creates an instance of the ApplicationMaster for that application. The ApplicationMaster then contacts the ResourceManager to request the resources that it needs to execute its tasks, such as CPU, memory, and storage. The ResourceManager uses its scheduler to determine the best way to satisfy the resource request, and it communicates the allocation decision to the NodeManager on the appropriate worker node.

The NodeManager then creates a container to hold the application and its allocated resources, and it launches the application within the container. The ApplicationMaster is responsible for managing the execution of the application's tasks within the container, and it communicates with the NodeManager to request and release resources as needed. It also monitors the progress of the tasks and provides status updates to the ResourceManager.

Overall, the ApplicationMaster is an important component of YARN that enables applications to request and use resources from the cluster in a dynamic and flexible manner.





# [17] Node Manager
The NodeManager is a key component of YARN (Yet Another Resource Negotiator), which is a resource management and scheduling system for distributed computing environments, such as Hadoop clusters. It is the slave component in a YARN cluster, and it is responsible for managing the resources on each individual worker node.

The NodeManager is responsible for reporting the available resources on the node to the ResourceManager (the master component), and it is also responsible for launching and managing application containers on the node. When the ResourceManager receives a resource request from an application, it communicates the allocation decision to the appropriate NodeManager, instructing it to allocate the requested resources to the application.

The NodeManager then creates a container to hold the application and its allocated resources, and it launches the application within the container. It monitors the application's use of the allocated resources and reports this information back to the ResourceManager. The ResourceManager uses this information to manage the overall allocation of resources across the cluster and to ensure that the resources are used efficiently.

Overall, the NodeManager is a critical component of YARN that enables the efficient and effective execution of applications on the worker nodes of a distributed computing environment.



# [18] Data node
In the context of HDFS (Hadoop Distributed File System), a DataNode is a worker node that is responsible for storing the actual data blocks of a file and serving read and write requests from the clients.

A typical HDFS cluster consists of a single NameNode (the master node) and multiple DataNodes. The NameNode is responsible for managing the file system namespace and regulating access to files by client applications. When a client application wants to read or write a file, it first contacts the NameNode to get information about the location of the data blocks. The NameNode then sends instructions to the appropriate DataNodes, which perform the actual read or write operations.

The data is typically replicated across multiple DataNodes for fault tolerance, and the NameNode keeps track of which blocks are stored on which DataNodes. The DataNodes also communicate with the NameNode periodically to report on the status of their blocks and to receive instructions on any necessary replication or rebalancing of the data.

Overall, the DataNodes are an essential component of HDFS, as they provide the storage and processing power for the file system.





# [19] Name node
In the context of HDFS (Hadoop Distributed File System), the NameNode is the master node that is responsible for managing the file system namespace and regulating access to files by client applications.

A typical HDFS cluster consists of a single NameNode and multiple DataNodes (worker nodes). The NameNode maintains the file system namespace and the file-to-block mapping, which describes how the files are stored as blocks across the DataNodes. It also maintains the edit logs, which are a log of all changes that have been made to the file system since the last checkpoint.

When a client application wants to read or write a file, it first contacts the NameNode to get information about the location of the data blocks. The NameNode then sends instructions to the appropriate DataNodes, which perform the actual read or write operations. The NameNode also monitors the health and status of the DataNodes, and it coordinates the replication and rebalancing of data blocks as needed.

Overall, the NameNode is a critical component of HDFS, as it provides the centralized control and management for the file system.




# [20] block
In the context of HDFS (Hadoop Distributed File System), a block is the basic unit of storage for data in the file system.

In HDFS, files are split into blocks and distributed across multiple DataNodes (worker nodes) in a cluster. Each block is typically 64 MB or 128 MB in size, and multiple blocks make up a file. The blocks are replicated across multiple DataNodes for fault tolerance, and the NameNode (the master node) keeps track of which blocks are stored on which DataNodes.

When a client application wants to read or write a file, it first contacts the NameNode to get information about the location of the data blocks. The NameNode then sends instructions to the appropriate DataNodes, which perform the actual read or write operations on the blocks.

Overall, the concept of blocks is an important aspect of the HDFS architecture, as it enables the efficient and scalable storage of large files across a distributed cluster of machines.



# [21] Map reduce architecture in hadoop
Hadoop is an open-source software framework for distributed storage and processing of large datasets on clusters of commodity hardware. It uses the MapReduce programming model for parallel and distributed processing of large datasets on clusters of computers. In Hadoop, the MapReduce framework consists of two main components: the Map function and the Reduce function. The Map function processes a dataset in parallel, dividing it into smaller sub-datasets, which are then passed to the Reduce function to produce a final output. The MapReduce framework in Hadoop automatically manages the parallelization, partitioning, and distribution of the data across the cluster, as well as the coordination of the tasks and their execution.





# [22] Step by step excution flow of Map Reduce
The input data is divided into small splits called blocks, which are then distributed across the cluster for processing.

The Map function is applied to each block of data in parallel, generating a set of intermediate key-value pairs.

The intermediate key-value pairs are grouped by key and passed to the Reduce function, which aggregates the values and produces a final output.

The final output is written to a distributed file system or returned to the application.

The MapReduce framework manages the parallelization, partitioning, and distribution of the data across the cluster, as well as the coordination and execution of the tasks.




# [23] Input files
Input files are the data that is processed by a program or application. In the context of the MapReduce framework, input files are the data that is fed into the Map function for processing. The input files can be of any format, such as text files, binary files, or sequence files. The Map function processes the input files and generates intermediate key-value pairs, which are then passed to the Reduce function for further processing. The input files are typically stored in a distributed file system, such as HDFS in Hadoop, and are divided into blocks that are distributed across the cluster for parallel processing.





 # [24] Input format
The input format is the way in which input data is structured and presented to a program or application. In the context of the MapReduce framework, the input format specifies how the input data is read and divided into blocks for processing by the Map function. There are different types of input formats, such as TextInputFormat, SequenceFileInputFormat, and KeyValueTextInputFormat, which are designed to handle different types of input data. The input format can be set by the user or application, depending on the specific requirements and characteristics of the input data.




# [25] Input splits
Input splits are the smaller sub-datasets that are derived from the larger input dataset in the MapReduce framework. The input data is divided into blocks, and the MapReduce framework uses the input format to determine how the blocks are split into input splits. The input splits are then distributed across the cluster for parallel processing by the Map function. The size of the input splits can be configured by the user or application, depending on the specific requirements and characteristics of the input data. The size of the input splits can affect the performance of the MapReduce job, as smaller input splits may lead to more overhead in terms of communication and coordination, while larger input splits may lead to uneven data distribution and inefficient processing.
