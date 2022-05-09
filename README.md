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
