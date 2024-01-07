**Flow control** is used to control the amount of data that a sender can send without overloading the receiver.
To make flow control work, the receiver must send some feedback back to the sender.

The network layer does not directly offer any flow control.
Datagrams are sent when they are ready, without focusing on whether the receiver can receive the datagrams.

Here are a few reasons why flow control is not offered:
* Since there is already no error checking, the network layer's job here is so simple that it is unlikely that the receiver will be overloaded.
* The upper layers that use the network layer can implement buffers to receive data from the network layer, so they do not have to consume data as fast as it is received at the network layer.
* flow control is provided for most of the upper-layer protocols that use the services of the network layer, so another level of flow control makes the network layer more complicated and the whole system less efficient.