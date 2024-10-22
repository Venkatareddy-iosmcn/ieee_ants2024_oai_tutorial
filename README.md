# TUT2: Innovation and Prototyping in O-RAN using Open-Source Testbeds

Welcome to our IEEE ANTS 2024 tutorial! In this page you will find all the information that is needed to participate in the OpenAirInterface (OAI) hands-on session.
The participants should carefully follow the below instructions and set up their environment before coming to the hands-on session.

## 1. Minimum Computing Requirements
To run an end-to-end 5G network with OAI Core Network (CN),
Radio Access Network (RAN) including base station (gNB) and user equipment (nrUE) in RFsim mode, we should have the following minimum recommended computing requirements: 
-  Operating System: Ubuntu 22.04 LTS
-  CPU: 8 virtual cores x86_64 @ 3.5 GHz
- RAM: 16 GB
  
Participants can use their own laptop having these requirments or can use a Virtual Machine (VM) in a cloud platform.
For VM setup, we recomend using the Google Computing Platform (GCP).
In either case, all users must bring a laptop that has access to internet.

## 1. Environment Setup

Follow these instrunctions in a sequnetial order.

1. To setup a VM in the GCP, follow the instructions provided in the  vmsetup/Setup_VM_GCP.md  file.
2. Install the required softwares using the file utils utils/Util_Installation.md in your VM.
3. Install the OAI CN by following the instructions provided in cn/CN_Installation.md
4. Finally, install the RAN using the instructions provided in ran/RAN_Installation.md


