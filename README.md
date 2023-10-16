# UE Context Release and PDU Session Release

## UE Context Release or IDLE Process:

After successful installation of free5gc and Ueransim, To start IDLE condition follow below procedure:

1. ssh into free5gc in 3 individual terminals for.
*	Webconsole
*	To run free5gc
*	tcpdump

2. ssh into UERANSIM in 3 individual terminals for.
*	GNB
*	UE
* UE context release

3. ssh in free5gc and run web-console in one terminal.

Remember to do if the vm free5gc is restarted give
```
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
sudo systemctl stop ufw
sudo iptables -I FORWARD 1 -j ACCEPT
```
4. Run free5gc in another terminal.
```
cd ~/free5gc
./run.sh
```
5. ssh into free5gc in another terminal and give tcpdump
```
sudo tcpdump -i enp0s8 -w filename.pcap
```
6.  start UERANSIM in another terminal for GNB and give
```
cd ~/UERANSIM
build/nr-gnb -c config/free5gc-gnb.yaml
```
7. start UERANSIM in another terminal for UE and give
```
cd ~/UERANSIM
sudo build/nr-ue -c config/free5gc-ue.yaml  
```
8. start the UERANSIM in another terminal for UE Context Release and give
```
cd ~/UERANSIM
build/nr-cli UERANSIM-gnb-xxx-xx-1 -e "ue-release 1"
```
note: Use PLMN number (in the place of xxx-xx) that is reflected on web-console

Now stop the UE, GNB and tcpdump in order by using ctrl+c in the respective terminals. And now transfer the file from vm to your computer and check the generated packets in pcap file using wireshark.

## PDU Session Release Process:

After successful installation of free5gc and Ueransim, To start PDU Session Release condition follow below procedure:

1. ssh into free5gc in 3 individual terminals for.
*	Webconsole
*	To run free5gc
*	tcpdump

2. ssh into UERANSIM in 3 individual terminals for.
*	GNB
*	UE
* PUD Session Release

3. ssh in free5gc and run web-console in one terminal.

Remember to do if the vm free5gc is restarted give
```
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
sudo systemctl stop ufw
sudo iptables -I FORWARD 1 -j ACCEPT
```
4. Run free5gc in another terminal.
```
cd ~/free5gc
./run.sh
```
5. ssh into free5gc in another terminal and give tcpdump
```
sudo tcpdump -i enp0s8 -w filename.pcap
```
6.  start UERANSIM in another terminal for GNB and give
```
cd ~/UERANSIM
build/nr-gnb -c config/free5gc-gnb.yaml
```
7. start UERANSIM in another terminal for UE and give
```
cd ~/UERANSIM
sudo build/nr-ue -c config/free5gc-ue.yaml  
```
8. start the UERANSIM in another terminal for PUD Session Release and give
```
cd ~/UERANSIM
```
can be approached in two ways:
8.1
```
build/nr-cli imsi-(xxxxxxxxxxxxxxx) -e "ps-release 1"
```
  (or)
 
8.2
```
build/nr-cli imsi-(xxxxxxxxxxxxxxx)
```
note: imsi number is reflected on webconsole and the same to be used here

and give
```
commands
```
list of commands will appear give 
```
ps-release
```
and you will find

$ ps-release
Trigger a PDU session release procedure
Usage:
  ps-release <pdu-session-id>...

and give
```
ps-release 1
```
 
Now stop the UE, GNB and tcpdump in order by using ctrl+c in the respective terminals. And now transfer the file from vm to your computer and check the generated packets in pcap file using wireshark.

