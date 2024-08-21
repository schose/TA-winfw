# Technology Add-On for Windows Firewall

The Splunk Technology Add-On for Windows Firewall provides extractions and CIM normalization for Windows Firewall Logs.


## Activation of Firewall Logging in Windows

To activate logging of Windows Firewall events run the "Windows Firewall with Advanced Security" App or simply run WF.msc from command line.
<ul>
<li>select "Windows Firewall properties"
<li>select "Customize..." in the "Logging" section
<li>define logfile location, logging settings (log dropped/allowed packets) and logfile size.
It's recommended to increase the logfile size to the maximum possible (32MB).
</ul>

<img src="https://www.batchworks.de/dateien/index.php/apps/files_sharing/ajax/publicpreview.php?x=600&y=848&a=true&file=hc_175.png&t=7k1taBr5kN0hy8H&scalingup=0" >


As soon as configured the logfile will be created and look similar to this:
<pre>
2016-08-31 10:47:42 ALLOW TCP 185.16.111.4 185.16.111.7 51171 10000 0 - 0 0 0 - - - SEND
2016-08-31 10:47:51 ALLOW UDP fe80::8182:6f65:d54f:3c64 ff02::1:2 546 547 0 - - - - - - - SEND
2016-08-31 10:47:51 ALLOW UDP fe80::4805:6c5e:a242:a171 ff02::1:2 546 547 0 - - - - - - - SEND
2016-08-31 10:47:52 DROP TCP 185.16.111.7 185.16.111.4 8089 51170 40 FA 2826662512 1602666708 63360 - - - RECEIVE
2016-08-31 10:48:06 ALLOW UDP fe80::8182:6f65:d54f:3c64 ff02::1:2 546 547 0 - - - - - - - SEND
2016-08-31 10:48:06 ALLOW UDP fe80::4805:6c5e:a242:a171 ff02::1:2 546 547 0 - - - - - - - SEND
2016-08-31 10:48:12 ALLOW TCP 185.16.111.4 185.16.111.7 51172 10000 0 - 0 0 0 - - - SEND
</pre>

## Installation and Deployment of TA-winfw

Download this TA and place it in etc/apps on your Searchhead and Universal Forwarders.

The default file input is deactivated by default. To collect data on the Forwarder make sure to create a local/inputs.conf file like this:

<pre>
[monitor://C:\Windows\system32\LogFiles\Firewall\pfirewall.log]
disabled = false
sourcetype = winfw
</pre>


Verify the data input and extraction works by searching for:

<pre>
sourcetype=winfw tag=network tag=communicate
</pre>
