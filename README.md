<h1>configure PfSense</h1>

<h2>Description</h2>
This guide will be a basic walk through of some of things I like to set up on a fresh instance of PfSense. Installing and configuring services will come in a later guide.
<br/>

<h2>Firewall</h2>
- <b>PfSense</b>

<h2>Program walk-through:</h2>

1. [First we will be setting up a new user and password just for security purposes.](https://docs.netgate.com/pfsense/en/latest/usermanager/users.html)
  - Navigate to System -> User Manager
  - Click on ADD
  - then ....

2. Second we will be setting up your subnet mask range for most 255.255.255.0 should be enough which will provide you with 253 useable IP's in your IP range
  - Select...
  - then ...

3. Next we will be setting up a private IP for your network which would range from (10.0.0.0 – 10.255.255.255) , (172.16.0.0 – 172.31.255.255) , (192.168.0.0 – 192.168.255.255)
  - Select...
  - then ...

4. Now we will be setting up extra subnets for added security and more control.
  - Select...
  - then ...

5. Now that we have some subnets built we will be providing the subnets internet access through some firewall rules.
  - Select...
  - then ...

6. We have officially configured your PfSense firewall!
