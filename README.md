<p align="center">
  <img src="https://github.com/user-attachments/assets/ae3435ca-58c8-4850-9057-0060b38b2215" width="150" height="auto">
  <h1 align="center">Using Azure Monitor, Alerts, and Log Analytics</h1>
</p>

#### *In this tutorial, we will:*
*•	Leverage Azure Monitor to track resource activity.*

*•	Set up Azure alerts to notify teams of critical events.*

*•	Perform queries with Log Analytics to analyze data.*

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
<img src="https://github.com/user-attachments/assets/cd0802b7-8eca-428e-ab1f-155b6a1a2f34">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/5eb29510-871d-418b-aa0c-18b000ffe5fb">
</p>

4.	Use your desired subscription and data collection rules, then select "Configure". It will take a few minutes for the virtual machine agent to install and configure.

<p align="center">
<img src="https://github.com/user-attachments/assets/b5a7e2db-073f-4f10-8fe2-dbf1bae08d3a">
</p>

5.	Continue on the Monitor page , select "Alerts". Select "Create +" and select "Alert rule".
6.	Select the box for the resource group, then select Apply. This alert will apply to any virtual machines in the resource group. Alternatively, you could just specify one particular machine.
7.	Select the Condition tab and then select the "See all signals" link. Search for and select "Delete Virtual Machine (Virtual Machines)" and Select "Apply".

<p align="center">
<img src="https://github.com/user-attachments/assets/948ff32d-1e3a-4226-aca6-ea03ff0b4cbe">
</p>

8.	In the Alert logic area (scroll down), review the "Event level" and the "Status" selections.

<p align="center">
<img src="https://github.com/user-attachments/assets/9ed164e4-2e5c-4ff3-9683-b51a8ec8c417">
</p>

## Task 2: Configure notifications for an action group.
In this task, when the alert is triggered, the configuration will send an email notification to the operations team.

1.	In the Create an alert rule pane select "Next: Actions >", choose Use action groups then "+ Create" action group. You can add up to five action groups to an alert rule.

<p align="center">
<img src="https://github.com/user-attachments/assets/e75b8ff3-a62d-48bc-bda6-35e1b78c9821">
</p>

2.	On the Basics tab, configure Subscription, Resource group, Action group name (in this case "Alert the operations team"), and Display name (in this case "AlertOpsTeam"), then click "Next: Notifications >" and set Notification type (here we reach the team via Email) and Name (this will be the title of the message). The group should receive an email notification saying they were added to an action group. 

<p align="center">
<img src="https://github.com/user-attachments/assets/8c72d875-668c-4e5e-9a34-8d264d1f7877">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/dd2ca3e6-873c-4b73-8d70-1dacefbfa24d">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/0fa8244c-9773-4a38-ac4d-a809d129f3ab">
</p>

3.	Select "Review + create" then "Create". Once the action group is created move to the "Next: Details >" tab and enter the following values for each setting: Alert rule name	"VM was deleted" and Alert rule description	"A VM in your resource group was deleted"

<p align="center">
<img src="https://github.com/user-attachments/assets/d23e9b62-a213-4b2e-966f-b15a012e62bb">
</p>

4.	Select "Review + create" to validate our input, then select "Create".

## Task 3: Trigger and validate an alert.
In this task, we trigger the alert and confirm a notification is sent.

1.  In the Azure portal, search for and select "Virtual machines".
2.	Check the box for a virtual machine in the resource group configured for the alert.
3.	Select Delete from the menu bar. Check the box for Apply force delete. Check the box at the bottom confirming that you want the resources to be deleted and select Delete.

<p align="center">
<img src="https://github.com/user-attachments/assets/8e90a9df-5a59-4451-8c8c-6991a4a73e05">
</p>

4.	In the title bar, select the Notifications icon and wait until the Virtual Machine is successfully deleted.
5.	The Operations Group should receive a notification email stating: "Important notice: Azure Monitor alert VM was deleted was activated.".

<p align="center">
<img src="https://github.com/user-attachments/assets/a2203176-9598-4167-96c3-412bb0c5749a">
</p>

6.	On the Azure portal resource menu, select Monitor, and then select Alerts in the menu on the left.
7.	We should have three verbose alerts that were generated by deleting the Virtual Machine. Note: It can take a few minutes for the alert email to be sent and for the alerts to be updated in the portal.

<p align="center">
<img src="https://github.com/user-attachments/assets/282acef3-767f-42fb-983f-bf8fc454b078">
</p>

## Task 4: Set up an alert processing rule.
In this task, we create an alert rule to suppress notifications during a maintenance period.

1.	Continue in the Alerts blade, click "+ Create" and select "Alert processing rules".
2.	Select your Resource group then select "Apply".
3.	Select "Next: Rule settings >", then select "Suppress notifications". Select "Next: Scheduling >".

<p align="center">
<img src="https://github.com/user-attachments/assets/a9c691b5-dc5f-4b7e-abb6-1af51feed01a">
</p>

4.	By default, the rule runs continuously unless disabled or scheduled otherwise. We are going to define a rule to suppress notifications during overnight maintenance. We will enter the following settings for the scheduling of the alert processing rule:

<p align="center">
<img src="https://github.com/user-attachments/assets/6ac6c106-962e-4469-98c9-78bd5b5a6fd2">
</p>

5.	Select "Next: Details >" and enter these settings after Subscription and Resource Group: Rule name	"Planned Maintenance" and Description	"Suppress notifications during planned maintenance.".

<p align="center">
<img src="https://github.com/user-attachments/assets/17ee12c6-9a6d-41b5-8a33-8ff99b4576de">
</p>

6.	Select "Review + create" to validate your input, then select "Create".

## Task 5: Use Azure Monitor log queries.
In this task, you will use Azure Monitor to query the data captured from the virtual machine.

1.	In the Azure portal, search for and select Monitor blade, then click "Logs".
2.	Select a scope, your Resource group, and select "Apply".

<p align="center">
<img src="https://github.com/user-attachments/assets/605741fc-c6ec-436b-b752-1d16ca518554">
</p>

3.	In the Queries tab, select Virtual machines (left pane).
4.	Run (hover over the query) the Count heartbeats query.

<p align="center">
<img src="https://github.com/user-attachments/assets/7f9c64ba-c3e8-4939-8226-c906990a294c">
</p>

5.	You should receive a heartbeat count for when the virtual machine was running. This query uses the heartbeat table.

<p align="center">
<img src="https://github.com/user-attachments/assets/2f168857-27ed-4bef-a181-47538cc91a7b">
</p>

6.	Replace the query with the following one, then click 'Run'. Review the resulting chart.

InsightsMetrics

  | where TimeGenerated > ago(1h)

  | where Name == "UtilizationPercentage"

  | summarize avg(Val) by bin(TimeGenerated, 5m), Computer //split up by computer

  | render timechart

<p align="center">
<img src="https://github.com/user-attachments/assets/6af9acc1-aade-444f-95e0-36eae1738e86">
</p>
