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

Once the attacker is connected to the dashcam's network, a list of videos can be viewed without any authentication:
192.168.1.1/cgi-bin/Config.cgi?action=dir&property=Normal&backward=1&format=all&count=10&from=0

and then dumped via 192.168.1.1/thumb/mnt/mmc/Normal/ch1/ch1_*TS
The RTSP feed can be accessed directly at rtsp://192.168.1.1:554/liveRTSP/av4

 

## Finding 3: Exposed OS password

The OS password of the dashcam can be extracted from the firmware (downloaded from official website) very easily because it's not XOR or encrypted or obfuscated - user:admin.

 ![image](https://github.com/user-attachments/assets/f719cfff-030f-4b8a-921b-98412943df92)


## Finding 4: Rooting the Dashcam

The dashcam has telnet open. Based on the above, we can infer that there's a root account with no password. Once I connected to telnet with root, I have remote and privileged control over the dashcam. There are now sounds or warnings given to the dashcam owner. I am able to change the configurations, disable battery protection to drain the car's battery, upload backdoor, etc.

![image](https://github.com/user-attachments/assets/5c2c9260-7615-4d50-95a6-e973afd569db)

![image](https://github.com/user-attachments/assets/3b930854-13ed-474f-b65f-f0bbbdd8c19b)

![image](https://github.com/user-attachments/assets/bf748c64-c89c-4454-b1e3-0f63c0867958)


## Disclosure Timeline

