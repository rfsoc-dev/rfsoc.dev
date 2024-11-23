---
title: RF Analyzer
permalink: /rf-analyzer
layout: default
nav_order: 4
---

# RF Analyzer
{: .no_toc }

---
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}
---

## Using AMD RF Analyzer
### Installation
Download the AMD RF Analyzer from [here](https://www.amd.com/en/products/adaptive-socs-and-fpgas/soc/zynq-ultrascale-plus-rfsoc.html#tabs-9c5228a5dd-item-c560eacfb2-tab). It supports Windows only.

### Troubleshooting on Windows 11
The GUI will not open on Windows 11.
This problem is due to the new Terminal introduced in Windows 11.
Therefore, we need to change the Terminal to the legacy one.

Run **Command Prompt** as Administrator:

![RF Analyzer Windows 11 Patch Procedure 1](/images/rf-analyzer-win11-patch-cmd-1.png)

Right click on the header and select **Properties**:

![RF Analyzer Windows 11 Patch Procedure 2](/images/rf-analyzer-win11-patch-cmd-2.png)

Check **Use legacy console**:

![RF Analyzer Windows 11 Patch Procedure 3](/images/rf-analyzer-win11-patch-cmd-3.png)

Restart the RF Analyzer and it should work now.

> AMD provides [an alternative solution](https://adaptivesupport.amd.com/s/article/000036565?language=en_US) but this has not been tested by the author.

## Using PYNQ RF Analyzer
Import [`xrfdc`](https://github.com/Xilinx/PYNQ/tree/93ddd21ab623883590a8c8b07f0b157b2855da4b/sdbuild/packages/xrfdc) to access RF data converter information:

```python
import xrfdc
```

Now the RF data converter IP has the `.IPStatus` attribute.
For example:

```python
print(ol.rfdc.IPStatus)
```

