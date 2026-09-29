**Steps**

**1**.Basic settings to all devices plus SSH on the routers and l3 switches.

2.VLANs assignment plus all access and trunk ports

3.Switchport security to all 12 switches.

4.Subnetting and IP addressing.

5.OSPF on the routers and l3 switches

6.Static IP address to server Room devices.

7.DHCP server device configurations.

8.Inter-VLAN routing on the l3 switches plus DHCP helper addresses

9.Wireless network configurations.

10.Verifying and testing Configurations





**STEP1 :Basic Configurations**

**1st Option**

**Layer 2 switches**

en

config t

hostname F1-Mgt-SW

banner motd #This Floor1-mgt switch#

enable password makupe123

line console 0

password makupe123

login

logging synchronous

exec-timeout 2

exit

line vty 0 15

password makupe123

exit

no ip domain-lookup

login

logging synchronous

exec-timeout 2

exit

service password-encryption

exit

do wr



**2nd Option**



en

config t

hostname F4-Server Room-SW

banner motd #This is Floor4-Server Room switch#

line console 0

password makupe123

login

exit



line vty 0 15

password makupe123

login

exit



no ip domain-lookup

enable password makupe123

service password-encryption



do wr



**Layer 3 switches \& Routers-with SSH configurations**



en

config t

hostname F4-Router

banner motd #This is F4-Router#

line console 0

password makupe123

login

exit



ip domain-name makupe.net

username makupe password makupe123

crypto key generate rsa

1024



line vty 0 15

login local

transport input ssh

exit



no ip domain-lookup

enable password makupe123

service password-encryption



do wr



**STEP 2 \& 3:VLANs-access switches**





int range fa0/1-2

switchport mode trunk

ex



vlan 120

name SR

ex



int range fa0/3-24

switchport mode access

switchport access vlan 120

switchport port-security

switchport port-security maximum 2

switchport port-security mac-address sticky

switchport port-security violation shutdown

do wr

exit



**STEP 4: Subnetting \& IP addressing**



**Layer 2 switches**

**Base Network: 192.168.10.0**





&#x20;                                 **First-Floor**

|**Department**|**Network Address**|**Subnet Mask**|**Hot Address Range**|**Broadcast Address**|
|-|-|-|-|-|
|Management|192.168.10.0|255.255.255.192/26|192.168.10.1 to 192.168.10.62|192.168.10.63|
|Research|192.168.10.64|255.255.255.192/26|192.168.10.65 to 192.168.10.126|192.168.10.127|
|Human Resource|192.168.10.128|255.255.255.192/26|192.168.10.129 to 192.168.10.190|192.168.10.191|





&#x20;                                 **Second Floor**

|**Department**|**Network Address**|**Subnet Mask**|**Hot Address Range**|**Broadcast Address**|
|-|-|-|-|-|
|Marketing|192.168.10.192|255.255.255.192/26|192.168.10.193 to 192.168.10.254|192.168.10.255|
|Accounting|192.168.11.0|255.255.255.192/26|192.168.11.1 to 192.168.11.62|192.168.11.63|
|Finance|192.168.11.64|255.255.255.192/26|192.168.11.65 to 192.168.11.126|192.168.11.127|





&#x20;                                 **Third Floor**

|**Department**|**Network Address**|**Subnet Mask**|**Hot Address Range**|**Broadcast Address**|
|-|-|-|-|-|
|Logistics|192.168.11.128|255.255.255.192/26|192.168.11.129 to 192.168.11.190|192.168.11.191|
|Customer|192.168.11.192|255.255.255.192/26|192.168.11.193 to 192.168.11.254|192.168.11.255|
|Guest|192.168.12.0|255.255.255.192/26|192.168.12.1 to 192.168.12.62|192.168.12.63|











&#x20;                                **Fourth Floor**

|**Department**|**Network Address**|**Subnet Mask**|**Hot Address Range**|**Broadcast Address**|
|-|-|-|-|-|
|Admin|192.168.12.64|255.255.255.192/26|192.168.12.65to 192.168.12.126|192.168.12.127|
|ICT|192.168.12.128|255.255.255.192/26|192.168.12.129 to 192.168.12.190|192.168.12.191|
|Server Room|192.168.12.192|255.255.255.192/26|192.168.12.193 to 192.168.12.254|192.168.12.255|





**Layer 3 switches \& Routers**



**Base Network Address: 10.10.10.0**

