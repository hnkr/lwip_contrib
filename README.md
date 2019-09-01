# Running LwIP TCP/IP Stack on Ubuntu
- To develop 'target' application on host 

## Requirements
- Ubuntu OS (on account of using TAP interface)
- gcc

## Compile & Run
Get in lwip_contrib/contrib/ports/unix/minimal directory.
- Compile:
    -  make
- Run:
    - sudo ./echop

## Working Principle
When it starts running, it will create tap1 interface and then it will link the tap1 interface to LwIP TCP/IP Stack.<br />
Thanks to this 'link', the end user will have the chance to run network applications on the same machine but with different IP Addresses.

- According to your network settings, you need to change the IP Address / GW Address / Subnet mask of TCP/IP Stack by changing the parameters mentioned below (in main.c):<br />
  IP4_ADDR(&gw, 192,168,1,1);  <br />
  IP4_ADDR(&ipaddr, 192,168,1,20);  <br />
  IP4_ADDR(&netmask, 255,255,255,0);  <br />

## Testing

- You should see messages on stdout like the ones below, when it starts running successfully:<br />

    Host at 192.168.1.20 mask 255.255.255.0 gateway 192.168.1.1 <br />
    TCP/IP initialized. <br />
    SNMP private MIB start, detecting sensors. <br />
    Applications started. <br />

- When you type "ip link" command in the terminal you should see tap1 interface up as mentioned below (Your MAC Address instead of NO):<br />

    tap1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN mode DEFAULT group default qlen 1000<br />
    link/ether NO:NO:NO:NO:NO:NO brd ff:ff:ff:ff:ff:ff<br />


- Communication Test:
    - To test TCP communication type the command mentioned below and then you will see the messages twice due to 'echo' server:<br />
        nc -l 192.168.1.20(Your IP Address) 45678<br />
    - To test UDP communication type the command mentioned below and then you will see the messages twice due to 'echo' server:<br />
        nc -u -l 192.168.1.20(Your IP Address) 7<br />





