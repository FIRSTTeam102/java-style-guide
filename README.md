# 1 Introduction
This document will serve as a list of conventions and recommendations for working with WPILib Java and other libraries as a member of Team 102. This guide is heavily based on [WPILib's Java Style Guide](https://github.com/wpilibsuite/styleguide/) and our original [C++ style guide](https://github.com/FIRSTTeam102/cpp-style-guide/), with modifications based on our evolving conventions and practices. This is a guide, not a set of laws. If anything is unclear, use your best judgement and then contact the programming lead with the question. They will decide the correct styling and add it to this guide if necessary.

Other teams, you are free to use, distribute, and contribute to this guide under the MIT License.

## 1.1 Terminology Notes
This document will assume familiarity with the basic terminology of WPILib and the libraries Team 102 uses, including but not limited to, subsystems, commands, AdvantageKit inputs, etc. In this document, unless otherwise noted:

- The term *class* refers to an "ordinary" class, enum, interface, annotation, record, or other extension of the common Java 'class'
- The term comment always refers to implementation comments. We do not use the phrase "documentation comments", instead using the term "[Javadoc](https://en.wikipedia.org/wiki/Javadoc)."

Other terminology notes will appear throughout the document as necessary

### 1.1.1 Rule Importance Terms
The terms *must*, *can*, and *should* have special meanings in this document

- A ***must*** requirement must be followed
- A ***should*** requirement is a strong recommendation
- A ***can*** requirement is a less strict guideline

## 1.2 Guide Notes
The code in this document is **non-normative**, meaning that styling of example code in parts that aren't about the rule it is exemplifying does not have to be followed. E.g., example code formatting is not taken as a hard rule.

# 2 Source File Structure
A source file must consist of, in order:

1. Package statement
2. Import statements
3. Exactly one top-level class

Exactly one blank line should separate each section that is present.

## 2.1 Terminology
- *Line wrapping*: when one line of code is split into multiple for readability purposes.

## 2.2 Package Statement
Package statements must not be line-wrapped

## 2.3 Import Statements
Import statements must not be line-wrapped, and should be ordered as such (each group itself organized alphabetically):

1. Static imports, in one group (*note:* unlike the WPILibJ guide, we allow and encourage wildcard imports in specific cases as covered in ##.##)
2. Non-command local imports (ex: `frc.robot.subsystems.Intake`)
3. Local command imports (ex: `frc.robot.commands.intake.SetIntakeSpeed`)
4. WPILib package imports
5. Vendor/3rd Party Libraries
6. Java imports

## 2.4 Class Declaration
Each top-level class must reside in its own source file, named accordingly. There must be no more than one top-level class in each file. (example, the top-level class `SwerveModule` resides in `SwerveModule.java`

### 2.4.1 Class Member Ordering
The ordering of the members of a class can have a great effect on learnability, but there is no single correct recipe for how to do it. Different classes may order their members differently.

What is important is that each class must order its members in some logical order, such its maintainer could explain if asked. For example, new methods are not just habitually added to the end of the class, as that would yield "chronological by date added" ordering, which is not a logical ordering.

#### 2.4.1.1 Overloads: never split
If a class has an overloaded constructor or method, they must appear sequentially. If an overloaded constructor or method serves to provide default values, the constructor/method with more parameters (the more specific one) should appear first.
```java
/* more specific constructor */
public SetIntakeSpeed(Intake intake, double speed, boolean isIndexing) {
  this.speed = speed;
  this.intake = intake;
  this.isIndexing = isIndexing;
  addRequirements(intake);
}
/* constructor that provides a default speed placed second */
public SetIntakeSpeed(Intake intake, boolean isIndexing) {
  this(intake, isIndexing ? IntakeConstants.indexSpeed : IntakeConstants.intakeSpeed, isIndexing);
}
```
If the constructors/methods are not used for this purpose, order them in the most logical sequence.

#### 2.4.1.2 AdvantageKit ordering
All 3 required declarations/initializations for AdvantageKit input logging should be placed sequentially in the following order:

- Inputs class definition (as a static class)
- Inputs object initialization
- Definition of the updateInputs() method (as a non-static method)
```java
@AutoLog
public static class IntakeIOInputs {
  public double current_A = 0.0;
  public double voltage_V = 0.0;
  public double tempature_C = 0.0;
  public double percentOutput = 0.0;
  public boolean noteSensor = false;
}

public IntakeIOInputsAutoLogged inputs = new IntakeIOInputsAutoLogged();

public void updateInputs(IntakeIOInputs inputs) {
  inputs.current_A = motor.getOutputCurrent();
  inputs.voltage_V = motor.getBusVoltage();
  inputs.tempature_C = motor.getMotorTemperature();
  inputs.percentOutput = motor.getAppliedOutput();
  inputs.noteSensor = !noteSensor.get();
}
```
If the inputs are defined within a separate IO file, the object initialization should be omitted and instead the inputs object should be initialized within the subsystem file.

# 3 Project Organization
All source code (files with a `.java` extension) must be contained within `src/main/java/frc/robot`. No source files can be placed any levels up from this folder. Unless otherwise noted, this folder will be treated as the source code root folder for the rest of this section. (Example: A reference to the `/subsystems/` folder actually refers to `src/main/java/frc/robot/subsystems/`)

`Main.java`, `Robot.java`, and `RobotContainer.java` must be placed directly in this directory, not in subfolders.

## 3.1 Commands
Any and all files completely dedicated to commands (a namespace for commands, inherit from a Command class, etc.) must be placed within the `/commands/` folder. Commands or methods that return commands which are placed within other files need not be moved into the `/commands/` folder, assuming the placement outside of the `/commands/` folder is more logical. The rest of section 3.1 will refer to commands defined within the `/commands/` folder, in their own file as the top-level class unless otherwise specified.

### 3.1.1 Organize by Subsystem
If a command's main function is related to a single subsystem, such as only moving the arm or only spinning the shooter, it should be in a folder named after the subsystem in question.

`/commands/intake/SetIntakeSpeed.java`, `/commands/arm/SetArmPosition.java`, `/commands/arm/ManualArmControl,java` from [2024](https://github.com/FIRSTTeam102/robot2024)

### 3.1.2 Organize by Purpose
If a command's main function is related to a single purpose/action, and uses multiple subsystems in a way where one is not clearly the most relevant, it should be in a folder that relates to its purpose.

`/commands/scoring/SetScoringPosition.java` from [2023](https://github.com/FIRSTTeam102/robot2023)

### 3.1.3 Autos on their Own
Autonomous routines and commands and methods only used in autonomous should be placed either in their own file (`/commands/Autos.java` or something similar), or within the folder `/commands/auto/` if there is a large number of autonomous-related commands.
