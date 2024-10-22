Installing wireshark

:red-exclamation-mark: Make sure to select `yes` when the Wireshark installation asks you whether non-superusers should be able to capture packets.
Otherwise, you will have to run in sudo mode.

```bash
sudo add-apt-repository ppa:wireshark-dev/stable
sudo apt update
sudo apt install -y git net-tools wireshark
```

Installing docker

```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable"
sudo apt update
sudo apt install -y docker docker-ce
```

Add your username to the docker group, otherwise you will have to run in sudo mode. 
```bash
sudo usermod -a -G docker $(whoami)
```

Now, close the terminal tab and re-open it.
