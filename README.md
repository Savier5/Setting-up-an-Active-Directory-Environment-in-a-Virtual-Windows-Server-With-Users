# Setting up an Active Directory Environment in a Virtual Windows Server With Users

This project employs VirtualBox for virtualization and Windows 10/Windows Server 2022 ISOs for VM foundation. After installation and configuration, it progresses through Active Directory setup, introducing components like a Remote Access Server (RAS), NAT, and a DHCP Server. PowerShell scripts facilitate user creation, and adjustments are made for internet browsing. The creation of a Windows 10 VM follows, with subsequent steps verifying DHCP leases and ensuring internet connectivity.

<img width="1280" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/b410b9b5-bac6-4186-8915-5bd12797636c">


## Step 1: Download and Install VirtualBox
  1. Visit the VirtualBox website to download it: https://www.virtualbox.org/wiki/Downloads
  2. Download the appropriate version for your operating system (Windows or Mac).
  3. Install VirtualBox.
  4. Download the VirtualBox Extension Pack after the installation.
     ![image](https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/a1f1875d-708f-4f29-bdd8-e09c212be0af)
## Step 2: Download Windows 10 and Windows Server 2022 ISOs
  1. Follow the link to download Windows 10: https://www.microsoft.com/en-us/software-download/windows10#d2784474-fdb0-4e9d-9e47-5e88c0e053ec
  2. Fill out the necessary information (language, version) and download the 64-bit ISO.
  3. Repeat the process for Windows Server 2022, selecting ISO format: [https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
  4. Remember where you save both downloads.
## Step 3: Create Virtual Machines in VirtualBox
  1. Open VirtualBox and click "New" to create a new virtual machine.
  2. Name it (e.g., dc for domain controller), choose OS (Other, Windows 64-bit) (Note: check the **Skip Unattended Installation** checkbox, as this can cause issues if it's not checked), adjust the processor settings (e.g., 4 cores), and allocate RAM (e.g., 2GB).
  3. Create a virtual hard disk with default settings.
  4. Open settings, go to Advanced, enable bi-directional for clipboard and drag-and-drop.
  5. In Network, leave the first adapter as NAT and add a second adapter for internal networking.
  6. Start the virtual machine and select the Windows Server 2022 ISO to boot from.
## Step 4: Install Windows Server 2022
  1. Install Windows Server 2022 with the desired settings (any of the Desktop Experience is recommended). To log in, you might have to go to Input > Keyboard > Insert Ctrl-Alt-Del in VirtualBox.
  2. Go to **Devices** in VirtualBox and then click **Insert Guest Additions CD image...**
     <img width="513" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/07614fec-221e-4644-93c8-512f5bd7023e">
  3. Go to File Explorer, This PC, and open VirtualBox Guest Additions.
     <img width="513" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/393b6c23-b265-481a-9841-66da1679be34">
  4. Run VBoxWindowsAdditions-amd64 and follow the setup, clicking next.
  5. Shut down the virtual machine and restart the virtual machine from VirtualBox.
  6. Rename the adapters to correctly represent what they are (one adapter for the internet (Make sure this one is connected to the internet), one for internal (Having an IPv4 of 169.254....)).
     <img width="513" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/93d4f623-f59b-428e-a534-c5e41f2d40b5">
  7. Go to the Internal adapter and change the IPv4 IP address to this:
      ![image](https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/7543f18d-3837-4933-9a5f-c670c5474d7b)
  8. Rename the PC to DomainController.
  9. Shut down the virtual machine and restart the virtual machine from VirtualBox.
## Step 5: Configure Active Directory
  1. In Server Manager, open "Add Roles and Features" in Server Manager.
  2. Install Active Directory Domain Services in the Server Roles section.
  3. Promote the server to a domain controller.
     ![image](https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/4abc7c97-bb45-4faf-99ac-9e6e09f7344b)
  4. Set up a new forest with a domain name (e.g., mydomain.com).
  5. Uncheck the Create DNS delegation checkbox in the DNS Options section.
  6. Complete the installation and restart the server.
## Step 6: Create Domain Admin Account
  1. Login using the new domain admin account created during the setup.
  2. Open Active Directory Users and Computers.
  3. Create an Organizational Unit (OU) for admins.
  4. Create a new user account for admin purposes.
     <img width="513" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/80091505-477d-4d73-92d6-777649f1865d">
  5. Make the user a member of the Domain Admins group.
     <img width="585" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/3f38d820-2441-466f-8265-4d428ec9540c">

  6. In the VM, sign out and sign in as the admin account we just created to verify it works.
     <img width="585" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/721fcae8-28dd-4597-b425-f78ef2723d02">
  Next, we will install RAS and NAT so it is still in a private network but can connect to the internet.
## Step 7: Install Remote Access Server (RAS) and NAT
  1. In Server Manager, open "Add Roles and Features" again.
  2. Choose Remote Access in the Server Roles section and install Routing in the Role Services section.
  3. Open Routing and Remote Access.
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/754e36b5-beb0-440e-ae01-68f6db498e2f">
  4. Right-click the domain controller we created and click on **Configure and Enable Routing and Remote Access**.
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/0faa255c-bfef-44d0-b2f7-8b60a4be5232">
  5. Select **Network address translation (NAT)**, and make sure **Use this public interface to connect to the internet** radio button is selected. If not, then close all the Routing and Remote Access windows and reopen them again.
  6. When the radio button is selected, select the Internet adapter.
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/de58a563-50e3-484b-b133-ca1b9518a6e5">
  7. Finish the configuration.
  Next, we will configure DHCP for the users so they can access the internet.
## Step 8: Set Up DHCP Server
  1. Open "Add Roles and Features" once more.
  2. Choose DHCP Server in the Server Roles section and install.
  3. Open DHCP.                              
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/7c3a7200-eef3-476c-83e7-6b310aca1eca">
  4. Configure a new scope for IPv4.
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/af9541ed-ce9e-43d7-a9f0-b3a47e2e6deb">
  5. Set up the DHCP scope information for internal clients; we want to have about 100 devices for this project and set the Lease Duration to something like 8 days (This is how long the IP address will last until it is renewed).
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/f51aa288-efdc-46e3-a6a2-68b600ec9e58">
  6. Make sure **Yes, I want to configure these options now** and click next. Then, we want to set it to the domain controller IP address for the Router default gateway and make sure to click **Add**. Add it again on the next page (Domain Name and DNS Servers).
      <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/61d5ce92-5c15-4388-8742-12bce3d92f84">
  7. Complete the DHCP server setup.
  8. Go to the domain controller, right-click and click Authorize, and then do that again and click Refresh, which should make the IPv4 and IPv6 icons green.
      <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/b9b8e0a6-4045-48dc-bd90-f74d31e161ec">
## Step 9: Run PowerShell Script to Create Users
  1. Download the folder with the PowerShell script to create users and random users in a text file. You can do this by going to a web browser on the VM, opening the project's GitHub page, and downloading it. Extract the folder and put it on the desktop.
  2. Open Windows PowerShell ISE as an administrator and then open the script there. Take some time to read through the script; this script was provided with the help of joshmadakor1. It basically goes through the names in the name.txt file, adds them as a non-admin user in AD, and then sets all the user's passwords to "Password1". We just did that for this project, and it is not recommended that all users use the same user; each user should use a different password.
  3. In Powershell, type "Set-ExecutionPolicy Unrestricted" so we can run the script without restrictions.
  4. Go to File Explorer, find the path to the folder with the two files we downloaded, and copy the path. Then, type "cd " in the Powershell terminal and paste the path to set the script path there.
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/1fcae0dd-29ad-4b9d-bff2-2d8e6e1b5dc4">
  5. Execute the PowerShell script to create a batch of sample users in Active Directory. (Some users might be duplicates and might show errors for them when the script is running).
     <img width="586" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/45a8d040-a941-4dff-84e8-1d13dae0b11a">
  If you open Active Directory Users and Computers, open your domain, then open _USERS, you will see all the users we inputted into AD.
## Step 10: Create Windows 10 Virtual Machine
  1. Open VirtualBox and create a new virtual machine for Windows 10.
     <img width="617" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/72115e34-6d69-4fb4-a38d-560a98a40ae8">
  2. Configure settings, allocate resources and set up an internal network adapter for the first adapter.
  3. Install Windows 10 using the ISO file, and choose Windows 10 Pro if it is an option when setting up the VM, as we know that version can join domains.
  4. When asked, click on I don't have internet, Continue with limited setup and complete the setup process.
## Step 11: Join Windows 10 to the Domain
  1. Go to the Windows icon in the taskbar, right-click it, and open Systems. In there, scroll down or to the right side to find and open Rename this PC (advanced). Click on Change, then rename the computer name and select the Domain radio button, entering the domain (e.g., mydomain.com).
  2. Use a domain user account in AD to log in. The password will be the password we talked about previously (Password1). Then, you'll be asked to restart the VM.
     <img width="1280" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/448c2107-9013-4d95-a183-f8895284fb17">
## Step 12: Explore Windows 10 Virtual Machine
  1. Log in to the Windows 10 virtual machine using domain credentials.
     <img width="1280" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/221a661d-a73d-4423-a6c9-6528579c798b">
  2. Check the system information to confirm domain membership.
     <img width="1280" alt="image" src="https://github.com/Savier5/Setting-up-an-Active-Directory-Environment-in-a-Virtual-Windows-Server-With-Users/assets/55478673/cc06e331-5cd2-4eba-8aa5-c29589e3f8b3">
  3. Explore the Windows 10 environment and ensure proper functionality.

In this comprehensive project, you've successfully orchestrated the setup of a virtualized Windows Server environment, mastering key technologies along the way. Starting with VirtualBox installation and Windows OS downloads, you crafted virtual machines, installed Windows Server 2019, and configured Active Directory services. Your journey continued with essential tasks like creating domain admin accounts, installing Remote Access Server and NAT, setting up a DHCP server, and executing PowerShell scripts for user creation. Finally, you seamlessly integrated a Windows 10 client, ensuring DHCP, internet connectivity, and Active Directory functionality.
