## Chap 10

#### Link state routing protocol features

building route information in these following steps:

1. Each router collect s the route information from all other routers in the network or within a **defined area of network**. This is achieved by exchanging **link-state advertisements(LSAs)** .
2. Once all information is collected, each router constructs a **topological database** with itself as the root of this topological tree.
3. Each router uses the SPF algs to calculate the shortest route to each network and stores the route information in the routing table.



It first uses **hello packets** to keep track of the state of the neighbor routers (to confirm that the neighbor is still reachable), 

then it uses **LSAs** to accquire all the routers to build its topological tree. When a failure occurs such as the neighbor is unreachable, link-state protocols flood **LSAs** again with a special multicast address throughout an area. Each link-state router takes a copy of the **LSA** and updates its link-state, or topological database. The link-state router then forwards the LSA to all neighbor devices. LSAs cause every router within the area to recalculate routes.



Link state protocol advantages:

* **Triggered** updates: fast convergence times
* Route updating messages are **partial**: improved bandwidth utilization
* **Exact topology**: difficult for routing loop to occur




#### OSPF

OSPFv2: IPv4

OSPFv3: IPv6

OSPF is a **TCP** segment



#### Hello packet

Hello packet is used to **initiate new ajacencies** and to **ensure** that neighbor routers are still functioning. 

The information it carries must be agreed upon by all neighbors

![hello packet](./src_img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-13%20%E4%B8%8B%E5%8D%887.51.36.png)



#### OSPF Area

Backbone area: also called transit area

Non-backbone area: also called regular area



#### Build route information

**Adjacency database -> Link-state database -> Forwarding database**

1. Establish neighbor adjacencies

   >  send Hello packets to directly connected networks to build adjacency database.

2. Elect DR and BDR

   * **Point-to-point networks**: fully adjancent to each other, no need for DR and BDR
   * **Multi-access networks**: DRs and BDRs are elected on a per-network basis and therefore each network segment has its own DR and BDR. DR and BDR for a network always retain the same.

3. Build the topology

   > After each OSPF router floods the LSAs out to all neighbor **within the same area**, OSPF constructs a topological database(link-state database) for all routers.

   _This database is **identical** among all routers in the same area._

4. Find the best path

   > SPF algs is applied to compute the best path to each destination network. The lowest cost path is added to the routing table which is also known as _Forwarding database_

   OSPF cost:

   ```
   OSPF cost = 100,000,000 / Bandwidth (bps)
   ```



#### Maintaining Route information

##### No changes in the network

hello packet sending interval:

Point-to-point and broadcast multi-access networks: 10 sec

Non-broadcast multi-access networks: 30 sec

##### Changes occur in the network

1. The OSPF router notifies the neighbors by flooding a LSU to all other routers within the area and the neighbors will **acknowledge the receipt of the LSU with an LSAck**.
2. On multi-access link, LSU is sent to DR using the multicast address **224.0.0.6. DR** then floods the LSU to all OSPF routers in this network using the multicast address **224.0.0.5**, means “all OSPF routers
3. On point-to-point link, LSU is sent to the peer using **224.0.0.5**.
4. If an OSPF router is attached to another network, it continue floods the LSU to other networks.
5. After an OSPF router receives an LSU that includes new information, it then runs the SPF algorithm to recalculate the routing table.



#### Configuration

1. Enabling the OSPF routing process

   ```
   Router(config)#router ospf process-id
   ```

   The _process-id_ is used to identify an OSPF routing process.


2. Assiociates a IP network with the routing process

   ```
   Router(config-router)#network ip-address wildcard-mask area area-id
   ```

   Backbone area: Area 0. All areas are required to connect to backbone area.

3. Configure the bandwidth on the OSPF interface

   ```
   Router(config-if)#bandwidth bandwidth-kbps
   ```

   _Bandwidth-kbps_ default value: 1.544Mbps



##### router id: IP address