# **Introduction**  
This repository provides MATLAB-based code for the center-out task, supporting both unimanual (single-hand) and bimanual (two-hand) paradigms.The task was designed for rhesus monkeys using joysticks to control on-screen cursors and reach targets.

## **Requirements**  
1.Use based Joysticks   
2.two computers with Matlab（MATLAB R2022a or later）  
3.NI 6009（external DAQ hardware for TTL signal recording）  
4.Ethernet cable or LAN connection for TCP communication

## **To run this code**  
On the left and right computers, run bimanual_L4.m and bimanual_R4.m respectively.  
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
### **Byte transmission limit:**    
Communication between client and server is based on byte packets (0–255). This means the maximum representable value per transmission is 255.  
This limitation comes from the TCP client’s use of fwrite with uint8 data type.  
To avoid overflow and loss of precision, signals are normalized before transmission and decoded back on the receiver side.
#### **Pointer precision:**      
in the OS settings, pointer acceleration must be disabled and pointer precision fixed. This ensures a stable and reproducible mapping between joystick deflection and cursor velocity.
