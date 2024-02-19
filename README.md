# 1 Introduction
This document will serve as a list of conventions and recommendations for working with WPILib Java and other libraries as a member of Team 102. This guide is heavily based on [WPILib's Java Style Guide](https://github.com/wpilibsuite/styleguide/) and our original [C++ style guide](https://github.com/FIRSTTeam102/cpp-style-guide/), with modifications based on our evolving conventions and practices. This is a guide, not a set of laws. If anything is unclear, use your best judgement and then contact the programming lead with the question. They will decide the correct styling and add it to this guide if necessary.

Other teams, you are free to use, distribute, and contribute to this guide under the MIT License.

## 1.1 Terminology Notes
In this document, unless otherwise noted:

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

