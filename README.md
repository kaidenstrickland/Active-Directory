<h1>Active Directory Lab</h1>

<h2>Objective</h2>
To create a functional Windows Domain environment by provisioning a Domain Controller, integrating a client workstation, and creating user accounts through scripting.
<br />

<h2>Project Summary</h2>
In this lab, I deployed two Virtual Machines, promoting a Windows Server to a Domain Controller while configuring network protocols including AD DS, DNS, NAT, and DHCP. I then connected a Windows 10 client to the domain and to verify dynamic IP addressing through DHCP scope and lease confirmation.
<br />

<h2>Languages and Utilities Used</h2>

- <b>Active Directory</b> 
- <b>PowerShell</b>

<h2>Environments Used </h2>

- <b>Windows Server 2022</b>
- <b>Windows 10</b>
<br>

<h2>Lab Report:</h2>
<br>


<p align="left">
<h2>Step 1: Installing/Configuring the Windows Server through VirtualBox</h2>
 
- <b>Purpose: Create an internal private network for our lab and install the Windows Server which will serve as the Domain Controller. 2 network interfaces are used: NAT adapter for external connectivity and an internal adapter for our private LAN.</b>

<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/7d14d019-9700-4767-8bdf-fd461f8e01d3" />
 <p align="center">
 - <b>NAT Adapter</b>

<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/3b4d240d-e8d9-4a83-b3c0-ab88f6920d45" />
 <p align="center">
 - <b>Internal Adapter</b>

 <p align="center">
 <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/011dbfdc-e7a9-483c-876d-2d0db202a690" />
<p align="center">
- <b>Windows Server</b>


<h2>Step 2: Configure the virtual interfaces and IPv4 addressing for the Internal Network</h2>
 
- <b>To give the internal network interface a static ip so there are no routing issues to the DC, and we set the default gateway to the same ip (or loopback) so the server uses itself as the DNS.</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/05c6fc9c-3c34-4f1f-b697-197edae576e7" />
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/a18cc67d-56be-43e0-ab28-48a7e733755b" />

<h2>Step 3: Active Directory Installation and Setup</h2>
 
- <b>To create our domain and begin setting up our environment with an Admin group and adding a user account.</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/b6a54b47-1336-4670-a666-9ea7ac06cf17" />
<p align="center">
- <b>Active Directory Install</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/34e0e1b3-dd8d-4b7d-8f8e-e67e73e02975" />
<p align="center">
- <b>Domain Deployment</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/6f84a52f-1f70-4bfc-8909-12fc1e6b3ec3" />
<p align="center">
- <b>Creation of Admin OU</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/ba62a301-f8f7-4917-9673-950205a8afb4" />
<p align="center">
- <b>Admin Account Creation</b>

<h2>Step 4: Routing and NAT</h2>
 
- <b>To transform our DC into a router by installing Remote Access and routing role services so that our internal traffic can be routed outside of our network. This is paired with NAT where our internal machines can access the internet from a single ip address because their private ones are unrouteable outside of the network.</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/057889ea-fe52-4248-a3af-1fb8de26a1c0" />
<p align="center">
- <b>Remote Access Install</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/37db3751-f5ad-4277-b60f-6a6c39b4b2a1" />
<p align="center">
- <b>Routing Role Services</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/120479b2-0797-4554-b9f6-3daa679588cf" />
<p align="center">
- <b>NAT through the DC public interface for internet connectivity</b>

<h2>Step 5: DHCP and DNS Configuration</h2>
 
- <b>We install DHCP so that our DC can automatically manage and assign ip addresses on the internal network. We configure DNS like before so that all traffic is routed through the internal network interface on its way to the internet.</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/dab98bcb-6022-4536-a362-d2bcc84eee56" />
 <p align="center">
- <b>DHCP and DNS Install</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/9ff1d761-c1c3-4493-a95b-3e5ee0964ed3" />
 <p align="center">
- <b>Traffic goes to the DC for routing</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/8c6f2fe0-33ac-4505-9f55-aa6361bd6771" />
<p align="center">
- <b>DNS through the DC</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/70c1b983-4cfa-4acb-8b6d-a5f10626fb29" />
<p align="center">
- <b>Confirmation of the DHCP and the scope (172.16.0.100-200)</b>

<h2>Step 6: User account creation using powershell script</h2>
 
- <b>Purpose: To create a pool of user accounts with a standardized attritbutes to serve as subjects for different departments or groups for future assignments.</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/be0a1a5a-299a-419a-81d7-d69ae926e961" />
 <p align="center">
- <b>PowerShell script</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/b74e8e66-a7ce-471c-93d5-61a15c1311b1" />
<p align="center">
- <b>Text file of our employee names</b>
 <p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/4f68d8db-fba2-4450-84ed-115349544e46" />
<p align="center">
- <b>Ouput of the script</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/3e5a72c0-092e-4dc2-bfc6-9b186bb3f134" />
<p align="center">
- <b>New user accounts created in Active Directory</b>

<h2>Step 7: Client Workstation</h2>
 
- <b>To join a user workstation to the domain to observe the DHCP addressing and leasing.</b>
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/d17faeaf-5d4d-418e-bc39-45cf033e833e" />
<p align="center">
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/39ddec99-fb6c-4790-aa3f-5bb62b2e8586" />

<h2>Final Summary</h2>
The objective of this lab was to build a functional enterprise network infrastructure and to manage centralized identities with routed connectivity. By using Windows Server Domain Controller and a client workstation, I successfully simulated a managed corporate environment where all network services are controlled from a single focal point. Utilizing Active Directory, DNS, and DHCP, I automated user lifecycle management and network addressing, while the implementation of the Remote Access role and NAT allowed the isolated client to securely access the internet through the DC’s public interface. 
<br />

<h2>Key Takeaways:</h2>

- <b>Active Directory:</b> I learned that Active Directory serves as the source of control for the network, where the creation of a domain allows for Organizational Units and Security Groups that govern user permissions and domain-wide security.
- <b>Automated DHCP Efficiency: </b> Deploying a DHCP scope demonstrated how critical automated addressing is for scalability, by configuring the scope options to distribute the DC’s IP as both the DNS server and the Default Gateway, I ensured that any client joining the Internal Network received the necessary configuration to communicate across the domain.
- <b>Precision in Static Inputs: </b> This lab taught me that networking requires a great attention to detail. Misinputting a single digit in the static IPv4 address or the NAT gateway settings prevents the internal traffic from being routed correctly.

<h2>Troubleshooting</h2>
- <b>Static IPs </b> As mentioned above, during this lab I had instances of misconfigured static IPs for some services which can be seen in some of the screenshots. What was supposed to be 172.16.0.1 ended up being 172.160.0.1 which caused problems in my network communication. Static routing has its benefits but ensuring the addresses are correct are vital to the network availability.
