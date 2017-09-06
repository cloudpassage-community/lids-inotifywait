# lids-inotifywait
Hook inotifywait into LIDS to detect file changes

Use
-

This is sample code and is not officially supported.  

Pre-requisites
-

1) Install inotify-tools for your OS

Command Example
-

sudo inotifywait -d -e modify,move_self -o /var/log/inotify_log /home/ec2-user/ /etc/test_config

-d run in background as a daemon  
-e events (a full list of events that can be monitored are at [https://linux.die.net/man/1/inotifywait])  In this
we are monitoring for modifications and self moves (caused by vi for example when a file is moved temporarily before
being written causing inotify to stop monitoring it)  
-o log to file

directories or files to monitor.  In this example we are watching the directory /home/ec2-user/ and the file 
/etc/test_config  


Events
-

Events can be detected using LIDS.  They can be seen in the Event monitor or can be sent to a SIEM.

Example:

2017-09-06T21:26:33.951Z	Log-based intrusion detection rule matched

Log-based intrusion detection rule A watched file or directory was moved. After this, the file or directory is no longer being watched. matched on Linux server ip-172-31-1-145 (54.xxxxxx.139, i-011972ea226a54e1c). (source: lids-inotifywait) - Hide Details
cloudpassage	ip-17xxxxx45	
/etc/test_config MOVE_SELF

LIDS Policy
-

See lids-inotifywait.json
 
