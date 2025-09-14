# **Introduction**  
This repository provides MATLAB-based code for the center-out task, supporting both unimanual (single-hand) and bimanual (two-hand) paradigms.The task was designed for rhesus monkeys using joysticks to control on-screen cursors and reach targets.

## **requirements**  
1.Use based Joysticks   
2.two computers with Matlab（MATLAB R2022a or later）  
3.NI 6009（external DAQ hardware for TTL signal recording）  
4.Ethernet cable or LAN connection for TCP communication

## **To run this code**  
On the left and right computers, run bimanual_L4.m and bimanual_R4.m respectively.  
Ensure TCP connection is established (default server IP: 192.168.0.10).

### **parameters**  
centerHoldDuration: required center-hold duration
targetHoldDuration: required target-hold duration
firstMoveThreshold: movement onset threshold
timeout: maximum trial duration
circleDiameter / radii: target size and distance


### **outputs**  
Event log (CSV/Mat format)trial index, success/failure  
timestamps for centerEnter/Exit, firstMove, hoverEnter, targetHold, trialEnd, etc.    
Cursor trajectories (mousePath, x/y vs. time)  
TTL signals (for alignment with neural recordings)
