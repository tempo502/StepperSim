# StepperSim
Ryan Carlyle

This is an Excel spreadsheet model of an open-loop stepper motor driver system. It is intended to facilitate drivetrain design for light CNC machinery such as 3D printers. 

New Feature! Try the stepper motor torque/RPM curve predictor spreadsheet. This is a useful tool for drivetrain design, such as picking gear ratios. It seems to be a pretty accurate estimate -- typically +/-10% from measured curves unless the real motor has resonance issues.

## How to use the stepper/driver simulators:
1. Download the appropriate spreadsheet for your stepper driver chip using the "raw" button or other suitable method of your choice, and open in a recent version of Excel. (LibreOffice also appears to work.) If there is a "with X" sheet, that is an experimental version that may run slower or have new bugs. 
2. Follow the in-file instructions to input the highlighted parameters for your motor, power supply, driver chip, and drivetrain.
3. Look at the output charts and interpret what you see. Hint: you want the coil current to closely track the target current.

Note that the calculation sheets are locked solely to prevent accidental editing... the password to unlock them is "StepperSim" (case sensitive)

Unfortunately, each driver chip has its own special control logic and features, so each spreadsheet is highly customized for a particular driver chip. Additional drivers may be added over time. Currently supported drivers:
- Allegro A3977 -- Makerbot Gen 4 electronics
- Allegro A4988 / A4982 -- Pololu, StepStick, BotStep
- TI DRV8825 -- Pololu, SureStepr, StepStick
- THB6128 -- Silencioso, RAPS128, SureStepr (also works for LV8729)

Future driver goals:
- "Optimal" driver (no PWM chopper) to check motor performance with adaptive drivers or high-end DSP stepper drivers like Leadshines
- Allegro A5984 - SureStepr
- Trinamic TMC2100 -- SilentStepStick
- Trinamic TMC2660 -- Duet Wifi

If you want to simulate a new driver with an "adaptive" current chopping scheme like the A5984 or TMC2xxx series, you can get a ballpark simulation out of the THB6128 sheet. All highly-advanced chopping algorithms should produce reasonably similar waveforms. (If your driver is really good, all the simulator really shows you is motor/voltage behavior.) 

## Basic model methodology:
3. Calculate the instantaneous state parameters (such as microstep target and back-emf voltage)
4. Calculate how long until the driver's PWM chopper will next change state
4. Calculate coil current at that time via a simple first-order RL circuit model
5. Increment time to the next state and repeat
6. Chart the output

There's also a lot of logic to determine how the driver will act at each state change and to output some useful calculations. But that's details. 
