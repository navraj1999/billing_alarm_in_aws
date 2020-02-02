# billing_alarm_in_aws
Make sure you are using the AWS console in the us-east (north-virginia) region, as billing related Cloudwatch data is collected there. The SNS topic should be located there as well.
A small AWS console cheat: if you haven't created any alarms yet, than the console will provide a wizard which helps you to create exactly a total estimated charges alarm, and the SNS topic with an email subscription can be created by providing a single email in the dialog

But once you already have an alarm, the helper wizard will not be available and you have to perform 2 separate steps:

create an SNS topic, with an email endpoint
create a new alarm, and connect it with the SNS topic
First you have to create an SNS Topic which will deliver alarms as email:

Go to AWS SNS console
Select Topics / Create new topic
Fill Topic name and Display name with EmailMe
Click Create Topic
Click on the newly created topic ARN to see the details page
push Create Subscription
Protocol: Email
Endpoint: YourEmail@comes.here
Now you are ready to create the billing alarm


Go to AWS Cloudwatch console
Navigate to Alarms / Billing / Create Alarm
Select Total Estimated Charge from the billing category, click next
Select USD, click next
Fill Alarm Threshold name and description
Enter the limit you want to be checked, lets say 1000 USD
In the Actions subsection
choose State is ALARM
choose the previously created SNS: EmailMe
click Create Alarm
