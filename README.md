<p align="center">
  <img src="https://github.com/user-attachments/assets/57f98e45-f9f1-45a6-ab58-66869034326e" alt="azure-vms-svgrepo-com" width="150" height="auto">
  <h1 align="center">Using Azure Monitor, Alerts, and Log Analytics</h1>
</p>

#### *In this tutorial, we will:*
*- Leverage Azure Monitor.*

*- Set up Azure alerts.*

*- Perform queries with Log Analytics.*

*- Work with Network Watcher.*

#### Tasks:
 1. Set up an alert using Azure Monitor.
 2. Configure notifications for an action group.
 3. Trigger and validate an alert.
 4. Set up an alert processing rule.

## Task 1: Set up an alert using Azure Monitor.
1.	In the Azure portal, search for and select "Monitor".
2.	Select "View" in the VM Insights box, and then select "Configure Insights".
3.	Select your virtual machine, and then "Enable" (twice).

<p align="center">
<img src="https://github.com/user-attachments/assets/09a2460f-9af1-49bd-92ff-edb7aa7ad823">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/1bf9ed4c-65a1-4447-84f7-5126999ddbc5">
</p>

5.	Use your desired subscription and data collection rules, then select "Configure". It will take a few minutes for the virtual machine agent to install and configure.

<p align="center">
<img src="https://github.com/user-attachments/assets/4c9c317d-a5a2-4f5a-9def-6dc5f1ecc1fc">
</p>

6.	Continue on the Monitor page , select "Alerts". Select "Create +" and select "Alert rule".
7.	Select the box for the resource group, then select Apply. This alert will apply to any virtual machines in the resource group. Alternatively, you could just specify one particular machine.
8.	Select the Condition tab and then select the "See all signals" link. Search for and select Delete Virtual Machine (Virtual Machines) and Select "Apply".

<p align="center">
<img src="https://github.com/user-attachments/assets/b1696df6-0fcd-4d44-a6ea-f6ef1d6a794a">
</p>

12.	In the Alert logic area (scroll down), review the Event level selections and the Status selections. Leave the default of All selected.

<p align="center">
<img src="https://github.com/user-attachments/assets/d4f1fe73-5a57-459a-9373-a1fca215375f">
</p>







