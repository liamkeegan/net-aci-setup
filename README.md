# net-aci-setup
Do you need to set up an ACI fabric in network-centric naming mode from scratch? Here's a handful of Postman collections that will take a Cisco ACI fabric (specifically, the ACI simulator) and setup the fabric for L2 and L3 outs, bridge domains, permit-any EPGs, and a Production VRF.

With a bit of renaming and node-id modification, you can leverage these scripts to setup a production, physical environment. The components here should give you enough to get a base deployment off the ground. 

The ACI Simulator is a fantastic resource for planning out an ACI implementation. Virtaully everything can be pre-configured and tested prior to performing the actual deployment. [Cisco dCloud](https://dcloud.cisco.com) offers ACI sandboxes that allow you to test and validate your scripts prior to implementation. 

There are five Postman collections, each broken out into multiple activities. Here's the summary:

| Link | Collection                     | Description                                                                                                                                 |
|------|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/d4d5b20e3651168e5aad)    | ACI Best Practices             | One-time fabric setup tasks, such as enabling MCP, loop protection and COS value preservation.                                              |
| [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/2b672266a6e0c9cdb3f4)    | One Time Management Setup      | Sets up common fabric tasks, such as NTP, OOB IPs, DNS, and management filters.                                                             |
| [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/33ea5a6d0dcf3e0fa9a0)    | Fabric and Tenant Provisioning | Configures a single production tenant, registers unregistered switches, plus VLAN pools, domains, and interface/port profiles.              |
| [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/0e943c3599b20a093d2e)    | L2 and L3 Outs                 | Sets up and assigns the L2 and L3 Outs to dedicated ports. The L2 ports are setup as a VPC port channel, the L3 are routed /30s with EIGRP. |
| [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/d815addf0a2eac33f9f0)    | Access and VPC Ports           | Pre-configured VPC pairs for easy port provisioning. Plug and go!                                                                           |

The Postman collections are commented as to what the function of each does.

## Prerequisites

These Postman scripts assume the following:

	- THERE IS NO ERROR CHECKING! Run these at your OWN RISK on a production environment.
	- This is not an ACI How-To. 
	- The physical (or in the case of the APIC simultator, virtual) connections are all completed.
	- The APIC fabric setup wizard is completed, including assigning IP addresses for the TEP pool and Pod ID (1).
	- You'll need to set a few variables in Postman for apic_ip, apic_username and apic_password.
	- Everything could be lumped together in one large script with a big GO button. The point of these documents is to walk the engineer/customer through step by step to explain the building blocks.

## Getting Started
It should be pretty simple. Set your environmental variables in a Postman enviornment, ensure you have a valid token by running the "0 - APIC Authenticate" first, then look at the Body of each call, modify it, and send it! 

This is a good "getting started" point - this foundation can be used to build multi-tier EPGs, more restrictive contracts, fancier routing, VMM, etc.
