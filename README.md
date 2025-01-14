# Active Directory with Splunk (SIEM) Integration Project

![Screenshot 2024-10-02 175634](https://github.com/user-attachments/assets/74cf95f2-ba5c-475a-b7ec-d1c1123a2721)


## Objective
The project involved setting up an Active Directory environment, integrating it with **Splunk** for SIEM capabilities, and detecting brute force attacks using various hacking tools. The goal was to simulate real-world cybersecurity scenarios and monitor suspicious activities within the network. This project also connected directly to the **MITRE ATT&CK** framework, aligning attack techniques observed in Splunk with the framework’s categorization, allowing for a better understanding of adversary tactics and techniques.

### Skills Learned
- Active Directory configuration and management.
- SIEM integration and analysis with Splunk.
- Attack detection and investigation.
- Log analysis and event monitoring.
- Cyber threat hunting using the **MITRE ATT&CK** framework.

### Tools Used
- **Windows Server 2022**: Domain controller and Active Directory management.
- **Windows 10**: Client machine joined to the domain.
- **Kali Linux**: Offensive machine for testing attacks.
- **Splunk**: SIEM tool used for monitoring and logging activities.
- **Crowbar**: Brute-force attack tool.
- **Atomic Red Team**: For simulating adversary techniques.
- **Sysmon**: For monitoring system activities and logging.
- **MITRE ATT&CK Framework**: Used for identifying and categorizing attack techniques.

## Steps

### Step 1: Active Directory Setup
Configured Active Directory Domain Services (ADDS) on a Windows Server 2022 machine. Created organizational units, users, and groups for domain management.

*Ref 1: Active Directory Setup Screenshot*

<img width="511" alt="server manager OU" src="https://github.com/user-attachments/assets/1e39c401-173e-488f-88e9-a48a97249a35">


### Step 2: Windows 10 Domain Join
Installed and configured Windows 10, then joined it to the Active Directory domain created on Windows Server.

*Ref 2: Windows 10 Domain Join Screenshot*

![Screenshot 2024-10-02 173630](https://github.com/user-attachments/assets/5bca87d2-333c-4dc1-bc52-b98713e8146c)


### Step 3: Sysmon and Splunk Setup
Installed Sysmon on Windows machines for logging system activities. Configured Splunk to index and monitor logs from the Windows machine, specifically targeting logs generated by Sysmon.

*Ref 3: Sysmon and Splunk Configuration Screenshot*

![Screenshot 2024-10-07 205800](https://github.com/user-attachments/assets/554b6cde-7e37-4775-8606-4864a17c6e11)


### Step 4: Attack Simulation with Crowbar

Installed Crowbar on Kali Linux to perform a brute force attack on the Windows machines using RDP. Captured both failed and successful login attempts in Splunk.

- *Ref 4: Crowbar Command Execution on Kali Linux*  
   This screenshot shows the terminal window on Kali Linux where the Crowbar brute force attack is being executed, targeting the Windows machine via RDP.

   ![Screenshot 2024-10-18 211846](https://github.com/user-attachments/assets/825a61d2-3732-46bc-b335-95d540ae369f)

- *Ref 5: Failed Login Attempts on Windows*  
   This screenshot captures the failed login attempts on the target Windows machine, showcasing the login screen after Crowbar has made several unsuccessful attempts.

   ![Screenshot 2024-10-02 191037](https://github.com/user-attachments/assets/393cfc33-9be4-4699-b807-4cd456477ee7)

   - **Event ID 4625**: This event is generated when a login attempt fails. It provides information about the account that was used, the source IP address, and the reason for the failure.

- *Ref 6: Successful Login on Windows*  
   This screenshot shows the successful login after the brute force attack successfully guessed the credentials, confirming the breach of the Windows machine.

   ![Screenshot 2024-10-02 190857](https://github.com/user-attachments/assets/1a90ff57-cafc-4ed1-8d69-63bcc779557c)

   - **Event ID 4624**: This event is generated when a login attempt is successful. It details the account that logged in, the source IP address, and the logon type used (e.g., interactive, remote).

### Step 5: Adversary Simulation with Atomic Red Team

Used Atomic Red Team to simulate additional attack techniques on the Windows machine. These simulations included various adversary tactics, such as creating an uncloseable pop-up window to emulate real-world malware behavior. The generated logs were captured in Splunk, where they were analyzed and mapped to relevant techniques from the MITRE ATT&CK framework.

*Ref 7: Atomic Red Team Simulation of Uncloseable Pop-up Window*

  ![Screenshot 2024-10-02 202809](https://github.com/user-attachments/assets/87c42125-88be-4259-8949-39f06f591fe6)

*Ref 8: Atomic Red Team Simulation of Process Execution (Sysmon Log)*
 
  ![process](https://github.com/user-attachments/assets/8b381d00-8c15-4066-b22e-78de9abe6e5c)

 ### Detection Rule Viability
  While developing a detection rule for **T1083** can enhance visibility into file and directory access patterns, it may also generate false positives due to legitimate user activity.

  **Recommendation:**
  - **Start with a Baseline:** Before fully deploying a detection rule, analyze normal user behavior in your environment. Identify what file and directory access looks like during regular operations.
  - **Implement with Caution:** Consider creating a detection rule, but implement it with a threshold or conditions to minimize false positives. Monitor its effectiveness and adjust as needed based on your environment's unique characteristics.
  - **Test the Rule:** Run the detection in a test environment or in monitoring mode to see how many legitimate activities trigger it before rolling it out fully.


## Conclusion
This project provided hands-on experience in configuring Active Directory, integrating with a SIEM tool (Splunk), and detecting real-world attack simulations. By monitoring and analyzing logs in Splunk, I was able to detect brute-force attacks and map them back to MITRE ATT&CK techniques for further investigation.
