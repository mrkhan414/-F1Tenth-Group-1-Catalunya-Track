# -F1Tenth-Group-1-Catalunya-Track# F1Tenth Group 1 — Catalunya Track

## Project overview
This project uses a Follow-the-Gap (FTG) reactive obstacle-avoidance controller for an F1Tenth vehicle in the ROS 2 / F1Tenth Gym simulator. The controller reads LiDAR data and publishes Ackermann steering and speed commands.

## Challenge result
The submitted terminal log reports 10 consecutive clean laps.

| Metric | Result |
|---|---:|
| Completed laps | 10 / 10 |
| Fastest lap | 147.27 s |
| Average lap | 148.17 s |
| Slowest lap | 148.91 s |

See `lap_results.csv` for individual lap times.

**Evidence note:** These values are transcribed from the terminal output supplied for this submission. The program reported "without a detected collision"; this should not be described as independent proof of collision-free driving unless the simulator's collision detection and video evidence are also checked.

## Environment
- Ubuntu 22.04
- ROS 2 Humble
- Python 3
- Workspace: `~/F1Tenth-Repository`
- Track map: Catalunya

## ROS topics
- LiDAR input: `/scan`
- Ego drive output: `/drive`
- Ego odometry: `/ego_racecar/odom`
- Opponent drive input (when the simulator is configured for two agents): `/opp_drive`

## Build
```bash
cd ~/F1Tenth-Repository
source /opt/ros/humble/setup.bash
colcon build
source install/setup.bash
```

## Run
Start the simulator in Terminal 1:
```bash
source /opt/ros/humble/setup.bash
source ~/F1Tenth-Repository/install/setup.bash
ros2 launch f1tenth_gym_ros gym_bridge_launch.py
```

If the bridge is configured for two agents and waits for an opponent command, send a stationary opponent command once in Terminal 2:
```bash
source /opt/ros/humble/setup.bash
ros2 topic pub --once /opp_drive ackermann_msgs/msg/AckermannDriveStamped "{drive: {speed: 0.0, steering_angle: 0.0}}"
```

Run the controller in another terminal:
```bash
source /opt/ros/humble/setup.bash
source ~/F1Tenth-Repository/install/setup.bash
ros2 run controllers gap_node
```

Run the lap timer in a separate terminal (if the executable is registered in `setup.py`):
```bash
ros2 run controllers lap_timer_node
```
Alternatively, run the Python file directly:
```bash
python3 ~/F1Tenth-Repository/src/controllers/controllers/lap_timer_node.py
```

## Follow-the-Gap method# F1Tenth Group 1 — Catalunya Track

## Project overview
This project uses a Follow-the-Gap (FTG) reactive obstacle-avoidance controller for an F1Tenth vehicle in the ROS 2 / F1Tenth Gym simulator. The controller reads LiDAR data and publishes Ackermann steering and speed commands.

## Challenge result
The submitted terminal log reports 10 consecutive clean laps.

| Metric | Result |
|---|---:|
| Completed laps | 10 / 10 |
| Fastest lap | 147.27 s |
| Average lap | 148.17 s |
| Slowest lap | 148.91 s |

See `lap_results.csv` for individual lap times.

**Evidence note:** These values are transcribed from the terminal output supplied for this submission. The program reported "without a detected collision"; this should not be described as independent proof of collision-free driving unless the simulator's collision detection and video evidence are also checked.

## Environment
- Ubuntu 22.04
- ROS 2 Humble
- Python 3
- Workspace: `~/F1Tenth-Repository`
- Track map: Catalunya

## ROS topics
- LiDAR input: `/scan`
- Ego drive output: `/drive`
- Ego odometry: `/ego_racecar/odom`
- Opponent drive input (when the simulator is configured for two agents): `/opp_drive`

## Build
```bash
cd ~/F1Tenth-Repository
source /opt/ros/humble/setup.bash
colcon build
source install/setup.bash
```

## Run
Start the simulator in Terminal 1:
```bash
source /opt/ros/humble/setup.bash
source ~/F1Tenth-Repository/install/setup.bash
ros2 launch f1tenth_gym_ros gym_bridge_launch.py
```

If the bridge is configured for two agents and waits for an opponent command, send a stationary opponent command once in Terminal 2:
```bash
source /opt/ros/humble/setup.bash
ros2 topic pub --once /opp_drive ackermann_msgs/msg/AckermannDriveStamped "{drive: {speed: 0.0, steering_angle: 0.0}}"
```

Run the controller in another terminal:
```bash
source /opt/ros/humble/setup.bash
source ~/F1Tenth-Repository/install/setup.bash
ros2 run controllers gap_node
```

Run the lap timer in a separate terminal (if the executable is registered in `setup.py`):
```bash
ros2 run controllers lap_timer_node
```
Alternatively, run the Python file directly:
```bash
python3 ~/F1Tenth-Repository/src/controllers/controllers/lap_timer_node.py
```

## Follow-the-Gap method
1. Read the LiDAR scan.
2. Clean invalid and out-of-range readings.
3. Restrict the scan to the forward field of view.
4. Identify the closest obstacle and mask a safety bubble around it.
5. Find the largest remaining free-space gap.
6. Select a target point inside that gap.
7. Convert the target angle to steering and choose speed based on steering demand and obstacle distance.
8. Publish an Ackermann drive command.

## Files to include from the ROS workspace
Copy the actual working source files into the repository before submission:
- `src/controllers/controllers/gap_node.py`
- `src/controllers/controllers/lap_timer_node.py`
- `src/controllers/setup.py`
- `src/f1tenth_gym_ros/config/sim.yaml` (if modified for Catalunya)

Do not replace your tested source files with this documentation pack. The exact code currently running should be committed.

## Evidence checklist
- [ ] Screenshot of the simulator showing the Catalunya track and ego car.
- [ ] Screenshot of the terminal showing the final 10/10 result and fastest lap.
- [ ] Video showing the car driving the track and the terminal result.
- [ ] GitHub repository URL added to the report/submission form.
- [ ] Confirm the submitted source files match the code used for the recorded run.
1. Read the LiDAR scan.
2. Clean invalid and out-of-range readings.
3. Restrict the scan to the forward field of view.
4. Identify the closest obstacle and mask a safety bubble around it.
5. Find the largest remaining free-space gap.
6. Select a target point inside that gap.
7. Convert the target angle to steering and choose speed based on steering demand and obstacle distance.
8. Publish an Ackermann drive command.

## Files to include from the ROS workspace
Copy the actual working source files into the repository before submission:
- `src/controllers/controllers/gap_node.py`
- `src/controllers/controllers/lap_timer_node.py`
- `src/controllers/setup.py`
- `src/f1tenth_gym_ros/config/sim.yaml` (if modified for Catalunya)

Do not replace your tested source files with this documentation pack. The exact code currently running should be committed.

## Evidence checklist
- [ ] Screenshot of the simulator showing the Catalunya track and ego car.
- [ ] Screenshot of the terminal showing the final 10/10 result and fastest lap.
- [ ] Video showing the car driving the track and the terminal result.
- [ ] GitHub repository URL added to the report/submission form.
- [ ] Confirm the submitted source files match the code used for the recorded run.
