---
title: RFSoC4x2
permalink: /boards/rfsoc4x2
parent: Boards
layout: default
nav_order: 1
---

# RFSoC4x2

[Board Website](https://www.amd.com/en/corporate/university-program/aup-boards/rfsoc4x2.html)

## Board Files

RFSoC4x2 board files are not directly available in the Vivado repository.
They can be found in the GitHub link below:

[`RFSoC4x2-BSP/board_files` at master · RealDigitalOrg/RFSoC4x2-BSP](https://github.com/RealDigitalOrg/RFSoC4x2-BSP/tree/master/board_files)

Add the following lines to the `Vivado_init.tcl` file with

```tcl
set_param board.repoPaths [list "/path/to/board_files"]
```

Here the path has the directory `rfsoc4x2`.
