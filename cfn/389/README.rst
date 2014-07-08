The 389 ldap server templates currently broken up into a few pieces.

Step 1: Init the Cluster

To start a new 389 cluster, spawn stack:
389_BaseCluster.yaml. name it something like "ldap-base".

This sets up all of your static cluster bits. Anti-Affinity Server Group, Read Only Load Balancer, etc.

*** NOTE, this template set depends on a Heat Resource that is not released as part of Icehouse yet. You can download the resource here:
https://review.openstack.org/#/c/100995/
This resource forces ldap servers to physically reside on separate resources, increasing reliability.

Note, due to a limitation/bug in neutron lbaas, after launching the load balancer, the load balancer may be assigned the
wrong security group on its vip. The following procedure can be used to fix it until the bug is resolved (replace content
listend in <...> with the value requested inside:
 * run "heat stack-show <your base cluster stackname>". Find the output_value associated with "ROLoadBalancerVipPort". Also find
       the output_value associated with "389SecurityGroup"
 * run "neutron port-update <output value ROLoadBalancerVipPort> --security-group <output value 389SecurityGroup here>"

Step 2: Init your Master Server volume

Create a SingleMaster ldap server by launching 389_Server_Init.yaml. Select Type SingleMaster. Give it params from the output of the
389_BaseCluster stack. Once the Init is complete, record the Output.VolumeId of the stack, and delete the stack.

Step 3: Start your Master Server

Copy 389_Server_SingleMasterExample.yaml somewhere and modify the paramaters to match your 389 base cluster outputs and other params.
This way, you can rebuild your Master server by simply deleting the stack and relaunching with your saved file. Once modified, launch.

Step 4: Create replica volumes
Copy 389_RO_Replica_Init_Example.yaml somewhere and modify the paramaters to match your 389 base cluster outputs and other params.
With this, you can easly init multiple server volumes by launching multiple stacks. When this is done, launch 1 or more of these.
I'd recommend at least 2. When complete, record their Output.VolumeId's and delete the stacks.


