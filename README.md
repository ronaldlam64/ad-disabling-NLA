<p align="center">
<img src="https://i.imgur.com/RgTEis3.png" alt="Active Directory logo"/>
</p>

<h1>Active Directory Lab - Disable NLA</h1>
<p>While testing out features in AD, I'll encounter this error that prevents me from signing into my client VM with a client account called Network Level Authentication (NLA).</p>

<img src="https://i.imgur.com/WBAhkXZ.png" alt="NLA error"/>

<p>NLA verifies your credentials before establishing a full Remote Desktop session. But the NLA handshake depends on contacting the Domain Controller to validate your account if you're logging in with domain credentials. If the remote machine cannot reach the Domain Controller, the authentication fails, and the RDP connection is denied.</p>

In this lab, I will show how to disable NLA with a GPO so you can proceed with experimenting in AD without this inconvenience.
<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Remote Desktop
- Active Directory Domain Services
- VMWare (or Oracle Virtualbox)
- Command Prompt or Windows Powershell

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Windows Server 2022

<h2>List of Prerequisites</h2>

- Microsoft Azure
- Azure Virtual Machine
- VMWare or Oracle Virtualbox (To configure the Azure VMs)
- <a href="https://knowledge.broadcom.com/external/article/344595/downloading-and-installing-vmware-workst.html" target="_blank">Download link for VMWare</a>
- <a href="https://www.virtualbox.org/wiki/Downloads" target="_blank">Download link Oracle Virtualbox</a>
- <a href="https://drive.google.com/file/d/1gyYBmOUnoNJiZQi3vncEkILpBNRA1fHU/view?usp=sharing" target="_blank">Windows 10 Pro Download link</a>
- <a href="https://github.com/ronaldlam64/active-directory-deployment" target="_blank">Active Directory Installation and Setup</a>
  - **Please go through this tutorial first if you haven't setup an Active Directory lab yet.**
 
<h2>Implementation Steps</h2>

1. First, open Group Policy Management in the DC VM -> right click your domain name -> click "Create a GPO in this domain and link it here..." -> Name GPO as "Disable NLA" -> click OK

   <img src="https://i.imgur.com/Mir5kLR.png" alt="create GPO"/>

2. Right click on Disable NLA GPO and click Edit -> Computer Configuration -> Policies-> Administrative Templates -> Windows Components -> Remote Desktop Services

   <img src="https://i.imgur.com/x3k6lnF.png" alt="edit GPO"/>

3. Click Remote Desktop Session Host -> Security -> Require user authentication for remote connections by using Network Level Authentication

   <img src="https://i.imgur.com/r9zNdHg.png" alt="configure RD Session Host"/>

   Click Disabled -> Apply -> OK

   <img src="https://i.imgur.com/47b9rP8.png" alt="Disable NLA"/>

4. Open Command Prompt or Windows Powershell as an administrator -> type gpupdate /force to apply the GPO changes immediately

   <img src="https://i.imgur.com/ErAtWBd.png" alt="gpupdate /force"/>

   Check if the GPO is applied using gpresult /r under COMPUTER SETTINGS

   <img src="https://i.imgur.com/CIqr5NN.png" alt="gpresult /r"/>

   Now I can sign into the client VM without encountering the NLA error.

   <img src="https://i.imgur.com/kJnPHpX.png" alt="Sign in successful"/>
