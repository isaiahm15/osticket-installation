<img src="https://miro.medium.com/v2/0*5C2XvKOhIcjjmd7A" height="75%" width="100%"/>
</h1>
This tutorial will guide you through installing osTicket, a ticketing system that can be used in help desk settings.
<br/>


<h2>Databases & Programs Used</h2>
<p>
 
- <b>MySQL</b>

- <b>Windows Features</b>

- <b>PHP</b>

- <b>Internet Information Services Manager (IIS)</b>

- <b>Microsoft Edge</b>

- <b>HeidiSQL</b>

</p>

<h2>Environments Used</h2>
<p>
 
- <b>Windows 10 Enterprise</b> (22H2)

<h2>Prerequisites</h2>

- <b><a href="https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0">osTicket Installation Files (Download)</a></b>
- <b>Windows 10 Enterprise (22H2) virtual machine setup through Azure</b>

<h2 align="center">Installing IIS with CGI</h2>

<p>Sign into your Windows 10 client, search for "Turn Windows features on or off", and click launch it. Then, check the box next to Internet Information Services and CGI. CGI will be located in the IIS folder under World Wide Web Services > Application Development Features > CGI.
<br><img src="https://github.com/user-attachments/assets/e43dcf16-fbb3-4a19-ac37-e77cc2345292" height="75%" width="100%"/>
<br/>
</p>

<p>Download the osTicket installation files from prerequisites section above. This .zip file contains all the installers and dependencies you need to get osTicket up and running without issue.
<br><img src="https://github.com/user-attachments/assets/029fcaa6-2836-4025-8c26-178b23b8ffcf" height="75%" width="100%"/>
<br/>
</p>

<p>Install these three programs from the installation files. PHPManagerForIIS_V1.5.0 will need some configuration after installation, but the other two installers are just dependencies.
<br><img src="https://github.com/user-attachments/assets/3a733049-156f-4a22-9de6-ad93e3495bb8" height="75%" width="100%"/>
<br/>
</p>

<p>Navigate to your C: drive and create a folder named "PHP". Then, extract all the files in php-7.3.8-nts-Win32-VC15-x86 (in osTicket installation files) to the "PHP" folder.
<br><img src="https://github.com/user-attachments/assets/1c3ec1ec-4412-4e13-96ed-00bc4bb2d7ec" height="75%" width="100%"/>
<br/>
</p>

<p>Launch the mysql-5.5.62-win32 installer. Once the initial MySQL is installed, enter "root" as the password in the MySQL Server wizard. (Make sure Enable root access from remote machines is checked)
<br><img src="https://github.com/user-attachments/assets/ce4d9e89-9439-4d43-9e5b-b2a5decee665" height="75%" width="100%"/>
<br/>
</p>

<p>Open up IIS Manager, select your VM from the list of connections, and click on the PHP Manager. Then, click on "Register new PHP version" and point the path to your "php-cgi.exe" file in your local PHP directory on the C: drive.
<br><img src="https://github.com/user-attachments/assets/2d43293b-f940-4324-aeef-e96bac30f5f5" height="75%" width="100%"/>
<br/>
</p>

<p>Access the osTicket-v1.15.8.zip and move the "upload" folder to C:\inetpub\wwwroot (this directory along with files in it were created when IIS and CGI were enabled). After the folder is transferred, rename the folder to "osTicket".
<br><img src="https://github.com/user-attachments/assets/a6842230-c787-4157-a9f6-50c058bc277d" height="75%" width="100%"/><img src="https://github.com/user-attachments/assets/3e9ca7e0-585c-4423-906c-af013cd96877" height="75%" width="100%"/>
<br/>
</p>

<p>Launch Microsoft Edge, type 127.0.0.1 into the address bar and press enter. The osTicket installation landing page should load here.
<br><img src="https://github.com/user-attachments/assets/5ae73182-c9d1-40f6-a2d0-065a80ed156e" height="75%" width="100%"/>
<br/>
</p>

<p>Return to IIS and navigate to the PHP Manager again. This time, select "Enabled or Disable an extension" under PHP Extensions. Then, enable php_opcache.dll, php_intl.dll, and php_imap.dll. Optionally, you can then refresh your osTicket landing page in Microsoft Edge to observe the newly enabled extensions from PHP Manager.
<br><img src="https://github.com/user-attachments/assets/ec33758d-2b32-4be7-bff8-b0bb1e6db992" height="75%" width="100%"/>
<br/>
</p>

<p>Install HeidiSQL from the osTicket installation files and launch it. Click "New" and create a new session named "osTicket". Configure the user/password to match your MySQL Server login (user:root and pass:root) and click "Open"
<br><img src="https://github.com/user-attachments/assets/c267116a-045f-4d9b-b0b4-b7e0a9c28241" height="75%" width="100%"/>
<br/>
</p>

<p>Navigate to C:\inetpub\wwwroot\osTicket\include > and rename "ost-sampleconfig.php" to "ost-config.php".
<br><img src="https://github.com/user-attachments/assets/6eeed21c-b283-4781-afdb-32efbb5b2fb1" height="75%" width="100%"/>
<br/>
</p>

<p>Access the file properties of the newly named ost-config.php file > Security > Advanced > Disable inheritance > Remove all inherited permissions from this object.
<br><img src="https://github.com/user-attachments/assets/dd694b1f-ef4b-4b6c-8c5d-f2e311623ef7" height="75%" width="100%"/>
<br/>
</p>

<p>Click "Add" and "Select a Principal". Type "Everyone" in the open field and click OK. Make sure before closing the permission windows entirely that the Permission Entry Type is set to Allow, and give full control permissions for "Everyone".
<br><img src="https://github.com/user-attachments/assets/7d232c19-99b0-4eeb-a26e-9902af812113" height="75%" width="100%"/><img src="https://github.com/user-attachments/assets/d3ae53c3-eb6a-472b-b1a4-e5696d0d155d" height="75%" width="100%"/>
<br/>
</p>

<p>Click "Continue" on your osTicket landing page and fill out the System Settings and Admin User section with custom passwords, usernames, and emails of choice (make sure you use different emails for each section here). Then,
<br><img src="https://github.com/user-attachments/assets/6768633f-4309-41ab-9a12-14b2552de352" height="75%" width="100%"/>
<br/>
</p>

<p>In your Windows Server client, open Group Policy Management from the "Tools" drop-down menu in Server Manager.
<br><img src="https://github.com/user-attachments/assets/dbaac5b8-58ff-404b-8b16-d887b2c99b97" height="75%" width="100%"/>
<br/>
</p>

