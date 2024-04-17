# Jamf Functions

This repository contains CloudFormation templates and Amazon States Language (ASL) files that will create resources in an AWS account to run scheduled and webhook-based automations from Jamf Pro. The examples in this project, and the base resources it creates, will then enable you to create _your own_ automations in template form or using AWS Step Functions Workflow Studio.

![AWS Step Functions Workflow Studio](images/workflow-studio.png)

## Base Resource Template

The base resources template at the root of this project creates resources in your AWS account that are required before you deploy any of the example workflows that are included.

- **API Gateway:** Jamf Pro needs an HTTP endpoint to send webhooks to. The API is created with a long randomized path value to obscure it from discovery (similar to how Slack's inbound webhooks work).
- **Event Bus:** This is a service in AWS that enables messages to be received and then delivered to one or more targets. There is a special logging rule included so a copy of _every_ webhook is saved in CloudWatch logs in case you need to troubleshoot.
- **API Connection:** This securely stores the client ID and secret for your Jamf Pro API client so the Step Functions can make authenticated requests to the Jamf Pro APIs. AWS handles all the token generation and management for you!

### Example Workflows

The workflows included with this project are based on published [Jamf Routines](https://learn.jamf.com/en-US/bundle/jamf-routines-documentation/page/jamf_workflow_automation.html). They are effectively Step Functions versions of those automations, and provide a good reference for writing your own.