# Robotics Examples For Deep Learn

Use these examples as patterns, not as facts to copy blindly. Always prefer the user's current
workspace, logs, and code over these examples.

## Example: VR Teleoperation Chain

```text
Quest controller pose/buttons
  -> pub_pose.py
  -> ROS topics: right_handle_pose, left_handle_pose, quest_buttons
  -> teleop_double_piper.py
  -> Pinocchio/CasADi IK
  -> /left_joint_states and /right_joint_states
  -> piper_start_ms_node.py
  -> Piper SDK JointCtrl(...)
  -> physical arm joints
```

Good explanation targets:

- This is not MoveIt if the code directly solves IK and publishes joint states.
- Separate sampling rate, IK/command rate, and driver feedback rate.
- Deadman buttons and home buttons are safety gates, not IK math.
- Joint command smoothing and jump rejection are safety/control layers.

## Example: Fixed-World Position Delta

Code pattern:

```python
world_delta_xyz = np.array(pose_data[:3]) - np.array(previous_pose[:3])
```

Teaching angle:

- `pose_data[:3]` is the current hand position in the pose publisher's world/reference frame.
- `previous_pose[:3]` is the previous hand position in the same frame.
- Subtracting them gives a displacement vector in that fixed frame.
- This differs from `inv(previous_pose) @ current_pose`, which expresses motion in the previous
  controller frame and can make translation direction rotate with the wrist.

Debugging prompts:

- Which axis changes when the user moves the controller forward?
- Does the logged raw delta stay stable when the user twists the wrist?
- If the raw delta is right but the arm direction is wrong, inspect axis map/sign first.

## Example: Joint5 Orientation Sign

Symptom:

- User pitches the VR wrist, but the physical wrist joint moves in the opposite intuitive direction.
- The arm may compensate with shoulder/elbow joints if orientation is weakly weighted or wrist motion
  is constrained.

Likely explanation layers:

1. Controller orientation delta becomes a rotation matrix.
2. The rotation matrix is converted to a rotation vector.
3. Axis order and sign parameters map VR axes to robot target orientation axes.
4. IK chooses joint angles that minimize position/orientation error plus regularization.
5. If joint5 is penalized or limited too strongly, IK may use joints 1/2/3 to compensate.

Good parameter categories:

- Axis/sign mapping: `ORIENTATION_AXIS_MAP`, `ORIENTATION_AXIS_SIGN`,
  `LEFT_ORIENTATION_AXIS_SIGN`, `RIGHT_ORIENTATION_AXIS_SIGN`.
- Orientation strength: `IK_ORIENTATION_WEIGHT`, `NEAR_BASE_ORIENTATION_WEIGHT`,
  `*_ORIENTATION_SCALE`.
- Joint preference: `IK_REGULARIZATION_WEIGHT`, `IK_REGULARIZATION_WEIGHTS`,
  `JOINT5_SOFT_ABS_LIMIT_DEG`.
- Safety and smoothness: `MAX_JOINT_STEP_DEG`, `COMMAND_HZ`, `CONTROL_SPEED`.

Safe experiment pattern:

```bash
CONTROL_SPEED=8 MAX_JOINT_STEP_DEG=2 COMMAND_HZ=10 JOINT_COMMAND_HZ=10 \
DEBUG_POSE=true LOG_JOINT_COMMANDS=true ./start_slow_double.sh
```

Explain that this is a low-speed diagnostic configuration, not necessarily the final operating
configuration.

## Example: What Makes A Good Robotics Deep-Learn Note

It should answer all of these:

- What exactly entered the system?
- Which process transformed it?
- Which coordinate frame and unit was each value in?
- Which frequency controlled that stage?
- Which safety gate could block motion?
- Which parameters change direction, scale, latency, smoothness, or solver preference?
- How can the user verify the claim without moving hardware?
- What is the smallest safe hardware test?
