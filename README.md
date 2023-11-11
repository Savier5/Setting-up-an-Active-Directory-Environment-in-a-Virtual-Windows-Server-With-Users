# Setting up an Active Directory Environment in a Virtual Windows Server With Users

This project employs VirtualBox for virtualization and Windows 10/Windows Server 2019 ISOs for VM foundation. After installation and configuration, it progresses through Active Directory setup, introducing components like a Remote Access Server (RAS), NAT, and a DHCP Server. PowerShell scripts facilitate user creation, and adjustments are made for internet browsing. The creation of a Windows 10 VM follows, with subsequent steps verifying DHCP leases and ensuring internet connectivity. The project concludes with exploration of the Windows 10 VM.

## Step 1: Download and Install VirtualBox
  1. Visit the VirtualBox download link in the description.
  2. Download the appropriate version for your operating system (Windows or Mac).
  3. Install VirtualBox.
  4. Download the VirtualBox Extension Pack after the installation.
## Step 2: Download Windows 10 and Windows Server 2019 ISOs
  1. Follow the link in the description to download Windows 10.
  2. Fill out the necessary information (language, version) and download the 64-bit ISO.
  3. Repeat the process for Windows Server 2019, selecting ISO format.
  4. Remember where you save both downloads.
## Step 3: Create Virtual Machines in VirtualBox
  1. Open VirtualBox and click "New" to create a new virtual machine.
  2. Name it (e.g., dc for domain controller), choose OS (Other, Windows 64-bit), and allocate RAM (e.g., 2GB).
  3. Create a virtual hard disk with default settings.
  4. Open settings, go to Advanced, enable bi-directional for clipboard and drag-and-drop.
  5. In System, adjust the processor settings (e.g., 4 cores).
  6. In Network, add a second adapter for internal networking.
  7. Start the virtual machine and select the Windows Server 2019 ISO to boot from.
## Step 4: Install Windows Server 2019
  1. Install Windows Server 2019 with the desired settings (Desktop Experience recommended).
  2. Configure network settings (one adapter for internet, one for internal).
  3. Install VirtualBox Guest Additions for better integration.
  4. Shut down and restart the virtual machine.
## Step 5: Configure Active Directory
  1. Open "Add Roles and Features" in Server Manager.
  2. Choose Active Directory Domain Services and install.
  3. Promote the server to a domain controller.
  4. Set up a new forest with a domain name (e.g., mydomain.com).
  5. Complete the installation and restart the server.
## Step 6: Create Domain Admin Account
  1. Log in using the new domain admin account created during the setup.
  2. Open Active Directory Users and Computers.
  3. Create an Organizational Unit (OU) for admins.
  4. Create a new user account for admin purposes.
  5. Make the user a member of the Domain Admins group.
## Step 7: Install Remote Access Server (RAS) and NAT
  1. Open "Add Roles and Features" again.
  2. Choose Remote Access and install Routing and Remote Access.
  3. Open Routing and Remote Access, configure NAT, and use the internet interface.
  4. Finish the configuration.
## Step 8: Set Up DHCP Server
  1. Open "Add Roles and Features" once more.
  2. Choose DHCP Server and install.
  3. Open DHCP Manager and configure a new scope.
  4. Set up the DHCP scope information for internal clients.
  5. Complete the DHCP server setup.
## Step 9: Run PowerShell Script to Create Users
  1. Use the provided link to download the PowerShell script for creating users.
  2. Disable Internet Explorer Enhanced Security on the domain controller.
  3. Execute the PowerShell script to create a batch of sample users in Active Directory.
## Step 10: Configure Internet Browsing on Domain Controller
  1. Disable Internet Explorer Enhanced Security on the domain controller.
  2. Modify the configuration to allow normal internet browsing.
## Step 11: Create Windows 10 Virtual Machine
  1. Open VirtualBox and create a new virtual machine for Windows 10.
  2. Configure settings, allocate resources, and set up an internal network adapter.
  3. Install Windows 10 using the ISO file.
  4. Complete the setup process.
## Step 12: Verify DHCP and Internet Connectivity on Windows 10
  1. Check DHCP lease on the domain controller for the Windows 10 virtual machine.
  2. Verify internet connectivity on the Windows 10 virtual machine by pinging external hosts.
## Step 13: Join Windows 10 to the Domain
  1. Change the Windows 10 computer name to match the network diagram.
  2. Join the Windows 10 virtual machine to the domain (mydomain.com).
  3. Use a domain user account to log in.
## Step 14: Check Active Directory and DHCP on Domain Controller
  1. Verify the creation of the computer account in Active Directory for the Windows 10 machine.
  2. Check the DHCP leases on the domain controller to confirm the assignment of an IP address to the Windows 10 machine.
## Step 15: Explore Windows 10 Virtual Machine
  1. Log in to the Windows 10 virtual machine using domain credentials.
  2. Check the system information to confirm domain membership.
  3. Explore the Windows 10 environment and ensure proper functionality.
