Title: Home-lab Kubernetes cluster setup
Date: 2024-03-17 10:20
Category: Kubernetes

I recently[ref]back in 2022 but time has no meaning[/ref] found myself in a position where 
my next job may be either working with Developer Productivity or Kubernetes, and since I don't trust a system
further than I can throw it I immediately set out to build a cluster.

And from past incidents I know that the moment I start using something it'll eventually become a production system,
so really the only viable way forward is to over-engineer the solution. It's like that old saying "If you're not part of the 
solution there's good money to be made in the problem"

So I set out with some basic requirements:
*It must be highly available*.
I'm not going to assume any machine will function perfectly, and I'm not going to incur 
downtime when I do upgrades. In fact, I'm going to be tinkering with this all the time, so the thing better work 
just fine after I accidentally restart or reinstall the wrong computer.

*Persistent storage must be available and dynamically provisioned*. I'm absolutely not going to hand-craft any PVs.

*When it breaks it must be in new and exciting ways*. Because everyone loves a good puzzle.


# Final setup

So attempting to meet all these basic requirements I ended up with a cluster that is:

* 3 rack-mounted nodes with battery backups
* segmented network firewalled off from the rest
* dynamically provisioned storage
* load-balancer support
* automatic security upgrades

And by that I mean I got 3 ThinkPad x230s that's hanging out in a closet on [IKEA wine racks](https://www.ikea.com/us/en/p/ivar-shelving-unit-with-bottle-racks-pine-gray-s39250601/)
supported through nfs-subdir-provisioner and my NAS. But really, that's pretty close.

I don't have dual PSUs or dual NICs, but I got built-in battery and bluetooth support.
Does your cluster support bluetooth? Didn't think so!