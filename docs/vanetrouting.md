# VANET Routing

Vehicular Ad Hoc Network (VANET) routing is a critical aspect of intelligent transportation systems, aiming to efficiently manage communication among vehicles on the move. In VANET routing, the challenge lies in establishing reliable and low-latency communication paths to support applications like collision avoidance and traffic management. Dynamic and ever-changing network topologies require adaptive routing protocols, often categorized into proactive, reactive, and hybrid approaches. These protocols leverage vehicle-to-vehicle (V2V) and vehicle-to-infrastructure (V2I) communication to relay information about road conditions, hazards, and traffic patterns. VANET routing plays a pivotal role in enhancing road safety, traffic efficiency, and overall transportation system effectiveness by facilitating seamless and timely data exchange among connected vehicles.

## Flooding in VANET
Vehicular Ad Hoc Networks (VANETs) utilize a routing technique known as flooding, where a message originating from a vehicle is broadcasted to all neighboring vehicles within its communication range. This straightforward approach ensures widespread dissemination of information throughout the network. While flooding is robust, it comes with challenges such as high message overhead and potential congestion. Optimizations, including the use of beacons and probabilistic rebroadcast mechanisms, are often employed to enhance efficiency and control the dissemination scope. Effectively managing flooding in VANETs is crucial for striking a balance between reliable information dissemination and resource utilization in dynamic vehicular environments.
## Steps
* Source node send message
* Every node contains a receiver module and transmitter module
* Except destination node, every receiver node retransmit message