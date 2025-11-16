# **Center-Out Reaching Task (Unimanual + Bimanual)**

MATLAB-based framework for running **unimanual (single-hand)** and **bimanual (two-hand)** center-out reaching tasks.
Originally designed for **rhesus monkeys** using joysticks to control on-screen cursors and reach peripheral targets.

Compatible with neural recording setups (e.g., Neuropixels) using high-precision TTL signals for alignment.

---

## **Requirements**

### **Hardware**

* USB-based joysticks
* **Two computers** running MATLAB R2022a or later
* **NI USB-6009** (or similar) for TTL signal output
* LAN / Ethernet connection for TCP communication

### **Software**

* MATLAB R2022a+
* Instrument Control Toolbox
* Data Acquisition Toolbox

---

## **How to Run**

1. On the **left computer**, run:

   ```matlab
   bimanual_L
   ```

2. On the **right computer**, run:

   ```matlab
   bimanual_R
   ```

3. Ensure both computers can communicate through TCP

   * Default server IP: `192.168.0.10`
   * Default port: `30000`

---

## **Parameters**

Key task parameters include:

| Parameter                  | Description                                   |
| -------------------------- | --------------------------------------------- |
| **centerHoldDuration**     | Required center-hold duration before movement |
| **targetHoldDuration**     | Required hold time inside target              |
| **firstMoveThreshold**     | Movement onset threshold                      |
| **timeout**                | Maximum allowed trial duration                |
| **circleDiameter / radii** | Target size and target distance               |

---

## **Outputs**

### **1. Event Logs**

Saved per trial (CSV or MAT format):

* Trial index
* Trial mode (uni-L / uni-R / bi)
* Success / failure
* Time of:

  * `centerEnter`
  * `centerExit`
  * `firstMove`
  * `hoverEnter`
  * `targetHold`
  * `trialEnd`

### **2. Cursor Trajectories**

Each trial saves a full trace:

```
[x, y, time]
```

Useful for:

* Movement kinematics
* Latency computation
* Velocity / acceleration extraction

### **3. TTL Signals**

For neural alignment (NI-6009):

* First movement onset
* Target acquisition
* Trial start/end
* Success / fail markers

---

## **Notes & Limitations**

### **Pointer precision**

For stable joystick-to-cursor mapping, disable in Windows:

* **Enhance pointer precision**
* **Pointer acceleration**

This ensures reproducible kinematic behavior.

---

### **Potential Issues**

#### **1. Incomplete coordinate recording**

Due to event handling such as:

* Trial resets
* Black-screen synchronization
* Premature aborts
* TCP delays

Some trials may have:

* Missing samples
* Shortened trajectories
* Misaligned time vectors

**Recommendation:**
Always cross-check:

* Event logs
* TTL time stamps

to ensure data integrity.

---

#### **2. Trial duration mismatch (network latency)**

Because the two computers run their own clocks:

* One machine may log slightly longer trial durations
* Differences come from TCP transmission delay

**Recommendation:**
During analysis:

* Align trials by the **shorter duration**
* Trim cursor trajectories accordingly

---

## **License**

MIT License

