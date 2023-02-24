<p align="center">
<img src="https://i.imgur.com/PPZWJaI.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Building Intuition For DNS</h1>

- DNS converts computer names and/or websites (such as Client-1.mydomain.com or www.google.com) to IP addresses which can be used by the computer to locate resources
- DNS is integrated with Active Directory and automatically got installed on DC-1 in the last tutorial [here](https://github.com/jnoriega232/configure-ad)
- In this tutorial we will use Client-1 and DC-1 to do a few exercises for the sake of understanding DNS a bit better


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Prompt


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Requirements</h2>

- Active Directory running in Azure on a virtual machine (DC-1)
- A client machine running in Azure on a virtual machine (Client-1) and joined to the domain


<h2>Practice Exercises</h2>

<h3><ins>A-Record Exercise</ins></h3>

<h3>Overview (What we will be doing):</h3>

- Inspect DNS A-Records on the server (hostname to IP address mappings)
- Create some of our own A-Records on the server and observe them from the client
- Delete records from server and inspect/clear the client DNS cache to gain understanding
- Touch on "CNAME" records (mapping one name to another name)
- Discuss Root Hints
	


**Step 1:** Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
       
<p align="center">
<img src="https://i.imgur.com/YBZsKda.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

**Step 2:** Connect/log into Client-1 as an admin (mydomain.com\jane_admin)

<p align="center">
<img src="https://i.imgur.com/CZBuWaw.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

**Step 3:** From Client-1 try to ping the hostname "mainframe" (currently nonexistent)
- Search and open Command Prompt
  - ping "mainframe"
  - notice it fails
 
 <p align="center">
<img src="https://i.imgur.com/BmGemOx.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

**Step 4:** Nslookup mainframe and notice that it fails (no DNS record)

<p align="center">
<img src="https://i.imgur.com/OdKI56J.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

**Step 5:** Create a DNS A-Record on DC-1 for "mainframe" and have it point to DC-1's private IP address

- Go back to DC-1 and open Server Manager
  - Go to Tools > DNS
  - On the left hand side, select and expand DC-1 > expand Forward Lookup Zones > select mydomain.com (here you can see the current list of A-Records

*Forward Lookup Zones = hostname to IP address mapping*
*Reverse Lookup Zones = IP address to hostname mapping*

<p align="center">
<img src="https://i.imgur.com/CUW3Q8A.png" height="70%" width="70%" alt="Azure Free Account"/> <img src="https://i.imgur.com/u5qY0og.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>


