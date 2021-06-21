# This just Git-essentials
# Just trying the ultimate time to embrace my enthousiasm of IT!

## Deployment notes 
crypto isakmp policy 1
 encryption aes
 authentication pre-share
 group 14
!
! A dynamic ISAKMP key and IPsec profile
crypto isakmp key supersecretkey address 0.0.0.0 crypto ipsec transform-set trans2 esp-aes esp-sha-hmac mode transport
!

## Staging notes 
crypto ipsec profile my_hub_vpn_profile
 set transform-set trans2
!
! The tunnel interface with NHRP Interface Tunnel0
 ip address 10.0.0.1 255.255.255.0
 ip nhrp authentication anothersupersecretkey
 ip nhrp map multicast dynamic
 ip nhrp network-id 99
 ip nhrp holdtime 300
 tunnel source GigabitEthernet0/0
 tunnel mode gre multipoint
! This line must match on all nodes that want to use this mGRE tunnel.
 tunnel key 100000
 tunnel protection ipsec profile my_hub_vpn_profile

## Usage notes
interface GigabitEthernet0/0
 ip address 172.16.0.1 255.255.255.0
!
interface GigabitEthernet0/1
 ip address 192.168.0.1 255.255.255.0
!
router eigrp 1
 network 10.0.0.0 0.0.0.255
 network 192.168.0.0 0.0.0.255

