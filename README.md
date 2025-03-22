## Installing and Setting Up osTicket on an Azure Windows 10 VM

  

This guide walks through setting up **osTicket**, a popular open-source helpdesk and ticketing system, on a **Windows 10 virtual machine** in Azure. The process involves **creating the VM**, **installing dependencies**, **configuring IIS and PHP**, **setting up MySQL**, and **finalizing the osTicket installation**.

----------

**Step 1: Create a Windows 10 VM in Azure**

• **VM Name**: osticket-vm

•  **vCPUs**:  4  (for better performance)

• **Username**: labuser

• **Password**: osTicketPassword1!

  

💡  _Explanation_:

•  Azure allows you to create virtual machines to host software applications.

•  A  **4-core CPU**  provides sufficient resources for osTicket and its dependencies.

----------

**Step 2: Log Into the Virtual Machine**

•  Use  **Remote Desktop (RDP)**  to connect to the  osticket-vm.

• **Login credentials**:

•  Username:  labuser

•  Password: osTicketPassword1!

  

💡  _Explanation_:

•  RDP allows you to remotely control your Azure VM just like a physical computer.

----------

**Step 3: Prepare Installation Files**

1. **Download** the osTicket-Installation-Files.zip onto the desktop.

2.  **Unzip**  the file.

3.  A new folder called  osTicket-Installation-Files  will appear.

  

💡  _Explanation_:

•  This folder contains  **all necessary components**  to install osTicket and its required software.

----------

**Step 4: Install IIS and Enable CGI**

1.  Open  **Windows Features**  and enable:

• **Internet Information Services (IIS)**

• **World Wide Web Services** → **Application Development Features** → **CGI**

  

💡  _Explanation_:

•  **IIS (Internet Information Services)**  is a web server that will host the osTicket web application.

•  **CGI (Common Gateway Interface)**  is needed to allow IIS to process PHP scripts.

----------

**Step 5: Install IIS Dependencies**

  

From the  osTicket-Installation-Files  folder, install the following:

1. **PHP Manager for IIS** (PHPManagerForIIS_V1.5.0.msi)

•  Allows IIS to manage PHP settings easily.

2. **Rewrite Module** (rewrite_amd64_en-US.msi)

•  Enables URL rewriting, which is necessary for clean URLs in osTicket.

----------

**Step 6: Install and Configure PHP**

1.  Create the folder  C:\PHP.

2.  Extract **PHP 7.3.8** (php-7.3.8-nts-Win32-VC15-x86.zip) into C:\PHP.

3.  Install  **VC_redist.x86.exe**  (Visual C++ Redistributable).

  

💡  _Explanation_:

•  **PHP (Hypertext Preprocessor)**  is the programming language osTicket is built with.

•  The  **Visual C++ Redistributable**  is required to run PHP on Windows.

----------

**Step 7: Install MySQL**

1.  Install **MySQL 5.5.62** (mysql-5.5.62-win32.msi).

2.  Choose  **Typical Setup**  during installation.

3.  After installation, launch the  **Configuration Wizard**:

•  Select **Standard Configuration**.

•  Set the **root user credentials**:

• **Username**: root

• **Password**: root

  

💡  _Explanation_:

•  MySQL is the  **database**  where osTicket will store ticket data.

•  The  **root user**  is the default administrator for MySQL.

----------

**Step 8: Configure IIS for PHP**

1.  Open **IIS Manager** as an **Administrator**.

2.  Register PHP with IIS:

•  In IIS, go to  **PHP Manager**  → Select  C:\PHP\php-cgi.exe.

3.  Reload IIS by stopping and starting the  **IIS service**.

  

💡  _Explanation_:

•  This step tells IIS where PHP is installed so it can execute PHP scripts.

----------

**Step 9: Install osTicket**

1.  Extract osTicket-v1.15.8.zip from osTicket-Installation-Files.

2.  Copy the  **“upload”**  folder into  C:\inetpub\wwwroot.

3.  Rename upload to osTicket.

4.  Restart IIS.

  

💡  _Explanation_:

•  The  wwwroot  directory is the  **default web directory**  for IIS, where websites and applications are hosted.

----------

**Step 10: Access osTicket via Web Browser**

1.  Open IIS Manager.

2.  Navigate to:

• **Sites** → **Default Web Site** → **osTicket**

3.  Click *_Browse :80_.

  

💡  _Explanation_:

•  Port  80  is the  **default HTTP port**.

•  osTicket should now load in a web browser.

----------

**Step 11: Enable Required PHP Extensions**

1.  In IIS, go to:

• **Sites** → **Default Web Site** → **osTicket**

2.  Open **PHP Manager** → **Enable or disable an extension**.

3.  Enable:

•  php_imap.dll  (Email handling)

•  php_intl.dll  (Internationalization)

•  php_opcache.dll  (Performance optimization)

4.  Refresh osTicket in the browser.

  

💡  _Explanation_:

•  These PHP extensions enable **email functionality, localization, and caching** for osTicket.

----------

**Step 12: Configure osTicket**

1.  Rename ost-sampleconfig.php to ost-config.php:

• **From**: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php

• **To**: C:\inetpub\wwwroot\osTicket\include\ost-config.php

2.  Assign permissions to  ost-config.php:

• **Disable inheritance** → **Remove all** permissions.

• **Grant “Everyone” full control**.

  

💡  _Explanation_:

•  The configuration file stores critical database settings, so it needs  **proper permissions**.

----------

**Step 13: Install HeidiSQL and Configure Database**

1.  Install **HeidiSQL** from osTicket-Installation-Files.

2.  Open  **HeidiSQL**  and create a  **new session**.

3.  Connect using:

• **Username**: root

• **Password**: root

4.  Create a  **new database**  called  osTicket.

  

💡  _Explanation_:

•  **HeidiSQL**  is a GUI for managing MySQL databases.

•  The  **osTicket database**  will store all ticketing system data.

----------

**Step 14: Finalize osTicket Installation in the Browser**

1.  In the browser, continue the osTicket setup:

•  **Helpdesk Name**:  _(Choose a name)_

•  **Default Email**:  _(Enter an email for customer tickets)_

2.  Enter **database details**:

• **MySQL Database**: osTicket

• **MySQL Username**: root

• **MySQL Password**: root

3.  Click **Install Now!**

  

💡  _Explanation_:

•  This step  **connects osTicket to MySQL**  and finalizes the setup.

----------

**Step 15: Access osTicket**

  

✅ **Admin Login Page**:

```
http://localhost/osTicket/scp/login.php
```

✅ **End-User Support Portal**:

```
http://localhost/osTicket/
```

🎉 **Congratulations! osTicket is now installed and running on your Azure VM!** 🎉

----------

**Summary & Significance**

  

**What You Did:**

•  Set up a  **Windows 10 VM**  in Azure.

•  Installed  **IIS, PHP, MySQL**, and necessary dependencies.

•  Configured  **IIS**  to run PHP applications.

•  Installed and configured  **osTicket**.

  

**Why This Matters:**

•  osTicket is widely used for **IT support and customer service ticketing systems**.

•  Understanding  **IIS, PHP, and MySQL**  integration is valuable for  **system administration**.

•  This project provides hands-on experience with **server configuration, database management, and web application hosting**.

----------

This guide ensures a clear, step-by-step understanding of the process! Let me know if you need any modifications. 🚀
