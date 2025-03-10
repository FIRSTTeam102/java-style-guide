# Table of Contents

- [Table of Contents](#table-of-contents)
- [1 Introduction](#1-introduction)
	- [1.1 Terminology Notes](#11-terminology-notes)
		- [1.1.1 Rule Importance Terms](#111-rule-importance-terms)
	- [1.2 Guide Notes](#12-guide-notes)
- [2 Source File Structure](#2-source-file-structure)
	- [2.1 Terminology](#21-terminology)
	- [2.2 Package Statement](#22-package-statement)
	- [2.3 Import Statements](#23-import-statements)
	- [2.4 Class Declaration](#24-class-declaration)
		- [2.4.1 Class Member Ordering](#241-class-member-ordering)
			- [2.4.1.1 Overloads: never split](#2411-overloads-never-split)
			- [2.4.1.2 AdvantageKit ordering](#2412-advantagekit-ordering)
- [3 Project Organization](#3-project-organization)
	- [3.1 Commands](#31-commands)
		- [3.1.1 Organize by Subsystem](#311-organize-by-subsystem)
		- [3.1.2 Organize by Purpose](#312-organize-by-purpose)
		- [3.1.3 Autos on their Own](#313-autos-on-their-own)
	- [3.2 Subsystems](#32-subsystems)
		- [3.2.1 Related files](#321-related-files)
	- [3.3 Constants](#33-constants)
		- [3.3.1 Organize by Subsystem](#331-organize-by-subsystem)
		- [3.3.2 Organize by Topic](#332-organize-by-topic)
		- [3.3.3 Universal Constants](#333-universal-constants)
	- [3.4 Utilities](#34-utilities)
- [4 Formatting](#4-formatting)
	- [4.1 Terminology Notes](#41-terminology-notes)
	- [4.2 Braces](#42-braces)
		- [4.2.1 Single-line braces are optional](#421-single-line-braces-are-optional)
		- [4.2.2 Non-empty blocks: K \& R style](#422-non-empty-blocks-k--r-style)
		- [4.2.3 Empty blocks: may be concise](#423-empty-blocks-may-be-concise)
	- [4.3 Block indentation: one tab](#43-block-indentation-one-tab)
	- [4.4 One statement per line](#44-one-statement-per-line)
	- [4.5 Line Wrapping](#45-line-wrapping)
	- [4.6 Whitespace](#46-whitespace)
		- [4.6.1 Vertical Whitespace](#461-vertical-whitespace)
		- [4.6.2 Horizontal Whitespace](#462-horizontal-whitespace)
		- [4.6.3 Horizontal alignment: discouraged](#463-horizontal-alignment-discouraged)
	- [4.7 Grouping Parentheses: recommended](#47-grouping-parentheses-recommended)
	- [4.8 Specific Constructs](#48-specific-constructs)
		- [4.8.1 Enum classes](#481-enum-classes)
			- [4.8.1.1 Line breaks: keep it consistent](#4811-line-breaks-keep-it-consistent)
			- [4.8.1.2 Short enums: may be concise](#4812-short-enums-may-be-concise)
		- [4.8.2 Variable declaration](#482-variable-declaration)
			- [4.8.2.1 One variable per declaration](#4821-one-variable-per-declaration)
			- [4.8.2.2 Declared when needed, initialized ASAP](#4822-declared-when-needed-initialized-asap)
		- [4.8.3 Arrays](#483-arrays)
			- [4.8.3.1 No C-style declarations](#4831-no-c-style-declarations)
		- [4.8.4 Switch statements and expressions](#484-switch-statements-and-expressions)
			- [4.8.4.1 Expressions only](#4841-expressions-only)
			- [4.8.4.2 Default case omitted if exhaustive](#4842-default-case-omitted-if-exhaustive)
		- [4.8.5 Modifiers](#485-modifiers)
		- [4.8.6 Ternary operators](#486-ternary-operators)
- [5 Naming](#5-naming)
	- [5.1 Terminology Notes](#51-terminology-notes)
	- [5.2 Shared rules](#52-shared-rules)
	- [5.3 Units](#53-units)
	- [5.4 Rules by identifier](#54-rules-by-identifier)
		- [5.4.1 Packages](#541-packages)
		- [5.4.2 Classes and interfaces](#542-classes-and-interfaces)
			- [5.4.2.1 Classes: mostly nouns](#5421-classes-mostly-nouns)
			- [5.4.2.2 Commands: mostly verbs](#5422-commands-mostly-verbs)
			- [5.4.2.3 AdvantageKit inputs: called inputs](#5423-advantagekit-inputs-called-inputs)
			- [5.4.2.4 IO interfaces and implementations](#5424-io-interfaces-and-implementations)
		- [5.4.3 Methods](#543-methods)
		- [5.4.4 Constants](#544-constants)
		- [5.4.5 Fields, variables, and parameters](#545-fields-variables-and-parameters)
		- [5.4.6 Type variables](#546-type-variables)
- [6 Programming Practices](#6-programming-practices)
	- [6.1 Annotation usage](#61-annotation-usage)
		- [6.1.1 @Override: always used](#611-override-always-used)
		- [6.1.2 @Getter/@Setter: used when applicable](#612-gettersetter-used-when-applicable)
			- [6.1.2.1 Edge case: transformed data](#6121-edge-case-transformed-data)
		- [6.1.3 @AutoLogOutput: used where applicable](#613-autologoutput-used-where-applicable)
	- [6.2 Try/catch blocks: try to avoid](#62-trycatch-blocks-try-to-avoid)
	- [6.3 Static members: qualified using class](#63-static-members-qualified-using-class)
	- [6.4 Built-in types](#64-built-in-types)
		- [6.4.1 Numerical Values](#641-numerical-values)
	- [6.5 Generated files](#65-generated-files)
	- [6.6 Utilities](#66-utilities)
- [7 Comments and Javadoc](#7-comments-and-javadoc)
	- [7.1 Comments](#71-comments)
		- [7.1.1 As often as possible](#711-as-often-as-possible)
		- [7.1.2 Minimize yapping](#712-minimize-yapping)
	- [7.2 Javadoc](#72-javadoc)
		- [7.2.1 Exceptions: obvious and self-explanatory members](#721-exceptions-obvious-and-self-explanatory-members)
		- [7.2.2 Eception: overrides](#722-eception-overrides)


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

Each top-level class must reside in its own source file, named accordingly. There must be no more than one top-level class in each file. (example, the top-level class `SwerveModule` resides in `SwerveModule.java`)

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

`/commands/scoring/SetScoringPosition.java` from [2023](https://github.com/FIRSTTeam102/robot2023) and [2024](https://github.com/FIRSTTeam102/robot2024)

### 3.1.3 Autos on their Own

Autonomous routines and commands and methods only used in autonomous should be placed either in their own file (`/commands/Autos.java` or something similar), or within the folder `/commands/auto/` if there is a large number of autonomous-related commands.

When using PathPlanner, named commands and autos should be registered in `RobotContainer.java`

## 3.2 Subsystems

All files whose top-level class is a **subsystem** (either extending `SubsystemBase` or conceptually analagous to a WPILib `Subsystem`) must be placed within the `/subsystem/` folder.

### 3.2.1 Related files

Files that are core to a subsystem's functionality but do not either

1. Contain the main class of the subsystem; or
2. Are not the associated constants file, as covered in section 3.3

Must be placed either in a subfolder of `/subsystems/` named appropriately, or in the `/io/` folder. This decision should be made based on whatever enhances readability the most. 

(*NOTE*: The `/io/` folder must, as named, be exclusively used for interfaces and classes that deal with IO. IO interfaces/classes can be placed in a `/subsystems/` subfolder, but non-IO interfaces/classes cannot be placed in `/io/`)

`subsystems/swerve/*.java` and `io/*VisionIO.java` from [2024](https://github.com/FIRSTTeam102/robot2024)

## 3.3 Constants

Important constants such as motor IDs, PID/FF constants, enums, record definitions, etc. should be defined in a separate file contained within the `/constants/` folder. These files should deal with a specific portion of the general code only and be named accordingly, with the format `**SUBJECT**Constants.java`, where \*\*SUBJECT** is a single, capitalized noun to describe the file. What the \*\*SUBJECT** is will be described in the following rules.

### 3.3.1 Organize by Subsystem

If constants are related by a common subsystem, they should all be placed in a file named after the subsystem

`constants/IntakeConstants.java`, `constants/ShooterConstants.java` from [2024](https://github.com/FIRSTTeam102/robot2024)

### 3.3.2 Organize by Topic

If constants are related by a common topic, they should be placed in a file named after that topic

`constants/ScoringConstants.java` from [2024](https://github.com/FIRSTTeam102/robot2024)

### 3.3.3 Universal Constants

One file, `constants/Constants.java`, should contain constants that are relevant to the entire robot, not a specific subsystem/topic.

## 3.4 Utilities

Classes, static methods, and more that have utility functionality that are generally relevant to the robot should be placed within the `/util/` folder. There is no specific naming convention for the files/classes contained within this folder.

# 4 Formatting

## 4.1 Terminology Notes

- Braces: `{}`
- Brackets: `[]`
- Block-like construct: the body of a class, method or constructor.
- Logical units: Multiple lines of code that fit together logically or contextually.
- Horizontal alignment: Adding extra whitespace to lines to make certain tokens appear below other tokens

```java
// No alignment
private int x;
private String str;

// alignment
private int    x;
private String str;
```

## 4.2 Braces

### 4.2.1 Single-line braces are optional

Single-line `if`, `else`, `for`, `do`, and `while` statements can have their braces ommitted if it enhances readability.

### 4.2.2 Non-empty blocks: K & R style

Braces follow the K & R style for *non-empty* blocks and block-like constructs:

- No line break before the opening brace
- Line break after the opening brace
- Line break before the closing brace.
- Line break after the closing brace if that brace terminates a statement or the body of a method, constructor or named class. For example, there is no line break after the brace if it is followed by else or a comma.

```java
public class TestClass {
	public static void method(boolean condition) {
		if (condition) {
			doSomething();
		} else {
			doSomethingElse();
		}
	}
}
```

### 4.2.3 Empty blocks: may be concise

An empty block or block-like construct may be closed immediately after being opened, with no spaces or line breaks in-between the braces.

```java
public void doNothing() {}
```

## 4.3 Block indentation: one tab

Each time a new block or block-like construct is opened, the indent increases by one tab. When the block ends, the indent decreases by one tab, as seen in the 4.2.2 example.

## 4.4 One statement per line

Every statement must be followed by a line break.

## 4.5 Line Wrapping

Statements that are very long should be line-wrapped to enhance readability. Each line after the first in a line-wrapped statement should be indented with the standard one tab as described in 4.3.

## 4.6 Whitespace

### 4.6.1 Vertical Whitespace

A single blank line should appear between *logical units* of code. Spacing out code by logical units helps to improve readability and reduce clutter.

### 4.6.2 Horizontal Whitespace

Aside where required by Java, a single space must appear in the following situations **only**:

1. Separating any reserved word, such as `if`, `for` or `catch`, from an open parenthesis (`(`) that follows it on that line
2. Separating any reserved word, such as `else` or `catch`, from a closing curly brace (`}`) that precedes it on that line
3. Before any open curly brace (`{}`), with two exceptions:
	- `@SomeAnnotation({a, b})` (no space is used)
	- `String[][] x = {{"foo"}};` (no space is required between `{{` or `}}`, by item 8 below)
4. On both sides of any binary or ternary operator. This also applies to the following "operator-like" symbols
	- the ampersand in a conjunctive type bound: `<T extends Foo & Bar>`
	- the pipe for a catch block that handles multiple exceptions: `catch (FooException | BarException e)`
	- the colon (`:`) in an enhanced `for` ("foreach") statement
5. After `,`, `:`, or `;` or the closing parenthesis of a typecast (`)`)
6. After the double slash (`//`) that begins a single line or end-of-line comment.
7. Between the type and variable of a declaration `List<String> list` 
8. *Optional* inside both braces of an array initializer
	- `new int[] {5, 6}` and `new int[] { 5, 6 }` are both valid

### 4.6.3 Horizontal alignment: discouraged

Horizontal alignment is generally discouraged, and may only be used if it substantially increases the readability of the code.

## 4.7 Grouping Parentheses: recommended

Optional grouping parentheses are omitted only when author and reviewer agree that there is no reasonable chance the code will be misinterpreted without them, nor would they have made the code easier to read. It is not reasonable to assume that every reader has the entire Java operator precedence table memorized.

## 4.8 Specific Constructs

### 4.8.1 Enum classes

Since enum classes are classes, all other rules for formatting classes apply, but there are specific rules for enums:

#### 4.8.1.1 Line breaks: keep it consistent

For a given enum class, there can be a line break following the comma after each enum constant, or no line-breaks at all. Do not mix and match in one enum declaration, and no more than one line break per constant.

```java
/* compliant with 4.8.1.1 */
public enum Suit { 
	Clubs, Hearts, Spades, Diamonds 
}

/* also compliant */
public enum Suit {
	Clubs,
	Hearts,
	Spades,
	Diamonds
}

/* not compliant */
public enum Suit {
	Clubs, Hearts,
	Spades,
	Diamonds
}
```

#### 4.8.1.2 Short enums: may be concise

An enum with no methods and no documentation on its constants may be formatted like an array initializer

```java
/* OK */
public enum Suit {
	Clubs, Hearts, Spades, Diamonds
}

/* also OK */
public enum Suit { Clubs, Hearts, Spades, Diamonds }
```

### 4.8.2 Variable declaration

#### 4.8.2.1 One variable per declaration

Every variable declaration (field or local) declares only one variable: declarations such as `int a, b;` are not used.

#### 4.8.2.2 Declared when needed, initialized ASAP

Local variables must **not** be habitually declared at the start of their containing block or block-like construct. Instead, local variables should be declared close to the point they are first used (within reason) to minimize their scope. Local variable declarations should have initializers, or be initialized immediately after declaration.

### 4.8.3 Arrays

Arrays must be declared with the same formatting as [enums](#4811-line-breaks-keep-it-consistent).

```java
/* OK */
new int[] {0, 1, 2, 3};

new int[] {
	0, 1, 2, 3
};

new int[] {
	0,
	1,
	2,
	3
};

/* not OK */
new int[] {
	0, 1,
	2, 3
};
```

#### 4.8.3.1 No C-style declarations

Square brackets must be a part of the *type*, not the variable name. `String[] args`, not `String args[]`.

### 4.8.4 Switch statements and expressions

#### 4.8.4.1 Expressions only

The modern switch expression syntax must be used instead of the classic switch statement syntax.

```java
/* Statements: NOT ok */
switch (alliance.get()) {
	case Red:
		redAllianceFunc();
		break;
	case Blue:
		blueAllianceFunc();
		break;
	default:
		break;
}

/* Expressions: OK */
switch (alliance.get()) {
	case Red -> redAllianceFunc();
	case Blue -> blueAllianceFunc();
}
```

#### 4.8.4.2 Default case omitted if exhaustive

The `default` case expression group may be omitted if the switch statement covers all possible values of the input (e.g., is exhaustive)

### 4.8.5 Modifiers

Class and member modifiers, when present, appear in the order recommended by the Java Language Specification

```java
public protected private abstract static final transient volatile synchronized native strictfp
```

### 4.8.6 Ternary operators

The ternary operator should be used for any conditional statement with simple expressions (simple operations, return value switch, etc.). Ternary operators may not be nested.

# 5 Naming

## 5.1 Terminology Notes

- `camelCase`: Each word has its first letter capitalized. The first word is not capitalized. There are no underscores or other characters between words.
- `PascalCase`: Same as camelCase, but the first word is capitalized.
- descriptor: An extra word or abbreviation placed after an underscore after the name. For the purposes of this guide, the name and descriptor are considered separate items within the entire identifier, in the form `<name>_<descriptor>`. Descriptors are all lowercase and limited to a single word or abbreviation.
  
## 5.2 Shared rules

Identifiers use only ASCII letters and digits, and in specific cases described below, underscores.

## 5.3 Units

Fields, variables, parameters, and other related constructs that have units associated with them must have those units as a descriptor. This is to reduce confusion between units that describe the same physical quantity (feet/s vs m/s, etc.). Use standard abbreviations, and to conform with [5.2](#52-shared-rules), the word 'per' (as in 'feet per second') should be replaced with a `p` in the abbreviation ('feet per second' becomes `ftps`, not `ft/s`).

```java
/* Good examples */
double voltage_V; // Volts

double velocity_mps; // Meters per second

double velocity_rpm; // Rotations per minute

double position_ft; // Feet

/* bad examples */
double voltage; // no unit, even though may be obvious

double voltage_millivolts; // not abbreviated, should be mV
```

## 5.4 Rules by identifier

### 5.4.1 Packages

Package names are all lowercase, with separate words concatenated together. `com.example.deepspace`, not `com.example.deepSpace`

### 5.4.2 Classes and interfaces

Class and interface names must be written in PascalCase

#### 5.4.2.1 Classes: mostly nouns

Subsystems, records, enums, data classes, utilities, and most other classes should generally be named with nouns, such as `Shooter`, `ArmConstants`, `ScoringPosition`, etc.

#### 5.4.2.2 Commands: mostly verbs

Commands that have a name (e.g., not inline) should generally be named with verbs, such as `SetScoringPosition` or `IntakeWithArm`, but may be named with other terms if more applicable, such as `ManualArmControl` or `XStance`.

#### 5.4.2.3 AdvantageKit inputs: called inputs

AdvantageKit inputs classes must be named with the name of their enclosing class, with `Inputs` appended at the end, such as `ShooterInputs` and `FieldVisionInputs`.

*(**NOTE**: the 2023 and 2024 robot code currently does not comply with this rule, with the suffix instead being `IOInputs`. Continue to use this non-compliant suffix or update all other inputs class names within these projects to maintain consistency.)*

#### 5.4.2.4 IO interfaces and implementations

Interfaces that lay out IO implementations or classes that define IO must have their name suffixed with `IO`, such as `SwerveModuleIO` or `FieldVisionIO`.

The implementations of IO Interfaces must have their name be the interface they are implementing suffixed with a descriptor of the implementation. There are no specific guidelines for this descriptor. Examples include `SwerveModuleIOReal`, `GyroIOPigeon2`, and `SwerveModuleIOSim`.

### 5.4.3 Methods

Method names must be written in camelCase, and are generally verbs or verb phrases.

Method identifiers may share names but have descriptors to describe their implementation, such as `estimateScoringPosition_math` and `estimateScoringPosition_map`.

### 5.4.4 Constants

Since constants reside in their own file, it is relatively obvious when something is a constant or not, and thus they do not require a prefix or other unique characteristic. They should be named just like variables and fields.

### 5.4.5 Fields, variables, and parameters

Fields, variables, and parameters must be in camelCase, and should generally be nouns or noun phrases.

One character variable names should be avoided, except for very temporary and specific looping variable. If a multi-character name can be used without hurting readability, it should be used.

### 5.4.6 Type variables

Each type variable is named in one of two styles:

- A single capital letter, optionally followed by a single numeral (such as `E`, `T`, `X`, `T2`)
- A name in the form used for classes (see [5.4.2](#542-classes-and-interfaces)), followed by the capital letter T (examples: `RequestT`, `FooBarT`).

# 6 Programming Practices

## 6.1 Annotation usage

A general rule of thumb is that, whenever an annotation can be used in a way to reduce code clutter, it should be used. Of course, readability is prioritized, and if an annotation will make a piece of code *more* difficult to read, its use should be discarded.

### 6.1.1 @Override: always used

A method is marked with the `@Override` annotation whenever it is legal. This includes a class method overriding a superclass method, a class method implementing an interface method, and an interface method respecifying a superinterface method.

### 6.1.2 @Getter/@Setter: used when applicable

Private member variables with getter and setter methods must have those methods defined with the `@Getter` and `@Setter` annotations provided by lombok

```java
/*Compliant with 6.1.2*/
@Getter
private double readOnlyValue = 0.0;

/*Non-compliant with 6.1.2*/
private double readOnlyValue = 0.0;

public double getReadOnlyValue() {
	return readOnlyValue;
}
```

#### 6.1.2.1 Edge case: transformed data

Getter and setter methods that transform the data in some way or perform some side-effect are exempt from rule [6.1.2](#612-gettersetter-used-when-applicable), and should be placed in their own methods for readability.

### 6.1.3 @AutoLogOutput: used where applicable

When a field should be logged as-is as a RealOutput in AdvantageKit, the `@AutoLogOutput` annotation should be used rather than `Logger.recordOutput()` being called in `periodic()`.

```java
public class Example extends SubsystemBase {
	/* compliant with 6.1.3 */
	@AutoLogOutput
	private double loggedOutput = 0.0;

	/* not compliant */
	private double loggedOutput2 = 0.0;
	@Override
	public void periodic() {
		Logger.recordOutput("Example/loggedOutput2", loggedOutput2);
	}
}
```

## 6.2 Try/catch blocks: try to avoid

Try/catch blocks are only permitted if there is no other way to do something. In all other cases, they should be avoided.

(***NOTE:*** *if you are tempted to use a try/catch block, think deeply about whether you should be doing what you're trying to do in the first place. Only after going through this process multiple times should you ever entertain the thought of using one.*)

## 6.3 Static members: qualified using class

When a reference to a static class member must be qualified, it is qualified with that class's name, not with a reference or expression of that class's type.

```java
Foo aFoo = ...;

Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad
```

## 6.4 Built-in types

WPILib uses `int` for user-facing interfaces instead of `byte` to avoid casts. 

### 6.4.1 Numerical Values

Java's default data type for all numerical values which include a decimal (i.e. 24.5) is `double`, which should be used instead of `float` for consistency unless absolutely necessary. 

**IMPORTANT:** ALWAYS include a decimal place when entering a numerical value within a `double`, and especially when performing calculations within a double. For example `1/21` should be entered as `1.0/21.0`. This is because Java will identify a whole number without a decimal as an integer (type `int`) by default, which may result in errors in calculation - in the examples above, `1/21` results in the value of `0` (zero) where we would most likely prefer the result of `1.0/21.0` which produces `0.0476190476190476`. 

## 6.5 Generated files

Since changes would be overwritten upon regeneration, generated files such as `BuildConstants.java` and `*.auto` files must not be manually edited.

## 6.6 Utilities

As noted in [3.4](#34-utilities), any utility methods, classes, etc. should be placed within an appropriately named file in the `/utils/` directory. Creation of utilities is recommended, and any general methods that do not have direct relation with a subsystem or command should be categorized as utilities.

# 7 Comments and Javadoc

## 7.1 Comments

Comments should generally be full line or end-of-line with double slashes (`//`). 

### 7.1.1 As often as possible

Whenever the implementation of a method is anything less than incredibly obvious/self-explanatory, or additional notes need to be provided for future reviewers, descriptive comments must be added. Implementation comments should accurately walk through the thought process and program flow in a given implementation, so that a future reviewer can get into the original developer's mindset.

### 7.1.2 Minimize yapping

Extraneous comments, jokes, self-deprecation, and more are not permitted to be part of any comments. Implemetation comments and comments that provide helpful notes should be concise and professional, without extraneous language.

## 7.2 Javadoc

At the *minimum*, Javadoc is present for every `public` class, and every `public` or `protected` member of a class, with a few exceptions noted below.

Other classes and methods still have Javadoc as needed. Whenever an implementation comment would be used to define the overall purpose or behavior of a class, method or field, that comment is written as Javadoc instead. (It's more uniform, and more tool-friendly.)

### 7.2.1 Exceptions: obvious and self-explanatory members

Javadoc is optional for simple, obvious methods like getters and setters, where there `really and truly` is nothing better to say than "Returns the thing".

*(**NOTE:**) It is not appropriate to cite this exception to justify omitting relevant information that a typical reader might need to know. For example, for a method named `getCanonicalName`, don't omit its documentation (with the rationale that it would say only `/** Returns the canonical name. */`) if a typical reader may have no idea what the term "canonical name" means!*

### 7.2.2 Eception: overrides

Javadoc does not need to be present on a method that overrides a supertype method.
