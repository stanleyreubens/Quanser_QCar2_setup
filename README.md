# Quanser Setup and Test Instructions

## Step 1 – Organize Library Files
**Use WinSCP to login to the QCar with the IpAddress. Make sure you ping it first on the host machine to ensure it's reachable:**

**On the right machine (QCar via IP address):**
- Go to `Documents/quanser/`
- Delete everything except the `libraries` folder.
- Inside `libraries/python`, delete all files.

**On the left machine (Host machine):**
- Navigate to `Documents/quanser/0_libraries/python`
- Copy everything inside the `python` folder to the right machine’s `Documents/quanser/libraries/python` folder.

---

## Step 2 – Transfer Resource Files
**On the right machine (QCar):**
- Go to `Documents/quanser/libraries/resources`
- Delete all files inside.

**On the left machine (Host):**
- Navigate to `Documents/quanser/libraries/resources`
- Copy all contents to the right machine’s `Documents/quanser/libraries/resources` folder.

---

## Step 3 – Transfer Research Hardware Files
**On the left machine (Host):**
- Navigate to `Documents/quanser/1_research/sdcs/qcar2/hardware`
- Copy the folders `application` and `hardware_test` into the right machine’s `Documents/quanser/` directory.

---

## Step 4 – Transfer Teaching Skill Activities
**On the left machine (Host):**
- Navigate to `Documents/quanser/6_teaching/4_Autonomous_Systems/SDCS/skill_activities`
- Copy the entire `skill_activities` folder into the right machine’s `Documents/quanser/` directory.

---

## Step 5 – Hardware Test Setup
1. Open **PuTTY** and connect to the QCar using its IP address.
   - Enable **X11 forwarding** (SSH → X11 → check "Enable X11 forwarding").
   - Set **X display location** to `local:0.0`.

2. In PuTTY, navigate to:
   ```bash
   Documents/quanser/hardware_tests
   ```

3. Run:
   ```bash
   python QCar2_hardware_test_basic_io.py
   ```

---

## Step 6 – CSI Camera Setup
- Open **another PuTTY session** (without X11 forwarding).
- Since CSI cameras don’t work with X11, run the observer script on the host PC.

**On the host machine:**
- Open this folder in VS Code:
  ```bash
  Documents/quanser/1_research/sdcs/qcar2/hardware/hardware_tests
  ```

- Run:
  ```bash
  python QCar2_hardware_test_csi_cameras_observer.py
  ```

---

## Step 7 – Update IP Address for CSI Camera Probe
**On the host machine:**
1. In WinSCP, open:
   ```bash
   Documents/quanser/hardware_tests
   ```
2. Double-click `QCar2_hardware_test_csi_cameras_probe.py`.
3. Change the IP address to your host machine’s IP, then save.

**On PuTTY:**
Run:
```bash
python QCar2_hardware_test_csi_cameras_probe.py
```

---

## Step 8 – Self-Driving Test
**On the host machine:**
1. Navigate to:
   ```bash
   Documents/quanser/6_teaching/4_Autonomous_Systems/SDCS/skill_activities/04_vehicle_control
   ```

2. Open `vehicle_control.py` in VS Code.
   - Set:
     ```python
     tf = 60
     V_ref = 0.5
     ```
   - Comment out the second `calibrationPose` line.
   - Uncomment the first `calibrationPose` line.
   - Save the file.

3. Transfer the modified file to:
   ```bash
   Documents/quanser/skill_activities/04_vehicle_control
   ```
   on the right machine (QCar).

**On PuTTY:**
Navigate to:
```bash
Documents/quanser/skill_activities/04_vehicle_control
```

Run:
```bash
python vehicle_control.py
```
