# Lindy Agent Configuration

This document provides step-by-step instructions for setting up the Lindy agent that processes showing feedback submissions.

## Agent Overview

**Name**: Garson Team Showing Processor  
**Purpose**: Automatically process new showing feedback submissions and maintain organized databases

## Setup Steps

### 1. Create New Lindy Agent

1. Log into [Lindy.ai](https://www.lindy.ai)
2. Click "Create New Agent"
3. Name it: `Garson Team Showing Processor`

### 2. Configure Trigger

**Trigger Type**: Google Sheets - New Row Added

**Settings**:
- Connect your Google account
- Select the "Garson Team RE Tracking" spreadsheet
- Select the "Form Responses" tab (this is where Google Form responses land)
- Trigger on: Every new row

### 3. Define Agent Instructions

Copy this prompt into the agent instructions:

```
You are a real estate showing feedback processor for the Garson Team.

When a new showing feedback form is submitted, you should:

1. VALIDATE the submission:
   - Ensure Property Address is filled
   - Ensure Showing Date is valid
   - Ensure at least one contact method for buyer's agent

2. UPDATE the "Showings Log" tab:
   - Copy the form response to this tab with proper formatting
   - Add a processed timestamp

3. UPDATE the "Agent Directory" tab:
   - Check if this buyer's agent already exists (by email or phone)
   - If new agent: Add a new row with their info and set "Showings Count" to 1
   - If existing agent: Increment their "Showings Count" by 1

4. UPDATE the "By Listing" tab:
   - Add this showing under the appropriate property address section
   - If this is a new property, create a new section for it

5. ANALYZE for hot leads:
   - If Outcome = "Making Offer" → Flag as priority
   - If Outcome = "Interested" and feedback is positive → Flag as warm lead

6. RESPOND with a summary:
   - Confirmation that the showing was logged
   - Any flags or notes (hot lead, missing info, etc.)
```

### 4. Connect Actions

Add these actions to your agent:

#### Action 1: Read New Form Response
- Type: Google Sheets - Read Row
- Sheet: Form Responses tab
- Row: Trigger row

#### Action 2: Append to Showings Log
- Type: Google Sheets - Append Row
- Sheet: Showings Log tab
- Values: Mapped from form response + processed timestamp

#### Action 3: Update Agent Directory
- Type: Google Sheets - Search & Update or Append
- Sheet: Agent Directory tab
- Search by: Agent Email or Phone
- If found: Increment Showings Count
- If not found: Append new row

#### Action 4: Conditional Notification (Optional)
- Type: Slack/Email
- Condition: If Outcome = "Making Offer"
- Message: "🔥 Hot Lead Alert: [Property Address] - [Agent Name] is making an offer!"

### 5. Test the Agent

1. Submit a test entry through the Google Form
2. Verify the agent triggers
3. Check all tabs are updated correctly
4. Adjust as needed

## Webhook Alternative

If you prefer webhook-based triggers instead of polling:

1. In Google Forms, go to Responses → Three dots → Select response destination
2. Link to your Google Sheet
3. In Google Sheets, go to Extensions → Apps Script
4. Add this script:

```javascript
function onFormSubmit(e) {
  const webhookUrl = 'YOUR_LINDY_WEBHOOK_URL';
  
  const payload = {
    timestamp: new Date().toISOString(),
    values: e.values,
    namedValues: e.namedValues
  };
  
  UrlFetchApp.fetch(webhookUrl, {
    method: 'post',
    contentType: 'application/json',
    payload: JSON.stringify(payload)
  });
}
```

5. Set up a trigger: Edit → Current project's triggers → Add trigger
   - Function: onFormSubmit
   - Event type: On form submit

## Maintenance

- Review agent logs weekly for any failed processing
- Update agent instructions if form fields change
- Monitor the Agent Directory for duplicate entries

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Agent not triggering | Check Google Sheets connection, verify trigger sheet |
| Duplicate entries | Add deduplication logic based on timestamp + property |
| Missing data | Update form to require critical fields |
