<p align="center">
<img src="https://i.imgur.com/MwrkwEQ.png" alt="DNS Photo"/>
</p>

<h1>Understanding DNS</h1>
This lab focuses on DNS and how it is used. DNS is a fundamental concept in IT. I will be configuring DNS records and seeing how it works in practice. This is building up from a previous lab where I have a client joined to my domain. I'm logged in as Jane Doe (admin) on both the client and domain controller VMs, and administrative access is required for this lab. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>DNS Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/5pjgtVz.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/Zl04Jyt.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/96xUgLF.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
DNS Configuration Steps
1. Creating A-Record:

- Log in to the client VM as an admin and open the command prompt.
- Ping "mainframe" (it will fail) and run nslookup "mainframe" (no DNS record found).
- On the domain controller, open DNS Manager, go to Forward Lookup Zones for ernestotest.com, and create a new Host with the name "mainframe" and the IP address of the domain controller. Refresh the DNS server and ping "mainframe" again—it should now resolve.
</p>
<br />

<p>
<img src="https://i.imgur.com/nLlOGKl.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/p0VcajB.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/ds0SCKW.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/d4cXTCS.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
2. DNS Cache Exercise:

- Change the mainframe's record address to 8.8.8.8 (Google) on the domain controller and refresh the DNS server.
- Ping "mainframe" on the client (it still pings the old IP).
- Run ipconfig /displaydns to view the DNS cache, which shows the old IP.
- Clear the cache with ipconfig /flushdns, then ping "mainframe" again to see the updated IP.
</p>
<br />

<p>
<img src="https://i.imgur.com/rI2NYU7.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/FmVM0IU.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/dyWduSW.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
3. Creating CNAME Record:

- In DNS Manager, create a new CNAME record called "search" pointing to Google. Refresh the server to save changes.
- On the client, ping "search" and run nslookup to confirm the CNAME record works.
</p>
<br />

<h2>Lessons Learned </h2>

This lab enhanced my understanding of DNS. I learned that changes to DNS records can cause connectivity issues and that clearing the DNS cache with ipconfig /flushdns is often necessary to update records. The system checks the DNS cache first, then the host file, and finally the DNS server. Creating a DNS record allowed successful pings to "mainframe," and a CNAME record enabled "search" to point to Google.
