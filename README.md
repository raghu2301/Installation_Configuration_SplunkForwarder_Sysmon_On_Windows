# Installation_Configuration_SplunkForwarder_Sysmon_On_Windows
## Objective:
1. Changing Dynamic IP to Static IP.
2. Downloading and Configuration of splunk forwarder and Sysmon.


# 1. Changing Dynamic IP to Static IP
Follow the following steps to change the Dynamic IP to Static IP
- Goto Network and Internet setting.
- Click on Change adapter option.
- Click on Change IPv4.
- Click Properties.
- Check Use the following IP.
  ![image](https://github.com/user-attachments/assets/1d014982-35ed-441c-b909-101f9ebc58e7)

# 2. Downloading and Configuration of Splunk Forwarder and Sysmon
**Installing Splunk Forwarder**
- Go to [Splunk Forwarder download page.](https://www.splunk.com/en_us/download.html)
- Download and install Splunk Forwarder.
- Set Hostname or IP to 192.168.10.10 and port number to 9997.
![image](https://github.com/user-attachments/assets/faa1e77b-695e-4c86-978d-5c3dcb91fc41)

 (Host IP is 192.168.10.10 because we created a [Splunk Server](https://github.com/raghu2301/Ubuntu_Server_Installation/blob/main/README.md) And we want to direct the data there)

**Installing and Configuring Sysmon**
- Goto [Sysmon Download link](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
- For Sysmon we will be using configuration by OLAF
  - Goto sysmon configuration by olaf [github page](https://github.com/olafhartong/sysmon-modular)
  - Click on [sysmonconfig.xml](https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml)
  - Click on **Raw**.
  - Right click on page and select **save as** and save the file.
  - Extract the Sysmon file which is downloaded.
  - Goto the extracted folder.
  - Click on file explorer bar and copy the path.
  - Open Powershell in administrator mode.
  - Change the directory to the sysmon folder.
  - Enter the following command.
```
.\sysmon64.exe -i ..\sysmonconfig.xml
```
 - Click on agree.


**Configuring Splunk Forwarder**
Now most **important** part:
We need to instruct our splunk forwarder on what we want to send over to splunk server.
For that we must configure a file named **inputs.conf**

Path location of **inputs.conf**
C:\Program Files\SplunkUniversalForwarder\etc\system\default

But we will not be editing this file rather we will create a new file on local folder.
Path location:
C:\Program Files\SplunkUniversalForwarder\etc\system\local

Copy the following [Configuration](https://github.com/raghu2301/Installation_Configuration_SplunkForwarder_Sysmon_On_Windows/blob/main/inputs.conf) into a notepad and save it as **inputs.conf** in the path location:
C:\Program Files\SplunkUniversalForwarder\etc\system\local

Whenever there is change in configuration file, Forwarder must be restarted.
To Restart Forwarder:
- Search **services**
- Run it as adminstrator.
- Find Splunk Forwarder.
- Check for **Log On As**
- Change it to **Local System account**
![image](https://github.com/user-attachments/assets/d3d4a6ea-6132-4481-bb6a-e90b8339e621)

Goto splunk web page and login using username and password for splunk
Splunk web page:
192.168.10.10:8000 (as i have set it for me for my [Ubuntu Server](https://github.com/raghu2301/Ubuntu_Server_Installation/blob/main/README.md)]

http://127.0.0.1:8000/ (for local system)
- Goto **Settings**
- Click on **indexes**
- Click on **New Index**
  
![image](https://github.com/user-attachments/assets/2c0de02c-81bd-4ffa-8529-19bac50e60c2)

Change **Index Name** to endpoint.

Save it.

Now we need to ensure we enable our splunk server to receive data.
We need to follow the steps:

 - Setting >  forwarding and receiving > reviece data (configure receiving) > new receiving port: 9997
 - Apps > search and reporting –>search bar
   type **index=endpoint** and search.

  # Conclusion
We have sucessfully installed and configured **Splunk Forwarder** and **Sysmon** on our windows system 


