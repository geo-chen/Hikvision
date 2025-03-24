# Hikvision

**Product**: Dashcam

**Model**: D1

## Finding 1: Common default password across all dashcams

**Description**: This allows an attacker to connect to the dashcam's network and interact with the dashcam. The SSID is always broadcasted and there's no secondary device pairing required. The wifi credentials are also hardcoded in the dashcam's config file in plaintext.

**Vulnerability Type**: Incorrect Access Control

**Vendor of Product**: Hikvision

**Affected Product Code Base**: D1

**Affected Component**: Authentication mechanism, plaintext password, lack of device pairing

**Attack Type**: Remote

**Impact Code execution**: False

**Impact Information Disclosure**: True

**Attack Vectors**: The dashcam ships with the same default password to all devices, does not require device registration/pairing, and writes the password to a config file in plaintext, increasing the susceptibility of a remote attacker connecting to it.

**Has vendor confirmed or acknowledged the vulnerability?**: Yes

## Finding 2: Unauthenticated web server and rtsp services

**Description**: Once the attacker is connected to the dashcam's network, a list of videos can be viewed without any authentication:
192.168.1.1/cgi-bin/Config.cgi?action=dir&property=Normal&backward=1&format=all&count=10&from=0

And then dumped via 192.168.1.1/thumb/mnt/mmc/Normal/ch1/ch1_*TS
The RTSP feed can be accessed directly at rtsp://192.168.1.1:554/liveRTSP/av4

**Vulnerability Type**: Incorrect Access Control

**Vendor of Product**: Hikvision

**Affected Product Code Base**: D1

**Affected Component**: Web server and RTSP service

**Attack Type**: Remote

**Impact Code execution**: False

**Impact Information Disclosure**: True

**Attack Vectors**: An attacker connected to the dashcam's network can access all video recordings and live feeds without any authentication. 

**Has vendor confirmed or acknowledged the vulnerability?**: Yes


## Finding 3: Exposed OS password

**Description**: The OS password of the dashcam can be extracted from the firmware (downloaded from official website https://www.hikvision.com/sg/support/download/firmware/) directly because it's not XOR or encrypted or obfuscated - user:ad<REDACTED>.

![image](https://github.com/user-attachments/assets/45f7b1e3-e88c-4845-b56b-1fa32c532f37)

 ![image](https://github.com/user-attachments/assets/f719cfff-030f-4b8a-921b-98412943df92)

**Vulnerability Type**: Insecure Permissions

**Vendor of Product**: Hikvision

**Affected Product Code Base**: AE-DC2018 Firmware v2.0.3_240510

**Affected Component**: Plaintext OS credentials

**Attack Type**: Remote

**Impact Code execution**: True

**Impact Information Disclosure**: True

**Attack Vectors**: An attacker can obtain the password of dashcam's OS from the dashcam's firmware that's hosted publicly on the manufacturer's website.

**Has vendor confirmed or acknowledged the vulnerability?**: Yes


## Finding 4: Rooting the Dashcam

**Description**: The dashcam has telnet open and the root account is set up with no password. An attacker connected to the dashcam's root account via telnet would have remote and privileged control over the dashcam. There are no sounds or warnings given to the dashcam owner when the root account is logged into remotely. An attacker would be able to change the configurations, disable battery protection to drain the car's battery, upload backdoor, etc.

![image](https://github.com/user-attachments/assets/5c2c9260-7615-4d50-95a6-e973afd569db)

![image](https://github.com/user-attachments/assets/3b930854-13ed-474f-b65f-f0bbbdd8c19b)

![image](https://github.com/user-attachments/assets/bf748c64-c89c-4454-b1e3-0f63c0867958)


**Vulnerability Type**: Insecure Permissions

**Vendor of Product**: Hikvision

**Affected Product Code Base**: AE-DC2018 Firmware v2.0.3_240510

**Affected Component**: Dashcam OS

**Attack Type**: Remote

**Impact Code execution**: True

**Impact Information Disclosure**: True

**Attack Vectors**: An attacker can obtain root privilege on the dashcam's telnet service and change the dashcam's configurations, disable battery protection to drain the car's battery, or even upload a backdoor.

**Has vendor confirmed or acknowledged the vulnerability?**: Yes


## Disclosure Timeline

7 Mar 2025 - Reported to manufacturer

11 Mar 2025 - Follow-up email sent to manufacturer

11 Mar 2025 - Manufacturer acknowledged report

11 Mar 2025 - Manufacturer sent questions to help in investigation

11 Mar 2025 - Provided manufacturer with response




