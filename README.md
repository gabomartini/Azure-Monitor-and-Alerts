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

Create an alert in Azure Monitor to detect when a virtual machine (VM) is deleted within a resource group.

1.	In the Azure portal, search for and select "Monitor".
2.	In the "VM Insights" box, click "View", then click "Configure Insights".
3.	Select your virtual machine, then click "Enable" twice to activate VM Insights.

<p align="center">
<img src="https://github.com/user-attachments/assets/cd0802b7-8eca-428e-ab1f-155b6a1a2f34">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/5eb29510-871d-418b-aa0c-18b000ffe5fb">
</p>

4.	Choose your desired subscription and data collection rules, then click "Configure". (Note: It may take a few minutes for the VM agent to install and configure.)

<p align="center">
<img src="https://github.com/user-attachments/assets/b5a7e2db-073f-4f10-8fe2-dbf1bae08d3a">
</p>

5.	Return to the "Monitor" page and select "Alerts".
6.	Click "Create +" and select "Alert rule".
7.	In the "Scope" tab, check the box for your resource group, then click "Apply". (This applies the alert to all VMs in the resource group; alternatively, you can select a specific VM.)
8.	Click the "Condition" tab, then click "See all signals".
9.	Search for and select "Delete Virtual Machine (Virtual Machines)", then click "Apply".

<p align="center">
<img src="https://github.com/user-attachments/assets/948ff32d-1e3a-4226-aca6-ea03ff0b4cbe">
</p>

10.	In the "Alert logic" area (scroll down if needed), review the default settings for "Event level" and "Status". (These define the alert’s trigger conditions.)

<p align="center">
<img src="https://github.com/user-attachments/assets/9ed164e4-2e5c-4ff3-9683-b51a8ec8c417">
</p>

## Task 2: Configure notifications for an action group.

Configure an action group (a set of notification recipients and actions) to send an email to the operations team when the alert is triggered.

1.	In the "Create an alert rule" pane, click "Next: Actions >".
2.	Choose "Use action groups", then click "+ Create action group". (You can add up to five action groups per alert rule.)

<p align="center">
<img src="https://github.com/user-attachments/assets/e75b8ff3-a62d-48bc-bda6-35e1b78c9821">
</p>

3.	On the "Basics" tab, configure:
    -  Subscription: Select your subscription.
    -  Resource group: Choose your resource group.
    -  Action group name: Enter "Alert the operations team".
    -  Display name: Enter "AlertOpsTeam".
4.	Click "Next: Notifications >" and configure:
    -  Notification type: Select "Email/SMS message/Push/Voice" and choose "Email".
    -  Name: Enter a title for the message (e.g., "VM Deletion Alert").
5.	Enter the operations team’s email address, then click "OK". (The team will receive a confirmation email about being added to the action group.)

<p align="center">
<img src="https://github.com/user-attachments/assets/8c72d875-668c-4e5e-9a34-8d264d1f7877">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/dd2ca3e6-873c-4b73-8d70-1dacefbfa24d">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/0fa8244c-9773-4a38-ac4d-a809d129f3ab">
</p>

6.	Click "Review + create", then click "Create" to create the action group.
7.	Back in the "Create an alert rule" pane, click "Next: Details >" and configure:
    -  Alert rule name: Enter "VM was deleted".
    -  Alert rule description: Enter "A VM in your resource group was deleted".

<p align="center">
<img src="https://github.com/user-attachments/assets/d23e9b62-a213-4b2e-966f-b15a012e62bb">
</p>

8.	Click "Review + create" to validate the settings, then click "Create".

## Task 3: Trigger and validate an alert.

Trigger the alert by deleting a VM and confirm the operations team receives a notification.

1.	In the Azure portal, search for and select "Virtual machines".
2.	Check the box for a VM in the resource group configured for the alert.
3.	Click "Delete" from the menu bar.
4.	Check "Apply force delete" and the confirmation box at the bottom, then click "Delete".

<p align="center">
<img src="https://github.com/user-attachments/assets/8e90a9df-5a59-4451-8c8c-6991a4a73e05">
</p>

5.	In the title bar, click the "Notifications" icon and wait until the VM deletion succeeds.
6.	Verify the operations team receives an email with the message: "Important notice: Azure Monitor alert VM was deleted was activated."

<p align="center">
<img src="https://github.com/user-attachments/assets/a2203176-9598-4167-96c3-412bb0c5749a">
</p>

7.	From the Azure portal resource menu, select "Monitor", then click "Alerts" in the left menu.
8.	Confirm three verbose alerts were generated from the VM deletion. (Note: It may take a few minutes for the email to arrive and alerts to update in the portal.)

<p align="center">
<img src="https://github.com/user-attachments/assets/282acef3-767f-42fb-983f-bf8fc454b078">
</p>

## Task 4: Set up an alert processing rule.

Create an alert processing rule to suppress notifications during a maintenance period.

1.	In the "Alerts" blade, click "+ Create" and select "Alert processing rules".
2.	In the "Scope" tab, select your resource group, then click "Apply".
3.	Click "Next: Rule settings >", then check "Suppress notifications".
4.	Click "Next: Scheduling >".

<p align="center">
<img src="https://github.com/user-attachments/assets/a9c691b5-dc5f-4b7e-abb6-1af51feed01a">
</p>

5.	Define a schedule to suppress notifications during overnight maintenance (e.g., 12:00 AM to 6:00 AM daily):

<p align="center">
<img src="https://github.com/user-attachments/assets/6ac6c106-962e-4469-98c9-78bd5b5a6fd2">
</p>

6.	Click "Next: Details >" and configure:
    -  Subscription: Select your subscription.
    -  Resource group: Select your resource group.
    -  Rule name: Enter "Planned Maintenance".
    -  Description: Enter "Suppress notifications during planned maintenance."

<p align="center">
<img src="https://github.com/user-attachments/assets/17ee12c6-9a6d-41b5-8a33-8ff99b4576de">
</p>

7.	Click "Review + create" to validate the settings, then click "Create".

## Task 5: Use Azure Monitor log queries.

Use Log Analytics (a tool within Azure Monitor for querying log data) to analyze telemetry data from the virtual machine.

1.	In the Azure portal, search for and select "Monitor", then click "Logs".
2.	In the "Scope" picker, select your resource group, then click "Apply".

<p align="center">
<img src="https://github.com/user-attachments/assets/605741fc-c6ec-436b-b752-1d16ca518554">
</p>

3.	In the "Queries" tab, under "Virtual machines" in the left pane, locate the "Count heartbeats" query.
4.	Hover over the "Count heartbeats" query and click "Run". (This query counts heartbeats from the VM’s Heartbeat table, showing when it was active.)

<p align="center">
<img src="https://github.com/user-attachments/assets/7f9c64ba-c3e8-4939-8226-c906990a294c">
</p>

5.	Review the heartbeat count results.

<p align="center">
<img src="https://github.com/user-attachments/assets/2f168857-27ed-4bef-a181-47538cc91a7b">
</p>

6.	Replace the query with the following, then click "Run":

  InsightsMetrics
  
  | where TimeGenerated > ago(1h)
  
  | where Name == "UtilizationPercentage"
  
  | summarize avg(Val) by bin(TimeGenerated, 5m), Computer
  
  | render timechart

7.	Review the resulting time chart, which shows the average CPU utilization percentage over the past hour, split by computer, in 5-minute intervals.

<p align="center">
<img src="https://github.com/user-attachments/assets/6af9acc1-aade-444f-95e0-36eae1738e86">
</p>
