# Steps to setup an instance in AWS (using EC2)

We will be using EC2 for this series of steps. As a starting point, this guide will cover all the steps you need to do from starting on the Console Home of AWS.

- Open EC2
- Find the Launch Instance button
- Give the instance a name, you can also add additional tags, which are comprised of a key-value pair
- Choose an Amazon Machine Image (Application and OS Images). There is a Quick Start section but you can also browse a whole array of OS images. Make sure to select the right architecture for what you want (Arm processors are, in short, a new version of 64-bit that uses new processors, making the experience better, but some tech has not reached support for it yet. For the architecture that is most likely to work with current tech, you should for now select 64-bit under x86)
- Choose an instance type (different versions can cost different amounts per hour, which also depends on your choice of OS. If you have been told to select a particular one, always pick that one)
- Select a key pair login (you can select no key pair, but this is not recommended as it isn't secure)
- Set up your network settings (You can select the VPC, Subnet and whether to auto-assign a public IP here, but you can also choose security groups. Security groups are a set of rules for a firewall that control what comes in and out of your instance connection-wise. You can create a security group, bearing in mind what connection type and ports you use, plus what IPs are allowed to connect - if something is sensitive you may wish to stop everything coming in. You can also select an existing security group, which is particularly useful if you have set up one in the past as you can re-use it here. There is also some advanced security rules, but we won't cover them here)
- Configure storage if you desire, but this isn't necessary in some instances and you can keep this as it is
- If you want you can check the advanced details, but this won't be covered here. Once you have checked that everything is ready to go, press "Launch instance"
- Now you can access it via the command line. Click on the instance's link and within this click the button "Connect"
- From here on, an SSH client example will be used. Open an ssh client and locate the folder that holds the private key you have (it should be related to the key pair you chose with the key pair login), this is usually the .ssh folder
- Once you have found the private key, ensure it is not public by running the command `chmod 400 "KeyHere.pem"
- Connect to the instance with the following: `ssh -i "KeyHere.pem" <Public DNS for instance here>`
- If you have done this for the first time, now just tell the computer you are fine connecting, then you are done! The instance is now running and you are viewing it via the command line
