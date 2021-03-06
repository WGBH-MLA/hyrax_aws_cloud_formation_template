# Hyrax AWS Cloud Formation Template
AWS Cloud Formation Templates for AMS (Archival Management System)

## Create a brand spankin new stack that can run AMS

Use the `ams.new_app.json` CloudFormation template. This will create a bunch of
AWS resources used to run AMS.

**NOTE: The stack costs $$$ when it's running so make sure you have approval
first!** When creating a new stack, AWS provides a cost estimate. Right now
(Dec 2020) it costs about $140/month.

### What you get

If successful, you'll have a fully functional stack of AWS resources capable of
running the AMS web app.

### Steps

1. Make sure you have the latest version of `ams.new_app.json` from this
   repository saved to your local machine.
1. Log into AWS Management Console.
1. Navigate to CloudFormation.
1. Click "Create stack" >> "With new resources".
1. Under "Prerequisite - Prepare template" select "Template is ready".
1. Under "Specify template" select "Upload a template file".
1. Click "Choose File" and select your local copy of `ams.new_app.json` from
   step 1, and then click "Next".
1. Enter a **Stack Name**, enter values for the parameters:
   1. All password fields are required.
   1. All other default values should work, but you can adjust them as needed.
   1. Click "Next" when finished.
1. For the "Configure stack options" and "Advanced options", defaults will
   suffice, but adjust as needed, and click "Next" when finished.
1. Review the stack details to make sure it's what you want. To go back, click
   the "Previous" button at the bottom.
1. If the stack looks good to go, check the checkbox labeled with
   "I acknowledge that AWS CloudFormation might create IAM resources."
1. Click "Create Stack". This will kick of an asynchronous process to build
   the stack. Check the "Events" tab to see the progress. When you see an event
   in the list whose "Logical ID" is your stack name, and the "Status" is
   "CREATE_COMPLETE", then the stack is ready.
1. Deploy Code
   1. In the AWS Management console, navigate to CodeDeploy.
   1. In the left menu, click "Applications".
   1. Click the AWS "Application" that was created with the CloudFormation
      template (it should be named the same as your stack).
   1. Click deployment group for the app (there should be only 1 and be named
      the same as the stack name, but with "-DG" suffix appended.
   1. Click the "Create Deployment" button.
   1. On the "Create Deployment" screen:
      1. Enter the deployment group that was created as part of the stack. It
         should be named the same as the stack, with a "-DG" suffix.
      1. Select the "My application is stored in Github" option.
      1. Enter the Github token name: 'jasoncorum'. (NOTE: if this stops
         working, we can connect another Github account).
      1. Enter the repository name: "wgbh-mla/ams".
      1. Enter the commit hash of the commit you want to deploy. **NOTE:
         Due to a branching convention we never truly followed, we do not
         currently use the `master` branch, but rather the the `develop` branch,
         thus we typically deploy the most recent commit from `develop`. This
         may change, so be sure to consult with developers if you are unsure
         which branch/commit represents the latest code.
      1. Add an optional description.
      1.

## Restore AWS stack using data from snapshot backups

Use the `ams.restore_from_backups.json` to restore the AMS

### What you get

If successful, you'll have a fully functioning AMS app with data rolled back
to the point-in-time that the snapshots were taken.

### Steps

1.
