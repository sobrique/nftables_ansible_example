# nftables_ansible_example

Wrote up an example of 'doing nftables' because I found that the documentation site was ... almost too comprehensive.

So my attempt to write up a 'simple ish' host based nftables setup - that would be automated by ansible - was for my own reference as much as for others.

https://edrolison.substack.com/p/nftables-simple-host-config

The rough summary is that by applying a 'standard' template /etc/nftables/main.nft, with a bunch of optional-include files, you get a 'conf.d like' approach to adding host/role/group specific related firewall snippets, without having to get all complicated with policy compilation, generation, etc.

And this was _specifically_ because 'firewalld' wasn't quite nuanced enough for my purposes, and I was resorting to a lot of rich rules as a result. 

Which is not to say firewalld is not perfectly adequate for most purposes, just that it wasn't enough for mine. 
