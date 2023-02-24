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
 
 When Client-1 tries to ping nonexistent hostname "mainframe"
 
 <p align="center">
<img src="https://i.imgur.com/BmGemOx.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>
  
 1. It checks the local DNS cache (no result)
  
  
 2. It checks the host file (no result)
  - Right-click the Start menu > Run > c:\windows\system32\drivers\etc\hosts > OK
    - Select Notepad > OK
    - Scroll down to see list of mappings of IP addresses to names (by default this host file is empty)

 <p align="center">
<img src="https://i.imgur.com/7XZ7FjY.png" height="70%" width="70%" alt="Azure Free Account"/> <img src="https://i.imgur.com/KV57s2s.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>

 3. It checks the DNS server assigned to the Network Interface Card (no result)

**Step 4:** Nslookup mainframe and notice that it fails (no DNS record)

<p align="center">
<img src="https://i.imgur.com/OdKI56J.png" height="70%" width="70%" alt="Azure Free Account"/>
</p>
