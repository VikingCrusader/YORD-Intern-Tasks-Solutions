# Task 1 - Yiwen Zhang

## VR Safety Training Simulator: Test Plan

To test the whole system, I want to divide the test roughly into 8 parts:

### 1. Basic Functional Testing

To make sure the basic functions work well. This is a common test for all types of software.

For example:
- Login
  - Edge cases: null characters or SQL injection.
- Open main menu
- Get in the scene and exit
- Whether the task flow works correctly, whether the training can be completed normally

### 2. Motion Testing

These are some of the features that first-person perspective software or 3D games test, and they are very basic.

For example:
- Walk and Teleport
  - Can users move both forward and backward?
  - Is the motion smooth?
  - Edge cases: the behaviour of the user walking to the edge of the Guardian Boundary.
- Pick up or lay down a fire extinguisher
  - Is the user's grip position accurate?
- Rotate the view
  - Edge cases: when the viewpoint rotates rapidly, will the high latency cause dizziness?
- Squat down and stand up

### 3. VR-Specific Testing

The biggest difference between VR and regular apps is that they involve hardware and real space.

For example:
- Latency
  - Will the screen stutter when the player turns their head quickly? (Users will feel uncomfortable if the stutter is high.)
- Clip Through
  - When a user crouches down, lies down, picks up a fire extinguisher, and walks to the boundary, will the image clip through the barrier?
- Controller tracking loss
  - Test what will happen when controller tracking is lost, for example when the hand is out of the camera's field of view.
- Depth perception accuracy
  - Test for errors in object rendering depth, causing objects that appear close to the viewer to be out of reach.

### 4. Multiplayer and Network Testing

Because of Voice Chat, it's essential to test with multiple users and network conditions.

For example:
- Can two people enter the same room normally?
- Will a bad network connection cause synchronization issues?
- What if one person disconnects?
- What if two people are carrying the same fire extinguisher? Test synchronization.
- Will there be audio delay?

### 5. Comfort, Accessibility and User Experience Testing

Comfort and accessibility are the most important aspects of VR.

For example:
- Can beginners learn how to operate it quickly?
- Is the UI easy to see?
- Are the prompts clear enough?
- Does i18n work well? (Will there be any translation errors due to the wording of menus and prompts in different languages?)
- Emergency Exit and Panic Mechanism: ensures that players can access the system menu or safely exit at any time, regardless of their orientation or animation state.
- Accessible for disabled players: verify whether the seated gameplay mode is smooth and whether the core gameplay and item accessibility are affected.

### 6. Performance Testing

VR is demanding for high performance.

For example:
- Is the FPS stable? (E.g., is there a huge FPS drop after 1 hour of play? This even happens in some AAA games.)
- Will the memory leak?

### 7. Hardware and Environment Limit Testing

Unlike regular software, VR testing also requires monitoring hardware performance.

For example:
- Monitor device overheating and frequency reduction, battery level, and screen lag during prolonged operation (over 30 minutes), to prevent exacerbating dizziness.
- Performance of the camera in low-light or high-light environments.

### 8. Edge Cases

Some rare but extreme cases.

For example:
- A user is very tall/short — e.g., 1.20m (dwarfism) and 2.10m
- User keeps picking up and putting down items. Will it cause a crash?
- User sticks their head into the wall.
- User throws the fire extinguisher off the map. (Will it cause tunneling or clip through?)
- User removes the headset — will the process terminate?
- Controller runs out of battery.
- Low battery behaviours.
- Re-enters game after a long standby.

## Assumptions & Questions

Because I'm not very familiar with VR devices, I have a few questions regarding specific situations, which might affect the testing methods.

1. Is the voice chat global broadcast or proximity-based chat? This will affect the testing scope.
2. Is the fire extinguisher purely for display, or does it involve actual "fire extinguishing" interaction logic (such as spraying it at virtual flames)? This isn't clearly stated in the task description, and it will affect the depth of the interaction testing.

## Time Consuming

I used Clockify to record the time spent on this task.

![Clockify time tracking screenshot](.images/task1.png)

It took 1 hour and 21 minutes.