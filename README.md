# boat-mc

This project is in ultra-early development phase, where it basically is just a concept.

<p align="center">
  <img width="460" height="300" src="https://github.com/leElvyn/boat-mc/blob/main/images/logo.png">
</p>

## The concept 

One of the major issues with minecraft servers currently is that it's basically impossible to have large servers on one map, as the hardware required to fit more than ~ 150 players with stable TPSs becomes extremely expansive.
So, the idea to divide a map into "sections", each one of them handled by a different physical server.
These sections should be of flexible size, managing a certain number of chunks, depending on the load put on each one of them.
Some high load areas, like spawn should be handled by more powerful servers, but others, can be scattered across smaller servers.
The biggest challenge would be to always keep the map in sync, while avoiding dupes.

## How it *should* work 
(aka : The drawing board)

The architecture is composed of : 

- A central server (the "relay"). This is the server where every players is connecting to. It doesn't implement any features from the NMS package. This server should be written in a language like Rust, and his only purpose would be to forward the traffic from the server currently handling the client, as well as orchestrate every other servers. That allows for smooth transitions whenever we need to change the physical server the player is managed by.
- A lot of smaller servers ("shards"), running a "normal" minecraft server, but only computing a certain number of chunks. They are orchestrated by the relay, and whenever a player approaches the border of a section, the relay will now forward to the player the traffic from the new server.

![illustration flowchart](https://github.com/leElvyn/boat-mc/blob/main/images/chart-v1.png)
