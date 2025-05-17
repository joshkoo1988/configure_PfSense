# Configure pfSense

## Description
This guide provides a step-by-step walkthrough of the **initial setup and configuration** of a new pfSense firewall instance. It focuses on improving security, organizing network structure, and preparing the environment for more advanced configurations, which will be covered in future guides.


## Program Walk-through

### 1. Create a Dedicated Administrator Account

To enhance security, the default `admin` account should not be used for daily administration.

📘 [User Management Documentation](https://docs.netgate.com/pfsense/en/latest/usermanager/users.html)

- Navigate to `System` → `User Manager`
- Click on **Add**
- Fill in:
  - **Username**: something other than `admin`
  - **Password**: choose a strong, unique password
  - **Full name**: optional
- Under the **Group Membership** section, add this user to the **admins** group
- Click **Save**
- (Optional but recommended) Go back to `System` → `User Manager`, edit the default `admin` account, and disable it.

---

### 2. Set Subnet Mask

Your subnet determines how many devices can connect within a network. For most home or small business setups, a **/24** subnet (255.255.255.0) is sufficient.

- Navigate to `Interfaces` → `LAN`
- Scroll down to the **IPv4 Subnet mask**
- Select **24 (255.255.255.0)** from the dropdown
- Click **Save** and then **Apply Changes**

This provides you with **253 usable IP addresses** (254 minus the network and broadcast addresses).

---

### 3. Set Private IP Address Range

Next, assign your LAN interface a private IP from one of the reserved private IP ranges:
- `10.0.0.0 – 10.255.255.255`
- `172.16.0.0 – 172.31.255.255`
- `192.168.0.0 – 192.168.255.255`

The most common choice is `192.168.1.1/24`.

- Navigate to `Interfaces` → `LAN`
- Set **IPv4 Configuration Type** to **Static IP**
- Set the **IPv4 Address** to `192.168.1.1`
- Ensure **Subnet mask** is set to `/24`
- Click **Save** and then **Apply Changes**

---

### 4. Create Additional Subnets (Optional but Recommended)

For better segmentation and security (e.g., IoT devices, guest WiFi), you can create multiple VLANs or subnets.

Example: Create a Guest subnet using `192.168.50.1/24`.

- Navigate to `Interfaces` → `Assignments`
- Click on the **+ Add** button to add a new interface
- Assign it to a VLAN or OPT port (e.g., `OPT1`)
- Click the new interface (e.g., `OPT1`) to configure it
- Enable the interface
- Set IPv4 Configuration Type to **Static IP**
- Assign a private IP (e.g., `192.168.50.1/24`)
- Click **Save** and then **Apply Changes**

Repeat as needed for additional networks (IoT, Cameras, etc.).

---

### 5. Set Up Firewall Rules for Subnets

Now that your subnets are defined, we need to give them access to the internet while maintaining separation.

- Navigate to `Firewall` → `Rules`
- Select the tab for your new interface (e.g., `OPT1`)
- Click **Add** to create a rule:
  - Action: **Pass**
  - Interface: `OPT1`
  - Protocol: **Any**
  - Source: `OPT1 subnet`
  - Destination: **Any**
- Scroll down and click **Save**
- Click **Apply Changes**

Repeat this for each subnet you want to allow internet access. For more control, you can define destination restrictions (e.g., allow only port 80/443).


