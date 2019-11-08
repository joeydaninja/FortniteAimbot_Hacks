// Display that the program has started to the screen.
    Brain.Screen.print("IAG CONTROLS");
    
    // Use these variables to set the speed of the arm and claw.
    static int ARMSPEEDPCT  = 30;
    static int CLAWSPEEDPCT = 256;
    static int GUNSPEEDPCT = 10;
    
    // Create an infinite loop so that the program can pull remote control values every iteration.
    // This loop causes the program to run forever.
    while(true) {
      //Drive Control
      //Set the left and right motor to spin forward using the controller's Axis positions as the velocity value.
      LeftMotor.spin(vex::directionType::rev, Controller1.Axis3.position(), vex::velocityUnits::pct);
      RightMotor.spin(vex::directionType::rev, Controller1.Axis2.position(), vex::velocityUnits::pct);
      // Arm Control
      // If button up is pressed...
      if (Controller1.ButtonR1.pressing()) { 
        //...Spin the arm motor forward.
        LeftArmMotor.spin(vex::directionType::fwd, ARMSPEEDPCT, vex::velocityUnits::pct);
        RightArmMotor.spin(vex::directionType::fwd, ARMSPEEDPCT, vex::velocityUnits::pct);

      }
      // else If the down button is pressed...
      else 
      if (Controller1.ButtonR2.pressing()) { 
        //...Spin the arm motor backward.
        LeftArmMotor.spin(vex::directionType::fwd, -ARMSPEEDPCT, vex::velocityUnits::pct);
        RightArmMotor.spin(vex::directionType::fwd, -ARMSPEEDPCT, vex::velocityUnits::pct);
      }
      // else If neither up or down button is pressed...
      else { 
        //...Stop the arm motor.
        LeftArmMotor.stop(vex::brakeType::hold);
        RightArmMotor.stop(vex::brakeType::hold);
        }

      if (Controller1.ButtonL1.pressing()) {
          LeftClawMotor.spin(vex::directionType::fwd, CLAWSPEEDPCT, vex::velocityUnits::pct);
          RightClawMotor.spin(vex::directionType::fwd, CLAWSPEEDPCT, vex::velocityUnits::pct);
      }

      else
      if (Controller1.ButtonL2.pressing()) {
          LeftClawMotor.spin(vex::directionType::fwd, -50, vex::velocityUnits::pct);
          RightClawMotor.spin(vex::directionType::fwd, -50, vex::velocityUnits::pct);        
      }

      else {
          LeftClawMotor.stop(vex::brakeType::hold);
          RightClawMotor.stop(vex::brakeType::hold);


      }

      
      if (Controller1.ButtonA.pressing()) {
          GunMotor.spin(vex::directionType::fwd, GUNSPEEDPCT, vex::velocityUnits::pct);
      }

      else {
          GunMotor.stop(vex::brakeType::hold);
      }

    
    // Sleep the task for a short amount of time to prevent wasted resources.
    vex::task::sleep(20);
    }
