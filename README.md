# Android-Vulnerabilities

## Resources
### Learning
- https://www.owasp.org/index.php/Projects/OWASP_Mobile_Security_Project_-2015_Scratchpad
- http://resources.infosecinstitute.com/cracking-damn-insecure-and-vulnerable-apps-diva-part-1/
- http://resources.infosecinstitute.com/android-hacking-and-security-part-18-introduction-to-reverse-engineering/
- http://resources.infosecinstitute.com/android-application-hacking-insecure-bank-part-1/
- https://androidtamer.com/learn_android_security
- https://www.owasp.org/index.php/OWASP_Mobile_Security_Project

### Vulnerable Tools
- https://github.com/payatu/diva-android
- https://github.com/dineshshetty/Android-InsecureBankv2


### Attacking Tools
- Dex2Jar - https://sourceforge.net/projects/dex2jar/files/dex2jar-2.0.zip/download
- JD-GUI - https://github.com/java-decompiler/jd-gui/releases/download/v1.4.0/jd-gui-1.4.0.jar
- APK-Tool - https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.2.0.jar
- http://www.vaibhavpandey.com/apkstudio/
- Similiar to Kali - https://androidtamer.com/
- https://labs.mwrinfosecurity.com/tools/drozer/

### Securing Tools
- https://www.owasp.org/index.php/OWASP_SeraphimDroid_Project

### Debugging Compiled APK
- https://blog.netspi.com/attacking-android-applications-with-debuggers/


# Lesson Objective
To understand the vulnerabilities on the mobile platform as growing number of users are using a personal smartphones and such devices have complex operations that we might not understand the vulnerability behind it. Today's lesson will be based on using Top 10 Mobile Vulnerabilities provided by OWASP as a guideline.

# Top 10 Vulnerabilities
- M1 - Improper Platform Usage
- M2 - Insecure Data Storage (1)
- M3 - Insecure Communication
- M4 - Insufficient Cryptography
- M5 - Insecure Authentication
- M6 - Client Code Quality
- M7 - Code Tampering
- M8 - Reverse Engineering (1)
- M9 - Extraneous Functionality

# Tips
1. Logcat
2. Reversed Code
3. 

# M1 - Improper Platform Usage
Misuse of a platform feature or failure to use platform security controls. It might include Android intents, platform permissions, misuse of TouchID, the Keychain, or some other security control that is part of the mobile operating system. There are several ways that mobile apps can experience this risk.

# M8 - Reverse Engineering
### Resources
- http://resources.infosecinstitute.com/cracking-damn-insecure-and-vulnerable-apps-diva-part-1/
- http://resources.infosecinstitute.com/android-hacking-and-security-part-18-introduction-to-reverse-engineering/

## Programs Required
- Dex2Jar - https://sourceforge.net/projects/dex2jar/files/dex2jar-2.0.zip/download
- JD-GUI - https://github.com/java-decompiler/jd-gui/releases/download/v1.4.0/jd-gui-1.4.0.jar
- APK-Tool - https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.2.0.jar

## Steps
### Reverse Engineer APK Files
1. Run the following command in terminal on the APK

``` bash
sh dex2jar.sh diva-beta.apk
```
2. Once done, a jar file should be generated.
3. Open the jar file using JD-GUI
4. Now you have all the Java Files

### Find AndroidManifest.xml
AndroidManifest.xml contains all Android intents (pages) and permissions that the application provides.
1. Run the following command in terminal

```bash
java -jar apktool_2.0.3.jar d diva-beta.apk -o output
```
2. Now you should see the XML Document!

## Challenge 1 - Insecure Logging (DIVA Android)
Sometimes developers keeps sensitive data logged into the developer console. Find a way to extract the information keyed in by the user

Hint: logcat

### Solution
1. Run the following command in terminal

``` bash
$ adb logcat
```
2. Look for the following line in terminal

``` java
E/diva-log( 1695): Error while processing transaction with credit card: 0000000000
```
3. Open up JD-GUI to see the code causing this vulnerability

## Challenge 2 -

# Android Storage Options
https://developer.android.com/guide/topics/data/data-storage.html
- Shared Preferences
- SQLite Databases
- Internal Storage
- External Storage
- Network Connection

# Places to Try
- Try BB Learn App. See where your credentials are stored
- 