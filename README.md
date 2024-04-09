# nftables_ansible_example

Wrote up an example of 'doing nftables' because I found that the documentation site was ... almost too comprehensive.

So my attempt to write up a 'simple ish' host based nftables setup - that would be automated by ansible - was for my own reference as much as for others.

https://edrolison.substack.com/p/nftables-simple-host-config

The rough summary is that by applying a 'standard' template /etc/nftables/main.nft, with a bunch of optional-include files, you get a 'conf.d like' approach to adding host/role/group specific related firewall snippets, without having to get all complicated with policy compilation, generation, etc.

And this was _specifically_ because 'firewalld' wasn't quite nuanced enough for my purposes, and I was resorting to a lot of rich rules as a result. 

Which is not to say firewalld is not perfectly adequate for most purposes, just that it wasn't enough for mine. 

Note: there's a flaw with the approach I made with ansible, in that because my 'rules' are auto-included but hard coded in the final result, there's potential for 'check mode' to give different results to running the policy by hand.
I'm thinking about how to improve on that, but for now it - more or less - builds a list of files as it runs, and uses recency to detect if the base policy needs reloading at all. (e.g. if anything has changed in the directory tree). 

That means it'll reload more than it should if you run it multiple times, and it will also give a DIFFERENT result (and thus look like an error) in check mode. 

You could simplify in your environment to using a 'conf.d' approach and just including all files in your main.nft:

    #include "/etc/nftables/my_policy/*.nft"

That should work just fine, but I wanted to be sure that the only things being included were the ones I'd put there explicity, and it's oddly messy to have ansible 'clean up' orphan files. 
But if you're not worried about that, then this will work just fine none the less, and maybe adding your own 'ad hoc' include files is a feature not a bug. 

