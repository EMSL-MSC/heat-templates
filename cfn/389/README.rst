The 389 ldap server templates currently broken up into a few pieces.

To start a new 389 cluster, spawn stack:
389_BaseCluster.yaml

This sets up all of your static cluster bits. Anti-Affinity Server Group, Read Only Load Balancer, etc.


*** NOTE, this template set depends on a Heat Resource that is not released as part of icehouse yet. You can download the resource here:
https://review.openstack.org/#/c/100995/
This resource forces ldap servers to physically reside on separate resources, increasing reliability.

Note, due to a limitation/bug in neutron lbaas, after launching the load balancer, the load balancer may be assigned the
wrong security group on its vip. The following procedure can be used to fix it until the bug is resolved (replace content
listend in <...> with the value requested inside:
 * run "heat stack-show <your base cluster stackname>". Find the output_value associated with "ROLoadBalancerVipPort". Also find
       the output_value associated with "389SecurityGroup"
 * run "neutron port-update <output value ROLoadBalancerVipPort> --security-group <output value 389SecurityGroup here>"

