#桥接  
1. 只需要设置虚拟机/etc/sysconfig/network-scripts/ifcfg-ens33,设置子网掩码、DNS1、IP、网关。  
    * IP：和主机在同一个网段下
    * 子网掩码：和主机一致
    * 网关：和主机一致
    * DNS：和主机一致  
**注意：**包括DNS在内的所有需要的信息都可以在WLAN下查看。双击WLAN查看详细信息即可。
2. 测试
    * 虚拟机ping主机（通）
    * 虚拟机ping网关（通）
    * 虚拟机ping百度（通）
    * 主机ping虚拟机（通）
    *主机ping网关（通）

#NAT连接
需要配置三个地方：  
1. VMware Network Adapter VMnet8:子网掩码和宿主机一致，ip随意设置，与宿主机同子网下即可。    
2.  NAT：类似网关，需要设置和宿主机不同的网关地址。但是虚拟机可以到达，主机却无法到达，所以跟普通网关又不一样。  
3.  ifcfg-ens33：设置IP（不设置的话，会使用DHCP服务器动态分配）、DNS1、网关（和nat相同，不设置的话只能访问NAT，无法访问外网，表明自己属于哪个网关）、子网掩码。  
**注意：**相当于虚拟机是NAT网关下的一部主机，而宿主机是另外一个网关下的一部主机。试图从宿主机ping虚拟机的时候，宿主机会先访问虚拟网卡（VMware Network Adapter VMnet8），但是无法访问虚拟机成功。  
**思考**  （主机ip：10.5.181.17；主机网关：10.5.181.3；NAT网关ip：192。168.1.3；虚拟机ip：192.168.1.88，VMware Network Adapter VMnet8 ip:192.168.1.6）  
1. 主机ping VMware Network Adapter VMnet8（通）  
2. 主机ping NAT（不通）   
3. 主机ping虚拟机（通）    
4.虚拟机ping主机（通）  
5. 虚拟机ping主机所在的网关（通）  
6.虚拟机ping NAT网关（通）  
7.虚拟机ping VMware Network Adapter VMnet8（不通）










