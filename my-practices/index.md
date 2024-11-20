---
title: My Practices
permalink: /my-practices
layout: default
nav_order: 5
---

# My Practices

## General
- Ba patient. Debugging RFSoC designs is not easy.

## Verilog
- Write good finite state machines (FSM) for the custom IP.

## Vivado Block Design
- Note that overwriting a net of an interface will remove the connection to the corresponding interface net. Therefore, another manual connection is needed. This is especially important when we want to probe some signals of an interface using ILAs.
- Write standard AXI/AXIS modules for the custom IP. This will make it easier to integrate your IP into the Vivado block design. Otherwise there can be some unexpected issues. Take special care of the `tready` signal. For instance, the buffering of a signal is not straightforward. It is easy just to use the `axi_register` or `axis_register` module from [AXI Utilities](https://github.com/alexforencich/verilog-axi) & [AXIS Utilities](https://github.com/alexforencich/verilog-axis) for Verilog.
- All AXI/AXIS modules should have a register stage (preferably have a registered output). Therefore there will be no mismatched clocks which have to be manually handled every time we regenerate the IP.

## Testing
### Integrated Logic Analyzer (ILA)