|**No.**|**Network Address**|**Subnet Mask**|**Hot Address Range**|**Broadcast Address**|
|-|-|-|-|-|
|1|10.10.10.0|255.255.255.252|10.10.10.33 to 10.10.10.34|10.10.10.35|
|1|10.10.10.4|255.255.255.252|10.10.10.37 to 10.10.10.38|10.10.10.39|
|3|10.10.10.8|255.255.255.252|10.10.10.41 to 10.10.10.42|10.10.10.43|
|4|10.10.10.12|255.255.255.252|10.10.10.45 to 10.10.10.46|10.10.10.47|
|5|10.10.10.16|255.255.255.252|10.10.10.49 to 10.10.10.50|10.10.10.51|
|6|10.10.10.20|255.255.255.252|10.10.10.53<br />to 10.10.10.54|10.10.10.55|
|7|10.10.10.24|255.255.255.252|10.10.10.33 to 10.10.10.34|10.10.10.35|
|8|10.10.10.28|255.255.255.252|10.10.10.37<br />to 10.10.10.38|10.10.10.39|
|9|10.10.10.32|255.255.255.252|10.10.10.41 to 10.10.10.42|10.10.10.43|
|10|10.10.10.36|255.255.255.252|10.10.10.45 to 10.10.10.46|10.10.10.47|
|11|10.10.10.40|255.255.255.252|10.10.10.49 to 10.10.10.50|10.10.10.51|
|12|10.10.10.44|255.255.255.252|10.10.10.53 to 10.10.10.54|10.10.10.55|
|13|10.10.10.48|255.255.255.252|10.10.10.33 <br />to 10.10.10.34|10.10.10.35|
|14|10.10.10.52|255.255.255.252|10.10.10.37<br />to 10.10.10.38|10.10.10.39|





**Trunk config in layer 3 switches**

int range gig1/0/3-8

switchport mode trunk

exit

do wr



NB: ENSURE YOU TURN THE LYER 3 SWITCH PORTS CONNECTED TO ROUTERS TO NO SWITCHPORT BEFORE IP ADDRESSING.

&#x20;   ENSURE YOU CONFIGURE CLOCK RATING IN THE SERIAL DCE CONNECTED PORTS

&#x20;    clock rate 64000







**STEP 5: OSPF Configurations**

What changes is the router-id and the network in each router and layer 3 switches.



**On Routers**

router ospf 10

router-id 3.3.3.3

network 10.10.10.40 0.0.0.3 area 0

network 10.10.10.48 0.0.0.3 area 0

network 10.10.10.36 0.0.0.3 area 0

network 10.10.10.20 0.0.0.3 area 0

network 10.10.10.32 0.0.0.3 area 0

do wr



**On Layer 3 Switches**



NB: Ensure you enable ip routing in the layer 3 switches before configuring ospf.



router ospf 10

router-id 8.8.8.8

network 10.10.10.48 0.0.0.3 area 0

network 10.10.10.52 0.0.0.3 area 0

network 192.168.11.128 0.0.0.63 area 0

network 192.168.11.192 0.0.0.63 area 0

network 192.168.12.0 0.0.0.63 area 0

network 192.168.12.64 0.0.0.63 area 0

network 192.168.12.128 0.0.0.63 area 0

network 192.168.12.192 0.0.0.63 area 0

do wr



**STEP 6: CONFIGURE STATIC ADDRESSES IN SERVER ROOM DEVICES**



**.193-default gateway**

.196

.197

.198



**STEP 7: DHCP SERVER DEVICE CONFIGURATIONS**



Open DHCP server

Click service on

Give pool name

Fill the default gateway. Each pool has its own default gateway

Fill starting IP Address

Fill subnet mask

Fill the maximum number users depending on the range of network addresses in your departments(vlans)

Then click add.

Repeat in each and every department







**STEP 8: INTER-VLAN ROUTING ON L3 SWITCHES AND IP-HELPER**



vlan 70

vlan 80

vlan 90

vlan 100

vlan 110

vlan 120

exit



int vlan 70

no shutdown

ip add 192.168.11.129 255.255.255.192

ip helper-address 192.168.12.196

exit



int vlan 80

no shutdown

ip add 192.168.11.193 255.255.255.192

ip helper-address 192.168.12.196

ex



int vlan 90

no shutdown

ip add 192.168.12.1 255.255.255.192

ip helper-address 192.168.12.196

exit



int vlan 100

no shutdown

ip add 192.168.12.65 255.255.255.192

ip helper-address 192.168.12.196

exit



int vlan 110

no shutdown

ip add 192.168.12.129 255.255.255.192

ip helper-address 192.168.12.196

exit



int vlan 120

no shutdown

ip add 192.168.12.193 255.255.255.192

exit

do wr



Step 1: Configure the DHCP Pool with the DNS IP

1\. Open your DHCP Server configuration.

2\. Select your IP pool and locate the DNS Server field.

3\. Enter the IP address of your DNS server into this field.

4\. Save or update the pool settings. (Repeat this step for any other active IP pools)



Step 2: Configure the DNS Server and Domain Name

1\. Navigate to the DNS service settings on your server.

2\. Turn on the DNS service by switching its status to On.

3\. Create a new DNS record:

&#x09;• Name: Enter a domain of your choice (e.g., www.makupe.com).

&#x09;• Address: Enter the IP address of the target web server.

4\. Save or add the record



Step 3: Refresh Network Settings on the PCs

1\. Go to any client PC connected to the network.

2\. Open its IP Configuration settings.

3\. Click on DHCP to request a new IP address configuration.

4\. Verify that the DNS Server field now automatically populates with the IP address you configured in Step 1.



Step 4: Test the Setup in the Web Browser

1\. Open the Web Browser on the client PC.

2\. Type your chosen domain name (e.g., www.makupe.com) into the URL address bar and hit Enter.

3\. The browser should successfully resolve the address and load the website's welcome page.



**STEP 9: WIRELESS CONFIGURATIONS**



I have attached a video showing how wireless configurations are done

