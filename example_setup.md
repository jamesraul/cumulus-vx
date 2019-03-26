# leaf01
    net add interface swp1
    net add vlan 11 ip address 192.168.1.1/24
    net add interface swp1 bridge access 11
    net add interface swp51
    net add interface swp52
    net add bgp autonomous-system 65001
    net add bgp neighbor swp51 interface remote-as external
    net add bgp neighbor swp52 interface remote-as external
    net add bgp network 192.168.1.0/24
    net add bgp ipv4 unicast maximum-paths 4
    net pending
    net commit

# leaf02
    net add interface swp1
    net add vlan 12 ip address 192.168.2.1/24
    net add interface swp1 bridge access 12
    net add interface swp51
    net add interface swp52
    net add bgp autonomous-system 65002
    net add bgp neighbor swp51 interface remote-as external
    net add bgp neighbor swp52 interface remote-as external
    net add bgp network 192.168.2.0/24
    net add bgp ipv4 unicast maximum-paths 4
    net pending
    net commit

# server01
    sudo su -
    echo "auto lo
    iface lo inet loopback
    
    auto eth0
    iface eth0 inet dhcp
    
    auto vagrant
    iface vagrant inet dhcp
    
    auto eth1
    iface eth1 inet static
        address 192.168.1.11
        network 192.168.1.0
        netmask 255.255.255.0
        broadcast 192.168.1.255
        up route add -net 192.168.0.0 netmask 255.255.0.0 gw 192.168.1.1
    "  > /etc/network/interfaces
    systemctl restart networking


# server02
    sudo su -
    echo "auto lo
    iface lo inet loopback
    
    auto eth0
    iface eth0 inet dhcp
    
    auto vagrant
    iface vagrant inet dhcp
    
    auto eth1
    iface eth1 inet static
        address 192.168.2.12
        network 192.168.2.0
        netmask 255.255.255.0
        broadcast 192.168.2.255
        up route add -net 192.168.0.0 netmask 255.255.0.0 gw 192.168.2.1
    "  > /etc/network/interfaces
    systemctl restart networking

