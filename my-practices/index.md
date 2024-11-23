---
title: My Practices
permalink: /my-practices
layout: default
nav_order: 5
---

# My Practices
{: .no_toc }

---
## Table of Contents
{: .no_toc .text-delta }
1. TOC
{:toc}
---

## General
- Ba patient. Debugging RFSoC designs is not easy.

## Verilog
- Write good finite state machines (FSM) for the custom IP.

## Vivado Block Design
- Note that overwriting a net of an interface will remove the connection to the corresponding interface net. Therefore, another manual connection is needed. This is especially important when we want to probe some signals of an interface using ILAs.
- Write standard AXI/AXIS modules for the custom IP. This will make it easier to integrate your IP into the Vivado block design. Otherwise there can be some unexpected issues. Take special care of the `tready` signal. For instance, the buffering of a signal is not straightforward. It is easy just to use the `axi_register` or `axis_register` module from [AXI Utilities](https://github.com/alexforencich/verilog-axi) & [AXIS Utilities](https://github.com/alexforencich/verilog-axis) for Verilog.
- All AXI/AXIS modules should have a register stage (preferably have a registered output). Therefore there will be no mismatched clocks which have to be manually handled every time we regenerate the IP.
- Use TCL scripts can save a lot of time. One small example is to use the script to copy the generated `.bit`, `.hwh` and `.ltx` file:
```tcl
cd [get_property DIRECTORY [current_project]]
file copy -force <proj>.runs/impl_1/<proj>_wrapper.bit <proj>.bit
file copy -force <proj>.gen/sources_1/bd/<proj>/hw_handoff/<proj>.hwh <proj>.hwh
file copy -force <proj>.runs/impl_1/<proj>_wrapper.ltx <proj>.ltx
```

## Testing
- I usually use LED lights as a bitstream version indicator, so I change the LED light pattern for each version of the bitstream. Therefore I can easily tell whether the new bitstream has been programmed successfully.

### Integrated Logic Analyzer (ILA)
