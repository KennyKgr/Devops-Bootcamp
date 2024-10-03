# AWS VPC Project

## Creating the **VPC**

- Understanding the requirements of this project I went on to Create a VPC **Project7** with *CIDR Block*  **10.0.0.0/24**.

![vpccreation](/Project7/img/01_Creating_a_vpc.png

- Created the VPC Successfuly

![createdvpc](/Project7/img/02_Vpc_created.png)

- Created an Internet Gateway) **Project7-IGW**

![Pj7](/Project7/img/04_IGW_Created.png)

- Pr0ceeded to next step that was aimed at attaching My IGW to the VPC

![vpc](/Project7/img/05_Attaching_to_Vpc.png)

- IGW attached to the VPC successfully

![vpcattach](/Project7/img/06_Attached_IGW_success.png)

## Subnets

- Following the desired naming scheme I went ahead to create public subnets with the information tabled below

| Avaliability Zone | CIDR Block | Type |
|:------------------|:----------:|-----:|
| us-west-2a | 10.0.0.0/28 | Public |
| us-west-2b | 10.0.0.16/28 | Public |
| us-west-2c | 10.0.0.32/28 | Public |

- Went ahead to created the public subnets

![publicsubnet](/Project7/img/07_Subnet_for_Public_2a_2b_2c_Create.png)

- Created public Subnets

![public](/Project7/img/08_Public_Subnet_creation_success.png)

- proceeded to create Application Subnets

![Appsubnet](/Project7/img/09_App_subnet_creation_success.png)

- Created Database Subnets

![dbsubnet](/Project7/img/10_Db_sunet_creation_success.png)

- Created management Subnets

![management](/Project7/img/11_management_subnet_creation_success.png)

- Created Platform subnets

![platform](/Project7/img/12_Platform_subnet_creation_success.png)

## Route Tables

- Named and created Routing Tables for each subnet group, with a custom route table

- Created the public Routing Table, selecting the vpc of **Project7**

![creatpubrt](/Project7/img/13_Public_Route_Table_Creation.png)

-Public Rt Created successfully

![cretdpbrt](/Project7/img/14_Public_Route_Table_Creation_Success.png)

- Went on to edit the public Routing Table in order to associate the public subnets

![asscpt](/Project7/img/15_Proceed_to_edit_subnet_Association.png)

- Associate the public subnets to the routing table

![associate](/Project7/img/16_Associate_3_Public_subnets.png)

- Public Route Table done successfully

![SuccessrT](/Project7/img/17_Public_subnets_Associated_successfully_with_Public_Routing_Table.png)

- Created App Route Table and associated the App subnets

![Apprt](/Project7/img/18_App_Subnets_Associated_with%20App_Routing_Table.png)

- Created Database Route Table and associated the Database subnets

![Dbrt](/Project7/img/19_DB_Subnets_Associated_successfully_with%20DB_Routing_Table.png)

- Created management Route table and associated the management subnets

![mangtrt](/Project7/img/20_management_Subnnets_Associated_successfully_with_management_Routing_Table.png)

- Created Platform route table and associated the platform subnets

![platfmrt](/Project7/img/21_Platform_subnets_Associated_successfully_with-with_platform_Routing_Table.png)

## Nat Gateway

- With need for a Nat gateway I went on to create a **Nat gateway**, add a subnet and associated an elastic ip address

![natcreation](/Project7/img/22_Creating_Nat-Gateway_and-Associating_An_Elastic_Ip_to_it.png)

- Nat Gateway **"Nat-Devpj7"**created successfully

![natsuccess](/Project7/img/23_Nat_Gateway_Created-success.png)

- Proceeded to add the Nat gateway to my route tables and destination **0.0.0.0/0**

![addrt](/Project7/img/24_Adding_Routes_to_Tables.png)

- Added the Nat Gateway to the platform Route Table and status was active

![pltrt](/Project7/img/25-NatGW_Route_added_to%20_platformRT.png)

- Added the nat gateway to the mangement Route Table and status was active

![mngtrt](/Project7/img/26_NatGW_Route_added_to_ManagementRT.png)

-Added the nat Gateway to the Database Route Table and status was active

![Dbrt](/Project7/img/27_NatGW_Route_added_to_DataBaseRT.png)

- Added the nat gateway to the App Route table and status was active

![Apprt](/Project7/img/28_NatGW_Route_added_to_AppRT.png)

- For the public Route Table and subnets I attached the Internet gateway

![publicRt](/Project7/img/29_IGW_Route_added_to_Public_RT.png)

## AWS VPC Topology

- To check my Vpc topology which was thus.

![vpc](/Project7/img/30_Vpc_Topology_top.png)

![vpcdetail](/Project7/img/31_VPC_Topology.png)

## Network Acls

- using the network Access Control List I needed to allow connections to the Database only for the App and Management subnets.

- The Public subnet should not have access to the Database subnet

- Went ahead to set create Nacl for Database Subnet **DBDev-Nacl**

![inbound](/Project7/img/33_Nacl_Created_for_DB_Subnet.png)

- Respecting the set rules **DBDev-Nacl(Inbound Rules)**

|Rule Number | Type | Protocol | Port Range | Source Ip | Allow/Deny |
|:-----------|:----:| :-------:| :---------:| :--------:| ----------:|
|100         |custom Tcp |TCP  | 3306       |10.0.0.0.96/28 |Allow |
|110         |custom Tcp |TCP  | 3306       |10.0.0.0.112/28 |Allow |
|120         |custom Tcp |TCP  | 3306       |10.0.0.0.128/28 |Allow |
|*           |All Traffic | All | All       |0.0.0.0/0    |Deny |

- Edited Inbound rules to Deny all traffic except for the necessary rules

![inboundrules](/Project7/img/34_Edit_inboud_rules_in_NaCl.png)

- The rules as configured

![rules](/Project7/img/35_Nacl_Inboud_rules_active.png)

- Respecting the set rules **DBDev-Nacl(Outbound Rules)**

|Rule Number | Type | Protocol | Port Range | Source Ip | Allow/Deny |
|:-----------|:----:| :-------:| :---------:| :--------:| ----------:|
|100         |custom Tcp |TCP  | 3306       |10.0.0.0.192/28 |Allow |
|110         |custom Tcp |TCP  | 3306       |10.0.0.0.208/28 |Allow |
|120         |custom Tcp |TCP  | 3306       |10.0.0.0.224/28 |Allow |
|*           |All Traffic | All | All       |0.0.0.0/0    |Deny |

- Edited outbound rules to Deny all traffic to the database subnets except for the necessary rules

![outboundedit](/Project7/img/36_Edit_outbound_rules_in_NaCl.png)

- The Rules set and active

![outbound](/Project7/img/37_Outboud_NaCl_rules_for_DbSubnets_Active.png)

## End Of Project)
