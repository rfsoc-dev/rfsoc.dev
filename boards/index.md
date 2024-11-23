---
title: Boards
permalink: /boards
layout: default
nav_order: 3
has_children: true
---

# Boards
{: .no_toc }

---
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}
---

## Setting up PYNQ in RFSoC FPGA

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
    }
}
```

[^for-vscode-ssh-config]: Reference: [this discussion on PYNQ forum](https://discuss.pynq.io/t/microsofts-vs-code-for-c-c-python-development-on-xilinx-platforms/2031#example-1-vitis-ai-c-debug-4)
[^vscode-github-copilot-fix]: Reference: [this discussion on GitHub](https://github.com/orgs/community/discussions/50328#discussioncomment-8238634)
