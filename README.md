# cpu_performance_check
Checking Slowframe machines during Unity

If you forget on how to use the tool, just simply execute the shell script ./scripts/utils/linux/slowframecheck -h

In order to execute the script please provide the IP and run the script as below 
./scripts/utils/linux/slowframecheck 129.227.181.218 

From this result we can say the below

1.CPU Frequency is Normal 

2.There are not much information from the dmsg log. 

3.Netstat and Segment Re-transmitted rate looks to be fine

4.Turbo Mode is enabled 

5.C-State is enabled. 


**Options you can use in the tool**

As also explained within the tool there are 8 Options you can use. 
By giving the option at the every end of the script indicates which Option you would like to use. 
As you can see in below box
*Note that Hyperthreading and Temperature are not included in the default setting (Running without any options). 

Options 
-h, --help HELP!!!	
This options gives you an idea of how to run the script

And provides you the option lists

 -d  Checking dmsge Only	
This option will provide you only dmesg logs of the machine

 -f  Checking Frequnecy Only	
This option will provide you only CPU Frequency of the machine

 -n  Checking Netstat Only	
This option will provide you only Nestat result of the machine

 -t  Checking Turbo Only	
This option will provide you only status of Turbo Mode of the machine

 -T  Checking Temperature Only	
This option will provide you only CPU Temperature of the machine

 -C  Checking C-State Only	
This option will provide you only status of C-State of the machin

 -y  Checking Hyperthreading Only	
This option will provide you only status of Hyperthreading of the machine



# C-state-diasble_tool

I. Objective of the tool

To disable C-state from GRUB level if the datacenter is unable to do it. 

In order to make sure the Frequency does not decrease even if it is at idle state. 



II. How to use the tool

This script does not check the status for C-State.

It will disable C-state and reboot the machine. Therefore, please make sure the machine is disabled in Gameforge. 

Once running the command as below, it will take 5 minutes since the machine needs to be rebooted to be checked again

./scripts/utils/linux/c-state-disable 46.23.78.211
46.23.78.211 C-State Disabled
The main idea here in the tool is to write and update it update-grub 

vi /etc/default/grub
 
GRUB_CMDLINE_LINUX="intel_pstate=disable intel_idle.max_cstate=0"
GRUB_CMDLINE_LINUX_DEFAULT="intel_pstate=disable intel_idle.max_cstate=0"


III. Expected Error 

The machine might not comeback from Reboot, so please raised this to the datacenter if that is the case. 

Also the script will check after 5 minutes again once the configuration is set. However, there are cases where the reboot takes long than 5 minutes, where it would return it is still enabled.

In that case make sure to run the script once again. 

# MTR-Tool

I. Objective of the tool

The objective of the tool is to get bi-directional MTR. Bi-directional MTR is getting MTR result from the troubled machine to the Monitoring machine. 

The purpose is to see where the problem is but mainly it is to provide this result to the Datacenter (DC). 

Many DCs tend to ask for bi-directional MTR result as to investigate further to see if they are the problem or their upstream providers are the culprit. 

Therefore we need to provide them once we see an outage - High latency / High Ping Loss. 

II. How to use the tool


If you forget on how to use the tool, just simply execute the shell script ./scripts/utils/linux/mtr-tool -h

Machine IP and the Monitor Machine of the Monitoring machines - or simply search it from Zabbix Tool (*.mon)

You will get the result as below.

**REMEMBER the locations have their own IDs for this script as mentioned in the how to use. 


If you have all the correct variables set it will work as below
Just be informed it takes time to load the result coming from each side so give it a 30s.

Example) henryle@jumpbox-1:~$ ./mtr-tool  129.227.187.30 SIG


III. Options you can use in the tool

 As also explained within the tool there are 4 Options you can use. 

By giving the option at the every end of the script indicates which Option you would like to use. 

As you can see in below box

-h, --help HELP!!!
-U  use UDP instead of ICMP echo
-T  use TCP instead of ICMP echo


-U Option is used when you need to measure Bi directional MTR result for UDP. 
-T Option is used when you need to measure Bi directional MTR result for TCP. 


IV. Expected Error Messages

If you see ssh is not possible, that indicates that the machine is unreachable.
ssh: connect to host 107.6.176.130 port 22: Connection timed out
Trying pinging that machine to double check if the machine is reachable. - Most likely they are unreachable by ping and ssh. 

If that's the case, raise a ticket to the Datacenter
