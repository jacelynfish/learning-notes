## Chap 11

### EIGRP

packet types:

* Hello packets: (Hello packets are always sent _unreliably_ on a regular time interval. No acknowledgement is transimitted)

  IPv4 multicast address: 224.0.0.10

  IPv6 multicast address FF02::A

* Update packets: (Update packets are sent _reliably_)

  * **New neighbor discovery**: When a router discover a new neighbor, it sent an **_unicast_** Update packet to that new neighbor to add it to its topology table
  * **Topological change**: send _**multicast**_ Update packets to all neighbors.

* Acknowledegment packets: send during reliable exchange. send in _**unicast**_

* Query packets, Reply packets



###### EIGRP timers

| Bandwidth                      | Default Hello Interval | Default Hold |
| ------------------------------ | ---------------------- | ------------ |
| **Equal, or below** 1.544 Mbps | 60 seconds             | 180 seconds  |
| **Greater** than 1.544 Mbps    | 5 seconds              | 15 seconds   |

###### EIGRP tables

**Neighbor table **(directly connected adjancent EIGRP routers) -> 

**Topology table **(calculate Feasible distance (FD), Reported distance (RD), Feasible successor (FS, backup successor) and successor.) ->

**IP routing table** (successor routes topology)



#### States

* Passive state: router is works find. It's not performing a recomputation;
* Active state: router is performing a recomputation.

> If the alternative route RD is less than the original successor FD, the route is accepted as a feasible successor route
>
> Recomputation occurs when the destination has no feasible successor. DUAL turns it into **Active** state that a **query update** is multicasted to all **directly connected neighbors** trying to locate a successor to the destination network.



#### Metric calculation

**Default metric = bandwidth + delay**

**EIGRP bandwidth** = (10^7 / _bandwidth_) * 256	//lowest configured bandwidth: kbps

**EIGRP delay** = (_delay_ /10) * 256				//accumulation of total delays