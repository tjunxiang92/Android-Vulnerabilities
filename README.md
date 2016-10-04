# Android Vulnerabilities 
To understand the vulnerabilities on the mobile platform as growing number of users are using a personal smartphones and such devices have complex operations that we might not understand the vulnerability behind it. Today's lesson will be based on using Top 10 Mobile Vulnerabilities provided by OWASP as a guideline.

## Resources  
## All In One Package
- https://drive.google.com/open?id=0B_96EHY-E-1GX2JMbEVUaG5VWjg
	- Android Emulator
	- VM with Tools Installed

## Files in the VM
|                      | Windows           | Linux  | Mac |
| ------------ |:-------------:|:-----:|:-----:|
| **Genymotion** | https://dl.genymotion.com/releases/genymotion-2.8.0/genymotion-2.8.0-vbox.exe | https://dl.genymotion.com/releases/genymotion-2.8.0/genymotion-2.8.0-linux_x64.bin | https://dl.genymotion.com/releases/genymotion-2.8.0/genymotion-2.8.0.dmg |
| **VirtualBox** | https://www.virtualbox.org/wiki/Downloads
| Java JDK      | http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html |
| Drozer          | https://labs.mwrinfosecurity.com/tools/drozer |
| APK Studio  | http://www.vaibhavpandey.com/apkstudio/ |
| JADX | https://github.com/skylot/jadx/releases/download/v0.6.0/jadx-0.6.0.zip |
| APK Tool | https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.2.0.jar |

### Learning
- https://www.owasp.org/index.php/Projects/OWASP_Mobile_Security_Project_-2015_Scratchpad
- http://resources.infosecinstitute.com/cracking-damn-insecure-and-vulnerable-apps-diva-part-1/
- http://w1a2d3s4q5e6.blogspot.sg/2016/08/diva-android-13input-validation-issues.html
- http://resources.infosecinstitute.com/android-hacking-and-security-part-18-introduction-to-reverse-engineering/
- http://resources.infosecinstitute.com/android-application-hacking-insecure-bank-part-1/
- https://androidtamer.com/learn_android_security
- https://www.owasp.org/index.php/OWASP_Mobile_Security_Project

### Vulnerable Tools
1. https://github.com/payatu/diva-android
2. https://github.com/jackMannino/OWASP-GoatDroid-Project
3. https://github.com/dineshshetty/Android-InsecureBankv2
4. https://github.com/intrepidusgroup/ig-learner

### Decompilers
- APK Studio - https://bintray.com/vaibhavpandeyvpz/generic/apkstudio/view
- https://github.com/skylot/jadx/releases
- https://sourceforge.net/projects/dex2jar/


### Obfuscators
- Comparisons - http://proguard.sourceforge.net/index.html#alternatives.html
- ProGuard - http://proguard.sourceforge.net/
- yGuard - http://www.yworks.com/products/yguard
- DexGuard - https://www.guardsquare.com/dexguard
	- String Encryption

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




# Top 10 Vulnerabilities
- M1 - Improper Platform Usage
- M2 - Insecure Data Storage
- M3 - Insecure Communication
- M4 - Insufficient Cryptography
- M5 - Insecure Authentication
- M6 - Client Code Quality
- M7 - Code Tampering
- M8 - Reverse Engineering
- M9 - Extraneous Functionality

## M1  - Improper Platform Usage
-  misuse of a platform feature
- failure to use platform security controls
- Examples
	- Android intents
	- Platform permissions 
	- Misuse of TouchID, the Keychain
	- some other security control that is part of the mobile operating system

## M3 - Insecure Communication
This covers poor handshaking, incorrect SSL versions, weak negotiation, cleartext communication of sensitive assets, etc.

M1, M3, M5, M7, M10 - Slides
M2, M4, M6, M8 - Workshop

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

# Android Storage Options
https://developer.android.com/guide/topics/data/data-storage.html
- Shared Preferences
- SQLite Databases
- Internal Storage
- External Storage
- Network Connection

# Drozer - Installation for Mac
Credits to: https://blog.ropnop.com/installing-drozer-on-os-x-el-capitan/

## Work on Virtual Env
```bash
sudo pip install virtualenvwrapper
mkvirtualenv drozer
workon drozer
```

## Set up Drozer folder
```bash
mkdir drozer-install
cd drozer-install
```

## Reinstall OpenSSL & PyOpenSSL
```bash
brew uninstall openssl
brew install openssl
wget https://pypi.python.org/packages/source/p/pyOpenSSL/pyOpenSSL-0.13.tar.gz
tar xzvf pyOpenSSL-0.13.tar.gz
cd pyOpenSSL-0.13
sed -i '' 's/X509_REVOKED_dup/X509_REVOKED_dupe/' OpenSSL/crypto/crl.c
python setup.py build_ext -L/usr/local/opt/openssl/lib -I/usr/local/opt/openssl/include
python setup.py build
python setup.py install
```

## Some dependencies
```bash
easy_install --allow-hosts pypi.python.org protobuf==2.4.1
easy_install twisted==10.2.0
```

## Install drozer egg
```bash
cd ..
wget https://github.com/mwrlabs/drozer/releases/download/2.3.4/drozer-2.3.4.tar.gz
tar xvfz drozer-2.3.4.tar.gz 
easy_install ./drozer-2.3.4-py2.7.egg
nano /usr/local/bin/drozer
```

## Write file to drozer
```python
#!/Users/rflather/.virtualenvs/drozer/bin/python
# EASY-INSTALL-SCRIPT: 'drozer==2.3.4','drozer'
__requires__ = 'drozer==2.3.4'  
__import__('pkg_resources').run_script('drozer==2.3.4', 'drozer')  
```

