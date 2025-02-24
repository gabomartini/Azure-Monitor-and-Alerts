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
 5. Use Azure Monitor log queries.

## Task 1: Set up an alert using Azure Monitor.
In this task, you create an alert for when a virtual machine is deleted.

1.	In the Azure portal, search for and select "Monitor".
2.	Select "View" in the VM Insights box, and then select "Configure Insights".
3.	Select your virtual machine, and then "Enable" (twice).

<p align="center">
<img src="https://github.com/user-attachments/assets/09a2460f-9af1-49bd-92ff-edb7aa7ad823">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/1bf9ed4c-65a1-4447-84f7-5126999ddbc5">
</p>

4.	Use your desired subscription and data collection rules, then select "Configure". It will take a few minutes for the virtual machine agent to install and configure.

<p align="center">
<img src="https://github.com/user-attachments/assets/4c9c317d-a5a2-4f5a-9def-6dc5f1ecc1fc">
</p>

5.	Continue on the Monitor page , select "Alerts". Select "Create +" and select "Alert rule".
6.	Select the box for the resource group, then select Apply. This alert will apply to any virtual machines in the resource group. Alternatively, you could just specify one particular machine.
7.	Select the Condition tab and then select the "See all signals" link. Search for and select "Delete Virtual Machine (Virtual Machines)" and Select "Apply".

<p align="center">
<img src="https://github.com/user-attachments/assets/b1696df6-0fcd-4d44-a6ea-f6ef1d6a794a">
</p>

8.	In the Alert logic area (scroll down), review the Event level selections and the Status selections.

<p align="center">
<img src="https://github.com/user-attachments/assets/d4f1fe73-5a57-459a-9373-a1fca215375f">
</p>

## Task 2: Configure notifications for an action group.
In this task, when the alert is triggered, the configuration will send an email notification to the operations team.

1.	In the Create an alert rule pane select "Next: Actions >", choose Use action groups then "+ Create" action group. You can add up to five action groups to an alert rule.

<p align="center">
<img src="https://github.com/user-attachments/assets/d1444a1b-8ecb-4dac-82e8-4df23ecfaccd">
</p>

2.	On the Basics tab, configure Subscription, Resource group, Action group name (in this case "Alert the operations team"), and Display name (in this case "AlertOpsTeam"), then click "Next: Notifications >" and set Notification type (here we reach the team via Email) and Name (this will be the title of the message). The group should receive an email notification saying they were added to an action group. 

<p align="center">
<img src="https://github.com/user-attachments/assets/5906e7ae-d47f-4d2d-9657-cbc190c7f4ed">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/b8ac33cd-415d-4943-9643-6cd3ac527a83">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/0cf798b8-ec7b-4737-8b94-969c0e7b9f19">
</p>

3.	Select "Review + create" then "Create". Once the action group is created move to the "Next: Details >" tab and enter the following values for each setting: Alert rule name	"VM was deleted" and Alert rule description	"A VM in your resource group was deleted"

<p align="center">
<img src="https://github.com/user-attachments/assets/e79e2bb5-fda2-40a5-9994-80742019c521">
</p>

4.	Select "Review + create" to validate our input, then select "Create".

## Task 3: Trigger and validate an alert.
In this task, we trigger the alert and confirm a notification is sent.

1.  In the Azure portal, search for and select "Virtual machines".
2.	Check the box for a virtual machine in the resource group configured for the alert.
3.	Select Delete from the menu bar. Check the box for Apply force delete. Check the box at the bottom confirming that you want the resources to be deleted and select Delete.

<p align="center">
<img src="https://github.com/user-attachments/assets/ddca69fa-c19a-4759-a0c3-8846cc0568b9">
</p>

4.	In the title bar, select the Notifications icon and wait until the Virtual Machine is successfully deleted.
5.	The Operations Group should receive a notification email that reads, Important notice: Azure Monitor alert VM was deleted was activated.

<p align="center">
<img src="https://github.com/user-attachments/assets/0f5c1611-55c3-4546-a6dd-94077cc5b1d0">
</p>

6.	On the Azure portal resource menu, select Monitor, and then select Alerts in the menu on the left.
7.	We should have three verbose alerts that were generated by deleting the Virtual Machine. Note: It can take a few minutes for the alert email to be sent and for the alerts to be updated in the portal.

<p align="center">
<img src="https://github.com/user-attachments/assets/fd789c61-d756-4204-9717-55d32d6d0997">
</p>

## Task 4: Set up an alert processing rule.
In this task, we create an alert rule to suppress notifications during a maintenance period.

1.	Continue in the Alerts blade, click "+ Create" and select "Alert processing rules".
2.	Select your Resource group then select "Apply".
3.	Select "Next: Rule settings >", then select "Suppress notifications". Select "Next: Scheduling >".

<p align="center">
<img src="https://github.com/user-attachments/assets/bee6d5f1-6f84-47c1-9b50-5d18a1612bab">
</p>

4.	By default, the rule works all the time, unless we disable it or configure a schedule. We are going to define a rule to suppress notifications during overnight maintenance. We will enter the following settings for the scheduling of the alert processing rule:

<p align="center">
<img src="https://github.com/user-attachments/assets/4ea3dc08-955f-4ba7-b8b1-d31954542207">
</p>

5.	Select "Next: Details >" and enter these settings after Suscription and Resource Group: Rule name	"Planned Maintenance" and Description	"Suppress notifications during planned maintenance.".

<p align="center">
<img src="https://github.com/user-attachments/assets/45ed3a6c-d6fe-43c5-997f-d4c3462010a6">
</p>

6.	Select "Review + create" to validate your input, then select "Create".

## Task 5: Use Azure Monitor log queries.
In this task, you will use Azure Monitor to query the data captured from the virtual machine.

1.	In the Azure portal, search for and select Monitor blade, click Logs.
2.	If necessary close the splash screen.
3.	Select a scope, your Resource group, AZ-104-Module11 then select Apply.
4.	In the Queries tab, select Virtual machines (left pane).
5.	Review the queries that are available. Run (hover over the query) the Count heartbeats query.
6.	You should receive a heartbeat count for when the virtual machine was running.
7.	Review the query. This query uses the heartbeat table.
8.	Replace the query with this one, and then click Run. Review the resulting chart.
9.	 InsightsMetrics
10.	 | where TimeGenerated > ago(1h)
11.	 | where Name == "UtilizationPercentage"
12.	 | summarize avg(Val) by bin(TimeGenerated, 5m), Computer //split up by computer
13.	 | render timechart
14.	As you have time, review and run other queries.











