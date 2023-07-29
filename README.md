<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>What is osTicket?</h2>

- osTicket is a widely-used open source support ticket system. It integrates inquiries created via email, phone and web-based forms into a simple easy-to-use multi-user web interface. Manage, organize and archive all your support requests and responses in one place to provide customers with accountability and responsiveness.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- Heidi SQL

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- osTicket Installation Files

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/VBjp96K.png" height="80%" width="80%" alt="Resource Group Setup"/>
</p>
<p>
First, we will set up a Resource Group (RG) in the Microsoft Azure Cloud Service. A resource group can be considered a folder that holds resources. We will name this resource group "osTickets" and set its location to US East. It is best practice to select the location closest to you. Please take note of the region where the RG is created, as it will be used in future instances.
</p>
<br />

<p>
<img src="https://i.imgur.com/DsA5UyJ.png" height="80%" width="80%" alt="Virtual Machine Setup"/>
</p>
<p>
Now, we will create a virtual machine under the RG. Think of the virtual machine as a computer on the internet you can access within your computer. As before, I will set my VM region to US East. We will be using Windows 10 with 4vCPUs. I'll name the virtual machine "VM-osTicket."

Next, create a username and password for your VM. Take note to remember your login credentials. I set my username to "labuser" and my password to "Password1". In the real world, never do this. You should always create a complex password. However, for this demonstration, it is okay. 

Now that our machine is ready, we will connect to it using Remote Desktop Connection. Before that, let us grab the public IP address of the VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/9a72kSn.png" height="80%" width="80%" alt="Public IP Address"/>
</p>
<p>
My IP address is "20.231.24.25". We will use this to connect to the VM using Remote Desktop Connection.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that we are connected, let us enable IIS (Internet Information Services ). ISS is a Microsoft web server that runs on the Windows operating system and is used to exchange static and dynamic web content with internet users. IIS can host, deploy, and manage web applications using technologies such as ASP.NET and PHP. 

Start Menu > Windows Feature > Internet Information Services > World Wide Web Services > Application Development Features > CGI.
</p>
<br />


<p>
<img src="https://i.imgur.com/YmpTa7K.png" height="80%" width="80%" alt="Internet Installation Services installation"/>
</p>
<p>
Now that we have this installed, let's download the installation files needed for osTicket and HeidiSQL.
</p>
<br />

<p>
<img src="https://i.imgur.com/n9NDKgB.png" height="80%" width="80%" alt="Internet Installation Services installation"/>
</p>
<p>
Now head to the installation folders.

•	From the Installation Files, download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi) 
•	From the Installation Files, download and install the Rewrite Module (rewrite_amd64_en-US.msi).

Create a directory C:\PHP.
</p>
<br />

<p>
<img src="https://i.imgur.com/BsYhvqG.png" height="80%" width="80%" alt="Create a PHP Folder in the C directory"/>
</p>
<p>
Download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) from the Installation Files and unzip the contents into C:\PHP 

•	From the Installation Files, download and install VC_redist.x86.exe. 
•	From the Installation Files, download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi). 

Next, download osTicket, and extract the content to the folder c:\inetpub\wwwroot. Rename the folder "Upload" to "osTicket."
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open IIS Manager as an Admin, Register the PHP using the PHP folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In IIS Manager, open PHP Manager. We need to enable three extensions named php_imap.dll, php_intl.dll, php_opcache.dll Now reload IIS manager and make your way to "Sites > Default > osTickets. Click " Browse *:80" on the right to open the osTicket web interface.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
It should look like this.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Perfect. Now let's return to c:\inetpub\wwwroot\osticket\include. Look for the file named "ost-sampleconfig.php" We will rename it to "ost-config.php." Once completed, right-click the file, and open properties, under the security tab, "Disable Inheritance." Then Remove all new permissions, and give everyone permissions.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
HeidiSQL From the Installation Files, download and install HeidiSQL.

 •	Open Heidi SQL 
•	Create a new session, root/Password1 
•	Connect to the session 
•	Create a database called "osTicket" 

Let's return to osTicket in the web interface. Name the Helpdesk and remember your login credentials. 

##Continue Setting up osticket in the browser 

•	MySQL Database: osTicket 
•	MySQL Username: root 
•	MySQL Password: Password1 
•	Click "Install Now!"
</p>
<p>
<img src="https://i.imgur.com/cPxyIZe.png" height="80%" width="80%" alt="osTicket Installer"/>
</p>

<p>
<img src="https://i.imgur.com/TGmrZnu.png" alt="osTicket Installer Complete"/>
</p>
<br />

<p>
osTicket should be up and running with no issues. We will now move on the Post Installation Config.
</p>
<br />

