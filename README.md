# **Introduction**  
This repository provides MATLAB-based code for the center-out task, supporting both unimanual (single-hand) and bimanual (two-hand) paradigms.The task was designed for rhesus monkeys using joysticks to control on-screen cursors and reach targets.

## **Requirements**  
1.Usb based Joysticks   
2.two computers with Matlab（MATLAB R2022a or later）  
3.NI 6009（external DAQ hardware for TTL signal recording）  
4.Ethernet cable or LAN connection for TCP communication

## **To run this code**  
On the left and right computers, run bimanual_L6.m and bimanual_R6.m respectively.  
Ensure TCP connection is established (default server IP: 192.168.0.10).

### **Parameters**    
centerHoldDuration: required center-hold duration  
targetHoldDuration: required target-hold duration  
firstMoveThreshold: movement onset threshold  
timeout: maximum trial duration  
circleDiameter / radii: target size and distance


### **Outputs**  
Event log (CSV/Mat format)trial index, success/failure  
timestamps for centerEnter/Exit, firstMove, hoverEnter, targetHold, trialEnd, etc.    
Cursor trajectories (mousePath, x/y vs. time)  
TTL signals (for alignment with neural recordings)

## **Notes & Limitations**  
### **Pointer precision:**      
in the OS settings, pointer acceleration must be disabled and pointer precision fixed. This ensures a stable and reproducible mapping between joystick deflection and cursor velocity.
### **Potential Issues:**    
1.Incomplete coordinate recording:Due to various event-handling routines in the code (e.g., trial resets, barrier synchronization, or premature exits), cursor coordinates may occasionally be missing or misaligned. This requires careful post-processing to ensure data integrity.When TTL pulses are sent in parallel with TCP communication, timing mismatches can occur. Users should cross-check event logs and TTL markers to avoid misinterpretation of trial timing.  

2.Trial duration mismatch due to network latency:
Because of network transmission delays, one computer may log a trial end time a few milliseconds longer than the other. During data processing, it is recommended to align trials by the shorter duration and adjust the corresponding cursor coordinates accordingly.
