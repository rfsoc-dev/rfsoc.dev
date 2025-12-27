---
title: RFSoC-PYNQ
permalink: /rfsoc-pynq
layout: default
nav_order: 2
---

# RFSoC-PYNQ
{: .no_toc }

---
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}
---

## Setting up PYNQ in RFSoC FPGA

See the official [PYNQ documentation](https://www.rfsoc-pynq.io/) for detailed instructions and image download.

## Internet Access on PYNQ
Usually when connected using Ethernet, the PYNQ board will not have internet access.
However, for package installation including [`RFSoC-MTS`](https://github.com/Xilinx/RFSoC-MTS), internet access is required.

Here is a working method to enable internet access on PYNQ used by me.

{: .warning }
> Use at your own risk. Different systems and network environments may require different settings.

### Prerequisites
- A computer with internet access (Wi-Fi in this case) using Linux (tested on Ubuntu 20.04)
- Ethernet connection to the PYNQ board
- PYNQ board IP assumes to be `192.168.2.99`, the default for PYNQ boards

### Step 1: Configuration at Computer
Set the computer Ethernet IP to be in the same subnet as the PYNQ board.
We set the IPv4 to be the manual mode.
In this case, we also want it to be the gateway for the PYNQ board, so it is `192.168.2.1`.
The subnet mask is `255.255.255.0`, and the gateway is left blank.
IPv6 will be disabled.

Then, in a terminal, we setup the WiFi sharing.
```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

Use `ip link` or `ifconfig` to find the WiFi and Ethernet interface names.
Then run

```bash
# Define your interface names here
export WAN=wlan0   # Your WiFi interface (Internet source)
export LAN=eth0    # Your Ethernet interface (Connected to RFSoC)

# Enable Network Address Translation (Masquerading)
sudo iptables -t nat -A POSTROUTING -o $WAN -j MASQUERADE

# Allow traffic forwarding between interfaces
sudo iptables -A FORWARD -i $WAN -o $LAN -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i $LAN -o $WAN -j ACCEPT
```

### Step 2: Configuration at PYNQ Board

Configure the RFSoC gateway to the computer
```bash
sudo ip route add default via 192.168.2.1
```

Set DNS
```bash
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

Now it should work.

## Using VS Code for Jupyter Notebook

The following procedures are tested by the author on ZCU208 with PYNQ image v3.0.1.

### Setting up SSH

First connect to SSH `root@192.168.2.99` with password `xilinx`,
and then run the following command: [^for-vscode-ssh-config]

```bash
sudo chmod u+w /etc/ssh/sshd_config
sudo echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
sudo service sshd restart
```

In VS Code, connect to remote SSH:

Username
: `root@192.168.2.99`

Password
: `xilinx`

Install the required extensions as needed.
For Jupyter Notebook, select the kernel from existing kernels named `pynq-venv`.

### Using GitHub Copilot
GitHub Copilot may show the log-in failed error message.
Use the following settings in `.vscode/settings.json`: [^vscode-github-copilot-fix]

```json
{
    "remote.extensionKind": {
        "GitHub.copilot": [
            "ui",
        ],
        "GitHub.copilot-chat": [
            "ui",
        ],
    }
}
```

[^for-vscode-ssh-config]: Reference: [this discussion on PYNQ forum](https://discuss.pynq.io/t/microsofts-vs-code-for-c-c-python-development-on-xilinx-platforms/2031#example-1-vitis-ai-c-debug-4)
[^vscode-github-copilot-fix]: Reference: [this discussion on GitHub](https://github.com/orgs/community/discussions/50328#discussioncomment-8238634)
