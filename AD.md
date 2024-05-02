	Domain controller: mydomain.com
	username : Administration
	passwd : Insrv8

## Windows Server 

- Type of Challenge: `Learning`
- Duration: `4 days`
- Deadline: `26/04/2024`
- Team challenge : `solo`

## Overview

This challenge guides you through deploying a secure Windows Server 2022 environment with Active Directory, essential server roles (IIS, DNS, DHCP), user management, Sysmon monitoring, and demonstration of its functionality to a client. Gain essential configuration skills, security awareness, and experience with Active Directory while incorporating user accounts like Alice and Bob for realistic role-based access.

## Learning Objectives:

- Install and configure Windows Server 2022.
- Create and manage user accounts within Active Directory.
- Set up and configure Active Directory for centralized user management.
- Apply granular permissions for users like Alice and Bob based on security principles.
- Install and configure essential server roles (IIS, DNS, DHCP).
- Implement Sysmon for system activity monitoring.
- Analyze Sysmon data and present its security value to the client.
## Environment:

**Ressources:**

- Virtualization software: Microsoft Hyper-V, 
- **Required:**  
    [Windows Server 2022 evaluation](https://www.microsoft.com/evalcenter/evaluate-windows-server-2022)
- [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) monitoring solution

## Steps:

**1. System Preparation:**

1. Set up your virtualization environment with multiple VMs:
**If you're short of resources, you can use just one server, which will be your domain controller, and one client.**

    - Client VMs (for access and monitoring)
    - Domain Controller VM + DNS + DHCP + IIS (Active Directory installation)

1. Download and install Windows Server 2022 evaluation on the Server VM and Domain Controller VM.

![vm](https://github.com/boolunpeu/windows-101/assets/131985567/9a15e8c7-b266-4f3c-beb4-c63c8574848b)


#### **Must have** :
**2. Active Directory Setup:**

1. Promote the Domain Controller VM to a domain controller.
2. Create a new Active Directory forest and domain structure.

![static ip](https://github.com/boolunpeu/windows-101/assets/131985567/8b7f8512-f2d7-49f2-88e7-c397802a9527)

(here we can see that i have a static ip and a domain controller) 

3. Configure DNS service on the Domain Controller VM.
   
4. Create organizational units (OUs) for user and group management.

![test ou](https://github.com/boolunpeu/windows-101/assets/131985567/9422c63b-6ade-435b-8594-d57d0ef55964)

   
5. Join the Server VM and Client VMs to the domain.

![connection domain](https://github.com/boolunpeu/windows-101/assets/131985567/42f10d51-b222-4b23-98c3-17bbde9c9fc9)


**3. User Management with Alice and Bob:**

1. Create user accounts within Active Directory:
    - Alice (Administrator, assigned to dedicated OU)

![alice member of](https://github.com/boolunpeu/windows-101/assets/131985567/7c30bb70-2cce-40fb-9691-b224790031e6)


	- Bob (Standard User with access to `/Users/Bob` folder, assigned to specific OU)

![bob user](https://github.com/boolunpeu/windows-101/assets/131985567/4bc59434-eea6-4684-aa97-214fbe089f62)


1. Leverage Group Policy Objects (GPOs) to configure user settings based on OUs.
2. Implement granular permissions based on security principles for both Alice and Bob.


**4. Server Roles:**

**4.1 IIS for Alice:**

1. Install and configure [IIS](https://www.iis.net/overview) on the Server VM for Alice's specific web application/service.

![Uploading IIS.PNG…]()


2. Apply robust security best practices (permissions, WAFs, considering Alice's admin role).

![permission for group in OU](https://github.com/boolunpeu/windows-101/assets/131985567/3fd4cefc-408d-4474-ac5f-1dc10e091c25)

    
3. Test the web application and ensure accessibility for authorized users in the domain.
    

**4.2 DNS:**

1. Verify DNS functionality within the Active Directory domain environment.

![dnnsss](https://github.com/boolunpeu/windows-101/assets/131985567/84d245a6-8c91-4afd-acaa-0b1124486850)


3. Configure conditional forwarders or external DNS integration if needed.

![forward dns](https://github.com/boolunpeu/windows-101/assets/131985567/8830c666-8102-4870-91ac-60361f49637d)

**4.3 DHCP:**

1. Install and configure DHCP on the Server VM for automatic IP assignment within the domain.

![dhcp](https://github.com/boolunpeu/windows-101/assets/131985567/72301034-25f9-4be6-af24-b9969ed93fec)

#### **Cool to have** :

**5. Sysmon Monitoring:**

1. Install and configure your chosen [Sysmon monitoring](https://syedhasan010.medium.com/sysmon-how-to-setup-configure-and-analyze-the-system-monitors-events-930e9add78d) solution on the Server VM.
2. Configure Sysmon to capture relevant events and filter noise specific to your domain environment and user activities (e.g., Alice's admin actions, Bob's file access).
3. Demonstrate Sysmon functionality by simulating suspicious activities and capturing events related to both Alice and Bob.

**6. Client-Side Access and Reporting:**

1. Connect to the Server VM from the Client VMs using domain credentials (Alice and Bob).
2. Verify access based on assigned user permissions and GPOs, demonstrating differences between Alice and Bob's access levels.
3. Access and analyze Sysmon logs using your chosen solution.
4. Prepare a client-facing report highlighting captured events, potential security concerns related to both Alice and Bob, and Sysmon's value within the Active Directory domain.

