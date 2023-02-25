<p align="center">
<img src="https://i.imgur.com/PPZWJaI.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Building Intuition For DNS</h1>

- DNS converts computer names and/or websites (such as Client-1.mydomain.com or www.google.com) to IP addresses which can be used by the computer to locate resources
- DNS is integrated with Active Directory and automatically got installed on DC-1 in the last tutorial [here](https://github.com/jnoriega232/configure-ad)
- In this tutorial we will use Client-1 and DC-1 to do a few exercises for the sake of understanding DNS a bit better

<h3>Overview (What we will be doing):</h3>

- Inspect DNS A-Records on the server (hostname to IP address mappings)
- Create some of our own A-Records on the server and observe them from the client
- Delete records from server and inspect/clear the client DNS cache to gain understanding
- Touch on "CNAME" records (mapping one name to another name)
- Discuss Root Hints

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


**Note: Forward Lookup Zones = hostname to IP address mapping & Reverse Lookup Zones = IP address to hostname mapping**


<p align="center">
<img src="https://i.imgur.com/CUW3Q8A.png" height="70%" width="70%" alt="Azure Free Account"/> <img src="https://i.imgur.com/u5qY0og.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

- We will manually create a new A-Record
  - Right-click near current list and select "New Host (A or AAAA)..." 
  - Name: mainframe
  - IP address: 10.0.0.4 (We will set it to DC-1's private IP address for a successful ping)
  - Select Add Host

<p align="center">
<img src="https://i.imgur.com/ZYWfLE8.png" height="70%" width="70%" alt="Azure Free Account"/> <img src="https://i.imgur.com/sFmduHK.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

- You should now be able to see "mainframe" in our list of A-Records

<p align="center">
<img src="https://i.imgur.com/pZ2sjFi.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

**Step 6:** Go back to Client-1 and try to ping "mainframe". Observe that it works

<p align="center">
<img src="https://i.imgur.com/knKbNzY.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

- Now if we nslookup mainframe we can see DC-1's server returned mainframe's record

<p align="center">
<img src="https://i.imgur.com/udxqW6n.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

<h3><ins>Local DNS Cache Exercise</ins></h3>

**Step 1:** Go back to DC-1 and change mainframe's record address to 8.8.8.8

- Double-click mainframe's A-Record we made > update it to 8.8.8.8 > Apply > OK

<p align="center">
<img src="https://i.imgur.com/MdmlW71.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>


- In Client-1 use Command Propmt to enter the comand "ipconfig /displaydns" to see the local DNS cache

<p align="center">
<img src="https://i.imgur.com/L5gEFUA.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

-If we scroll down we can see the record of mainframe has resolved
  -We can see mainframe's record name: mainframe.mydomain.com maps to A (Host) Record: 10.0.0.4
  
<p align="center">
<img src="https://i.imgur.com/WeStr8p.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>
