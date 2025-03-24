# JDK Installation Guide

Here are the step-by-step instructions for installing the Java Development Kit (JDK):

## Step 1: Choose Your JDK Version
- Decide which JDK version you need (e.g., JDK 11, 17, or 21)
- Consider your project requirements and long-term support needs

## Step 2: Download the JDK
- Visit the official Oracle website (oracle.com/java/technologies/downloads/) or alternative sources like OpenJDK (openjdk.org)
- Select your operating system (Windows, macOS, or Linux)
- Choose the appropriate installer package for your system

## Step 3: Run the Installer
**For Windows:**
- Double-click the downloaded .exe file
- Follow the installation wizard instructions
- Note the installation directory (typically C:\Program Files\Java\jdk-version)

**For macOS:**
- Open the downloaded .dmg file
- Double-click the package installer (.pkg file)
- Follow the installation prompts

**For Linux:**
- For Debian/Ubuntu: Use `sudo apt install openjdk-xx-jdk` (replace xx with version)
- For RPM-based systems: Use `sudo yum install java-xx-openjdk-devel`
- Or extract the downloaded tarball to your preferred location

## Step 4: Set Environment Variables
**For Windows:**
- Right-click "This PC" or "Computer" → Properties → Advanced system settings
- Click "Environment Variables"
- Create/edit JAVA_HOME: Set to your JDK installation path (e.g., C:\Program Files\Java\jdk-17)
- Edit Path variable: Add %JAVA_HOME%\bin

**For macOS/Linux:**
- Edit your shell profile file (~/.bash_profile, ~/.zshrc, etc.)
- Add: `export JAVA_HOME=/path/to/your/jdk`
- Add: `export PATH=$JAVA_HOME/bin:$PATH`
- Apply changes with `source ~/.bash_profile` (or relevant profile)

## Step 5: Verify Installation
- Open a terminal or command prompt
- Run `java -version` to verify Java runtime
- Run `javac -version` to verify Java compiler
