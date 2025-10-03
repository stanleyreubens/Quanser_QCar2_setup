# Quanser Setup and Test Instructions

Before starting, ensure your **QCar is powered on** and you can **ping it from the host machine** to verify connectivity.  

---

## Step 1 – Initial Setup
1. **Connect to QCar with WinSCP** using its IP address.  
   - First, verify you can ping the QCar from the host machine.  

2. **Configure PuTTY for X11 Forwarding** on the host machine:  
   - Open PuTTY → expand **Connection → SSH → X11**.  
   - Check **Enable X11 Forwarding**.  
   - Set **X display location** to:  
     ```
     localhost:0.0
     ```
   - Open the session and keep PuTTY running.  

3. **Confirm Bash Setup** on the QCar:  
   - Press `Ctrl + Alt + H` to show hidden files.  
   - Open `.bashrc` and confirm the Python path is set correctly.  

---

## Step 2 – Organize Library Files
**On the QCar (right machine):**
- Go to `Documents/Quanser/`.  
- Delete everything **except** the `libraries` folder.  
- Inside `libraries/python`, delete all files.  

**On the Host (left machine):**
- Navigate to `Documents/Quanser/0_libraries/python`.  
- Copy all contents into the QCar’s `Documents/Quanser/libraries/python`.  

---

## Step 3 – Transfer Resource Files
**On the QCar:**
- Go to `Documents/Quanser/libraries/resources`.  
- Delete all files.  

**On the Host:**
- Navigate to `Documents/Quanser/libraries/resources`.  
- Copy all contents into the QCar’s `Documents/Quanser/libraries/resources`.  

---

## Step 4 – Transfer Research Hardware Files
**On the Host:**
- Navigate to `Documents/Quanser/5_research/sdcs/qcar2/hardware`.  
- Copy the folders `application` and `hardware_test` into the QCar’s `Documents/Quanser/`.  

---

## Step 5 – Transfer Teaching Skill Activities
**On the Host:**
- Navigate to `Documents/Quanser/6_teaching/4_Autonomous_Systems/SDCS/skill_activities`.  
- Copy the entire `skill_activities` folder into the QCar’s `Documents/Quanser/`.  

---

## Step 6 – Hardware Test Setup
1. Open **PuTTY** and connect to the QCar using its IP address.  
   - Ensure **X11 forwarding is enabled**.  
   - Set display to `localhost:0.0`.  

2. Navigate to:
   ```bash
   Documents/Quanser/hardware_tests
   ```

   > ⚠️ Place the QCar on the floor, not on a table, before running tests.  

3. Run:
   ```bash
   python QCar2_hardware_test_basic_io.py
   ```

---

## Step 7 – Intel RealSense & LiDAR Tests
From `Documents/Quanser/hardware_tests` in PuTTY, run the following as needed:

- **Intel RealSense IR Scopes**
  ```bash
  python QCar2_hardware_test_intelrealsense_IR.py
  ```

- **Intel RealSense Depth Measurement**
  ```bash
  python QCar2_hardware_test_intelrealsense.py
  ```

- **RP LiDAR A2 Mapping**
  ```bash
  python QCar2_hardware_test_rp_lidar_a2.py
  ```

---

## Step 8 – CSI Camera Setup
CSI cameras do not work with X11 forwarding.  

1. **On the Host Machine (Observer):**
   - Open:
     ```bash
     Documents/Quanser/5_research/sdcs/qcar2/hardware/hardware_test
     ```
   - Run:
     ```bash
     python QCar2_hardware_test_csi_cameras_observer.py
     ```

2. **Update Probe IP Address:**
   - In WinSCP, edit:
     ```bash
     Documents/Quanser/hardware_tests/QCar2_hardware_test_csi_cameras_probe.py
     ```
   - Change the IP address to the host machine’s IP.  

3. **On the QCar (Probe):**
   - Navigate to:
     ```bash
     Documents/Quanser/hardware_tests
     ```
   - Run:
     ```bash
     python QCar2_hardware_test_csi_cameras_probe.py
     ```

   > Ensure the observer script is running on the host machine. You should now see CSI camera output.  

---

## Step 9 – Self-Driving Test
**On the Host Machine:**
1. Navigate to:
   ```bash
   Documents/Quanser/6_teaching/4_Autonomous_Systems/SDCS/skill_activities/04_vehicle_control
   ```

2. Open `vehicle_control.py` and configure:
   ```python
   tf = 60
   V_ref = 0.5  # vehicle speed
   nodeSequence = [0, 4, 0]
   ```
   - Comment out the second `calibrationPose` line.  
   - Uncomment the first `calibrationPose` line.  
   - Save the file.  

3. Transfer the file to:
   ```bash
   Documents/Quanser/skill_activities/04_vehicle_control
   ```
   on the QCar.  

**On the QCar (via PuTTY with X11 enabled):**
- Navigate to:
  ```bash
  Documents/Quanser/skill_activities/04_vehicle_control
  ```
- Run:
  ```bash
  python vehicle_control.py
  ```

---

✅ Your QCar is now set up and ready for testing.  


---

## Step 10 – Manual Drive Test
1. Ensure the **USB dongle** is connected to the QCar.  
2. Open **PuTTY** and navigate to:
   ```bash
   Documents/Quanser/applications/manual_drive
   ```
3. Run:
   ```bash
   python manual_drive.py
   ```
