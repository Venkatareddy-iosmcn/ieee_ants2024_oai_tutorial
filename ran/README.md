# Procedure to install and run OAI basestation (gNB) and the user equipment (nrUE)

clone the ran repository
```bash
git clone https://gitlab.eurecom.fr/oai/openairinterface5g.git
```
compile the gNB and nrUE

```bash
cd openairinterface5g/
source oaienv
cd cmake_targets/
./build -I  
./build_oai -w SIMU --gNB --nrUE --ninja
```

Run the gNB

```bash
cd openairinterface5g/cmake_targets/ran_build/build
sudo -E ./nr-softmodem --rfsim --sa -O ~/ANTS_O-RAN_OAI_TUTORIAL/ran/conf/gnb.sa.band78.106prb.rfsim.conf
```


Run the UE  from a second terminal:

```bash
cd ~/openairinterface5g/cmake_targets/ran_build/build
sudo -E ./nr-uesoftmodem -r 106 --numerology 1 --band 78 -C 3619200000 --rfsim --sa -O ~/ANTS_O-RAN_OAI_TUTORIAL/ran/conf/ue.conf
```

Verify that it is connected: you should see the following output at gNB:

```
[NR_RRC]   UE 1: Receive RRC Reconfiguration Complete message (xid 3)
[NR_RRC]   msg index 0, pdu_sessions index 0, status 2, xid 3): nb_of_pdusessions 1,  pdusession_id 10, teid: 2466254620
 [NR_RRC]   NGAP_PDUSESSION_SETUP_RESP: sending the message
```

and nrUE:

```
[NAS]   [UE 0] Received NAS_CONN_ESTABLI_CNF: errCode 1, length 99
[LIBCONFIG] nas.noS1: 3/3 parameters successfully set, (3 to default value)
[OIP]   Interface oaitun_ue1 successfully configured, ip address 10.0.0.2, mask 255.255.255.0 broadcast address 10.0.0.255
```

Correspondingly, an interface should have been brought up:
```
113: oaitun_ue1: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 500
    link/none
    inet 10.0.0.2/24 brd 10.0.0.255 scope global oaitun_ue1
       valid_lft forever preferred_lft forever
    inet6 fe80::b732:d985:ef8b:4f9f/64 scope link stable-privacy
       valid_lft forever preferred_lft forever
```

Some other things to check:
- You see the RA procedure of the UE in the gNB logs

---

# Inject traffic


- Check the UE's IP address: interface `oaitun_ue1` using `ip address`
- The IP address `192.168.70.135` is the IP address of the `oai-ext-dn` container.
- Ping:
```
ping -I oaitun_ue1 192.168.70.135 # from host, "UL", to oai-ext-dn
docker exec -it oai-ext-dn ping <UE IP address>              # from container, "DL"
```
- Iperf3 testing between `oai-ext-dn` (in Docker) and the UE (running locally)
```
docker exec -it oai-ext-dn bash
iperf3 -s
```
- on the host in new terminal, run iperf3 client and bind the UE IP address:
```
iperf3 -B <UE IP ADDRESS> -c 192.168.70.135 -u -b 50M -R # DL
iperf3 -B <UE IP ADDRESS> -c 192.168.70.135 -u -b 20M    # UL
