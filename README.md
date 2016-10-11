# WEBLOGIC_DYNAMIC_CLUSTER_AND_DYNAMICSERVERLIST
The Dynamic cluster concept in Weblogic for creating the managed servers has a hidden feature when it is used along with parameter DynamicServerList.

When set to OFF, the plug-in ignores the dynamic cluster list(Managed Servers) used for load balancing requests proxied from the plug-in and only uses the static list specified with the WebLogicCluster parameter. 

Normally this parameter should remain set to ON.

1) Should the dynamic servers be brought up at peak load or it will be active by itself. (We need to bring them up manually)

I am trying to give you example : Lets take we have created Dynamic-cluster with 4 Servers , and we have bring them up manually and all are up and Running , and we know in specific Time Period we have huge Load for 2 hours,so we have just updated
Maximum Number of Dynamic Servers: parameter from Admin Console to 6 through Summary of Clusters >DynamicCluster >Summary of Servers navigation , so another 2 Managed servers will be created dynamically with the same configurations of already existed with 4 Servers.
Now we need to bring up two new Managed-servers just now we have created, so now all the 6 JVM's will take the Load.

http://docs.oracle.com/middleware/1213/wls/CLUST/dynamic_clusters.htm#CLUST709


2) Does the"dynamic server list" parameter in webserver has any link with weblogic dynamic clusters, knowing that webserver wont collect information of servers which are not running untill a peak loaded is reached.
According to above example , we will update ManagedServers information of Dynamic-Cluster in Webserver like (ip:port,ip:port,ip:port,ip:port) , in Peakload after we have included 2 more new JVM's into the Dynamic-Cluster and they are Up and Running
Now no need to update webserver with 2 New JVM's Ip:port information , because as we have discussed earlier bydefault DynamicServerList option will be on at Webserver Level , so Weblogic is Sending the response back to the webserver ( including with response List of all the servers in
cluster information will sent back to the plug-in ) so Traffic will be distributed across all 6 JVM's (Old 4 and 2 New)

Now we are done with Load and now only 4 JVM's are enough to take the calls , so we can bring down newly created 2 JVM's so accordingly Plug-in is smart enough to remove those 2 JVM's a from the List and Traffic wont route to those JVM's 
