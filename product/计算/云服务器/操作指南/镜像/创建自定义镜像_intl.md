## Overview of Creation
### Common steps
You can launch an instance with a public image or a service marketplace image, and then connect to the instance and deploy your software environment. If the instance runs normally, you can create a new custom image based on this instance as needed, so that you can use this image to launch more new instances that have the same custom configurations with the original one.

### Best practice
 - **Shut down instance:**
Shut down the instance before you can create a custom image to ensure that the image has exactly the same deployment environment as that of the current instance.
 - **Data migration:**
To keep the data in the original instance data disk when you lunch a new instance, you can first take a Snapshot of the data disk, and then create a new CBS data disk with this snapshot when launching the new instance.

### Limit
 - Each region supports a maximum of 10 custom images.

### Notes
1. The following directory and files will be removed.
- /var/log/  
- /root/.bash_history, /home/ubuntu/.bash_history (Ubuntu system)

2. /etc/fstab will reset to avoid launch failure due to no data disk found.

## Creation Method
### Create an image from an instance via the console

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. Shut down the instance. Select the instance to be shut down, and then click **Shutdown** on the top.
 ![Create Custom Images](https://main.qcloudimg.com/raw/09102b9c844236d102a7f9e29a7e595c.png)
![Create Custom Images](https://main.qcloudimg.com/raw/4b8516ecd808a8a9ffd06ad90ba27af1.png)

 3. Click **More** on the right side of the instance used to create an image, and click **Create Image**.
 ![Create Custom Images](https://main.qcloudimg.com/raw/5f4190da7a8b547fd751c5b5e0790755.png)
 4. Enter **Image Name** and **Image Description** in the pop-up box, and click **OK** to submit the creation application.
 ![Create Custom Images](https://main.qcloudimg.com/raw/80ee47a3d7f6d0b640b2bc3b04fa881c.png)

 5. To purchase a server with the same image as the previous one, click **Create CVM** on the right side of the image in the image list.
![](https://main.qcloudimg.com/raw/31c3ec91fe0e42f7f32d1025e04c5671.png)

### Create an image using API
You can use the API CreateImage to create a custom image. For more information, please see the API [Create Image](/doc/api/229/1273).
