# zeek-hunting
This Splunk app Zeek_Hunting, is app that can be used to hunt for malicous activity in the Zeek logs. The app includes dashboards for the following Zeek logs:
  - conn.log                  
  - files.log                 
  - http.log                  
  - smb_files.log             
  - smb_mapping.log           
  - dns.log                  
  - smtp.log
  - ssh.log
  - rdp.log
  - ntlm.log
  - kerberos.log
  - ftp.log


  ![search picture](https://github.com/gageb1989/Splunk-App/blob/main/pictures/files.PNG)
  
## USE
This app makes it easy to hunt in the Zeek logs using Splunk. Zeek logs are stored in JSON format making it hard to read all the information in the logs. There are also fields that are not important to search for malicous behavior making it harder to parse through all the data. All the dashboards show only the most important feilds mking it easier to read the logs. You can see in the example of the conn.log below

![conn.log](https://github.com/gageb1989/Splunk-App/blob/main/pictures/conn.PNG)

### Searching
Using the search bar is the same as using the search bar on the main Splunk page. The feilds of the Zeek logs are renamed to make searching easier. For example, the source IP fields is named id.orig_h, which can be less efficient to type every time. That field was renamed to ip.src. This was done to also be the same is Wireshark filters, which more people are familiar with as well. The files.log in Zeek uses the rx_hosts for the source IP field making it more confusing for most. That was also renamed to ip.src as you can see in the picture below:

![fields picture](https://github.com/gageb1989/Splunk-App/blob/main/pictures/fields.PNG)

### Logical Expressions
All logical expressions that can be used in the main search bar can be used in the dashboards. 

You can search for an IP in the source or destination field as shown below:

![search picture](https://github.com/gageb1989/Splunk-App/blob/main/pictures/search.PNG)


It is also easy to use the NOT expression to filter out good traffic when hunting:

![not picture](https://github.com/gageb1989/Splunk-App/blob/main/pictures/not.PNG)


## Costimizing the App
It is easy to customize the app for your needs. Different feilds can be added in the source code by adding their name after the "table" portion in the code as shown below in the picture. It is also simple to add more dashboards for other Zeek files by copying the code and changing the sourcetype and any fields that are specific to that log.

![code picture](https://github.com/gageb1989/Splunk-App/blob/main/pictures/code.PNG)


## SETUP
Correct setup is very important when using this app. When setting up the Splunk forwarder DO NOT just list the folder location to forward logs. This will not index and sourctype the logs properly making the app not work. Make sure to set up the inputs.conf using the inputs.txt that has been provided.

EXAMPLE:
[monitor:///nsm/bro/logs/current/conn.log]

disabled = 0

followTail = 0

index = zeek

sourcetype = bro_conn
  
It is important that the index is set and the sourctype is set. The names can be changed but they need to match the names in the source code of the dashboard. Setting up the inputs.conf properly will ensure that all fields are indexed in Splunk properly and that the app works correctly. 

The zeek.spl file can be uploaded into Splunk like any other app and will be ready to use. 









