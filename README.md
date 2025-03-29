# iot_pmdoro

Study buddy is a compact workstation assistant that guides the user toward a healthy lifestyle and productivity habits.

![image](https://github.com/user-attachments/assets/d8823197-0e9e-4483-8ac2-9df04e7382c3)

Figure 1: The connections between the sensor and the M5 Stack

It aims to challenge 1) unhealthy sitting posture and eye problems from extended times at workstations, 2) decreased productivity, and 3) distractions during work time.

The project was specifically created for students and office workers; universities and companies where unhealthy productivity habits are rampant.

Study buddy allows the user to set a work-break schedule (Pomodoro technique) that they can customize to their own needs. It also measures the angle between the user’s eyes and body and the computer, allowing for a sustained healthy posture. The device alerts the user if they are sitting while the break time is ongoing in order to encourage movement, especially for office workers who sit for long periods of time. The device also lets the user display ‘free’ or ‘busy’ based on their focus level, which allows coworkers/friends nearby to see whether they are available for conversation.

Objectives:
- To keep the distance between the user and the screen between 50-70 cm and alert the user upon non-compliance,
- To let the user utilize the Pomodoro technique study/work method upon wish,
- To alert the user when work and break times begin and end,
- To encourage the user to move around during breaks,
- To let the user demonstrate when they are free and when they are busy to nearby colleagues,
- To display the bending angle of the back.

Technical Details:
The ultrasonic sensor was connected to the actuator as seen in Figure 1: the UCC end was connected to the 5V inlet for powering the sensor, Trig end was connected to the G33 inlet, Echo end was connected to the G32 inlet, and gnd was connected to the ground.

The ultrasonic sensor receives input in the form of time. The Trig pin is set on a high state for 10 µs, which induces an 8 cycle ultrasonic burst at the speed of sound. The created burst is then received by Echo pin, and the Echo inlet returns the time the sound wave took to return. The speed of sound is 0.034 cm/µs, thus the distance to any object can be found by multiplying the time the wave took to return with the speed of sound and then dividing by two (due to the sound echoing back, taking twice the time it takes to reach the object). 

The equation is as below: distance(cm)=(0.034cm/µm)∗time(µs)/2distance(cm)=(0.034cm/µm)∗time(µs)/2

It should be noted that solely this distance does not denote the distance between the eye to the computer, because the sensor is placed at the bottom of the computer screen, to the computer end of the h line in Figure 2.

![image](https://github.com/user-attachments/assets/f35eb6e3-a95f-441c-98d5-6d39ce487279)

As shown in Figure 2, the distance from the eye to the computer is measured from the top of the computer. Therefore, the distance needs to be adjusted based on a recommended 30° angle between the eye view and the bottom of the screen. This can be achieved by a simple trigonometric calculation as shown below: d=h∗cos(30∗π/180)d=h∗cos(30∗π/180) 
where d and h are quantities shown in Figure 1 and there is a conversion between degrees and radians, as the trigonometric functions take radians only.

During the work period, whenever the user stands closer than 50 cm, the device displays “GO BACK” on the screen to alert the user. At the end of the work interval, the “BREAK” text is shown on the screen and a five-minute break begins. For the duration of the break, the user is not supposed to come near the screen since we aim to encourage users to walk around as part of the physical health initiative. After the break is over, the device displays “Great!” for encouragement. By pressing the middle button again, the program will open another Pomodoro session. By using any of the two other buttons, the free/busy display can be shown.

The functionalities of the Pomodoro and User-Computer distance were tested by live coding the M5. The first test saw the ultrasound output work with inverse parameters. In other words, when the user distanced themselves away from the ultrasound sensor, the M5 displayed “GO BACK”, creating, unintentionally, a dystopian device trying to control the user. Similarly, during the break, the ultrasound would display the text “NO, GO RELAX” when the user got closer to the sensor. These errors were fixed by changing the signs of inequality within the code. Other than these errors, there were no major changes required. In order to debug, the serial plotter and monitor were used to visualize in real-time what the M5 and the ultrasound sensors were calculating.

![image](https://github.com/user-attachments/assets/ce82f8c7-bc6d-40e6-8f26-596b9ef3abfe)

Figures 3-7: Pomorodo timer, user-screen distance regulation, break timer, break time movement initiation, positive feedback, respectively.

The free/busy state was the first functionality to be implemented due to its simplicity. For the testing, the buttons were inverted, making the free state appear in the button intended for the busy state and vice versa. It was determined that being busy was likely to be the default state when working, so the busy button was placed at the right where the right-handed majority could naturally press it. Figures 8 and 9 show the implementation of free/busy states. This functionality fulfilled objective 5 in the problem definition.

![image](https://github.com/user-attachments/assets/25adec0d-ee7c-4bdb-bd1f-c5d22d233ca1)

Figures 8 and 9: The busy and free state displays



