# 1. Setup AWS Ubuntu Server
## 1.1 Launching an AWS Instance
Firstly, click on the `Launch instance` button to start the process of launching a new instance. And name that instance link `Jenkins`.

<img src="./assets/Screenshot (76).png" alt="" width="600" />

<br/>

Choose the Amazon Machine Image (AMI) that you want to use for your instance. This will typically be the operating system you want to use (Ubuntu).

<img src="./assets/Screenshot (77).png" alt="" width="600" />

<br/>

Configure additional details such as the key pair settings and security group (Network) settings.

<img src="./assets/Screenshot (78).png" alt="" width="600" />
<img src="./assets/Screenshot (79).png" alt="" width="600" />

<br/>

Review all settings and click the `Launch` button to create an instance.
Once your instance is launched, it can be connect using a remote desktop or SSH client and start configuring  software and applications.

<img src="./assets/Screenshot (82).png" alt="" width="600" />

<br/>

## 1.2 Adding Jenkins Port to AWS Instance
Select the `Jenkins` instance that you want to add Jenkins port to. Click on the `Security` tab in the details pane at the bottom of the screen. Under `Security details` menu click on the `Security group` link.

<img src="./assets/Screenshot (83).png" alt="" width="600" />

<br/>

Then under the `Inbound rules` tab Click on the `Edit inbound rules` button. 

Inside `Edit inbound rules` section Click on the `Add rule` button to create a new inbound rule.

Select `Custom TCP` rule from the `Type` dropdown menu and enter `8080` as the `Port range`. Then Select `Anywhere` (or a specific IP range) as the `Source` to allow access from any IP address or a specific range of IP addresses.
Finally, click on the `Save rules` button to apply the changes.

<img src="./assets/Screenshot (84).png" alt="" width="600" />
<img src="./assets/Screenshot (85).png" alt="" width="600" />

<br/>
<br/>

# 2. Installing Jenkins on AWS Ubuntu Server

## 2.1 Installing Jenkins
First, update the default Ubuntu packages lists for upgrades with the following command:
```bash
sudo apt update
```
Then, run the following command to install JDK:
```bash
sudo apt install default-jdk -y
```
Now, we will install Jenkins itself. Issue the following four commands in sequence to initiate the installation from the Jenkins repository:
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update

sudo apt install jenkins -y
```
<br/>

## 2.2 Setting Up Jenkins
When the Jenkins has been installed on the Ubuntu, next step is to make the Jenkins enable using the systemctl command:
```bash
sudo systemctl enable jenkins
```
![](./assets/Screenshot%20(92).png)

<br/>

Once that’s done, start the Jenkins service with the following command:
```bash
sudo systemctl start jenkins
```
![](./assets/Screenshot%20(94).png)

<br/>

To confirm its status, use:
```bash
sudo systemctl status jenkins
```
![](./assets/Screenshot%20(95).png)

<br/>

## 2.3 Allowing Jenkins Port [8080]
With Jenkins installed, we can proceed with adjusting the firewall settings. By default, Jenkins will run on port 8080.

In order to ensure that this port is accessible, we will need to configure the built-in Ubuntu firewall (ufw). To open the 8080 port and enable the firewall, use the following commands:
```bash
sudo ufw allow 8080
```
![](./assets/Screenshot%20(97).png)

<br/>

Then we will enable the UFW(Ubuntu Firewall) service:
```bash
sudo ufw enable
```
![](./assets/Screenshot%20(98).png)

<br/>

Once done, test whether the firewall is active using this command:
```bash
sudo ufw status
```
![](./assets/Screenshot%20(99).png)

<br/>

With the firewall configured, it’s time to set up Jenkins itself. Type in the IP of your EC2 along with the port number. The Jenkins setup wizard will open.

<br/>

## 2.4 Jenkins Credentials
To check the initial password, use the cat command as indicated below:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

All Set! You can now start automating...
