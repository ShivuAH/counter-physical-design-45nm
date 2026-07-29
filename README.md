# Counter Physical Design (45nm PDK)

This repository contains the physical design implementation of a 4-bit Up/Down counter designed using the 45nm technology node (Nangate / Generic 45nm PDK) with Cadence Innovus / Genus EDA tools.

## Project Structure

```
├── inputs/
│   ├── counter_netlist.v    # Synthesized Verilog netlist (Module: up_dn)
│   ├── counter_sdc.sdc      # Synopsys Design Constraints (Clock: 10ns / 100MHz)
│   ├── Default.globals      # Cadence Innovus global configuration file
│   └── Default.view         # Analysis view configuration
├── scripts/
│   ├── floorplan_new.tcl    # Floorplanning, IO pin placement, well-tap & endcap placement
│   ├── power_plan.tcl       # Power ring, stripes, and PG mesh synthesis (VDD/VSS)
│   ├── placement.tcl        # Standard cell placement and optimization
│   ├── cts.tcl              # Clock Tree Synthesis (CTS) and clock tree optimization
│   ├── route.tcl            # NanoRoute detail routing and DRC resolution
│   └── master_flow.tcl      # Top-level master TCL execution script
├── reports/                 # Output DRC, pin assignment, and netlist verification reports
└── images/                  # Layout screenshots, floorplans, and clock tree topology
```

## Physical Design Workflow

1. **Design Import & Setup (`Default.globals`)**
   - Import synthesized netlist, LEF standard cell libraries, technology files, and SDC constraints.
2. **Floorplanning & Cell Placement (`floorplan_new.tcl`)**
   - Define core boundaries, aspect ratio, core-to-IO margins.
   - IO Pin placement on Metal 5 layers and track alignment.
   - Insertion of physical-only cells (Endcaps and Well-tap cells).
3. **Power Planning (`power_plan.tcl`)**
   - Construct VDD and VSS power rings and power grid mesh.
   - Power grid connectivity verification (`verify_PG_short`, `verify_drc`, `verify_connectivity`).
4. **Standard Cell Placement (`placement.tcl`)**
   - Execute congestion-driven placement (`place_design`).
5. **Clock Tree Synthesis (`cts.tcl`)**
   - Synthesize clock tree network, buffer insertion, and skew optimization.
6. **Detailed Routing & DRC (`route.tcl`)**
   - NanoRoute global and detail routing.
   - Final DRC verification and signoff checks.

## Timing Constraints Summary

- **Clock Period**: 10.0 ns (100 MHz)
- **Clock Uncertainty**: 100 ps (Setup / Hold)
- **Input / Output Delay**: 2.0 ns
- **Target Cell Library**: 45nm Low Voltage Threshold (LVT) Standard Cell Library

## Tool Requirements

- Cadence Genus™ Synthesis Solution
- Cadence Innovus™ Implementation System
