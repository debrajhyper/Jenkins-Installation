# 1. Setup AWS Ubuntu Server










# 2. Installing Jenkins on AWS Ubuntu Server

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
When the Jenkins has been installed on the Ubuntu, next step is to make the Jenkins enable using the systemctl command:
```bash
sudo systemctl enable jenkins
```
Once that’s done, start the Jenkins service with the following command:
```bash
sudo systemctl start jenkins
```
To confirm its status, use:
```bash
sudo systemctl status jenkins
```
With Jenkins installed, we can proceed with adjusting the firewall settings. By default, Jenkins will run on port 8080.

In order to ensure that this port is accessible, we will need to configure the built-in Ubuntu firewall (ufw). To open the 8080 port and enable the firewall, use the following commands:
```bash
sudo ufw allow 8080
```
Then we will enable the UFW(Ubuntu Firewall) service:
```bash
sudo ufw enable
```
Once done, test whether the firewall is active using this command:
```bash
sudo ufw status
```
With the firewall configured, it’s time to set up Jenkins itself. Type in the IP of your EC2 along with the port number. The Jenkins setup wizard will open.

To check the initial password, use the cat command as indicated below:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

All Set! You can now start automating...
