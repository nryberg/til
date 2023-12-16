## Tailscale is the bomb dot com

I tore apart the messy set of wires in the basement printer area and distributed the computers to other places. 

I'd installed Tailscale a while back, but hadn't really used it other than a convenience.

Now that the servers are running wireless, I don't know what ip address they're using... and I don't care.

Now I have to fix up the connections pushing data to Minio.  Minor pain, but if the ip addresses are reliable, then I don't have to worry about managing it. 

One question - won't tailscale run out of ip addresses to distribute?

## Command Line

It appears that the Menu Bar version of Tailscale isn't showing.  

If you need the command line version:

`/Applications/Tailscale.app/Contents/MacOS/Tailscale`

Use `up` and `down` as needed. 

## 2023-12-16

So - love the Tailscale.  Love using PiHole.  Love trying to use PiHole across the entire network.  Don't like using Tailscale to configure DNS for the entire network and then having the PiHole go down leaving me with no connectivity.  

The Tinkerboard is dead.  I don't know why and I don't have time to fix it.  I'm tempted to either use a good service (AdBlock) or host my own PiHole in the cloud - which is tempting but hackable. 

Oi.


