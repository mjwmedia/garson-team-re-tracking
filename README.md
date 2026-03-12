# Garson Team RE Showing Tracker

A streamlined system for tracking real estate showings, collecting buyer feedback, and building a database of agent contacts and property insights.

## Overview

After each showing, team members fill out a quick Google Form (60 seconds). A Lindy agent automatically processes each submission, logging it into a structured Google Sheet organized by listing and date.

## Components

1. **Google Form** - Mobile-friendly form for quick post-showing submissions
2. **Google Sheet** - Structured database of all showings and feedback
3. **Lindy Agent** - Automation that processes new submissions

## Form Fields

| Field | Type | Description |
|-------|------|-------------|
| Property Address | Text | Full address of the listing shown |
| Showing Date | Date | Date of the showing |
| Buyer's Agent Name | Text | Name of the buyer's agent |
| Buyer's Agent Phone | Phone | Contact number |
| Buyer's Agent Email | Email | Contact email |
| Buyer Profile | Long Text | Description of the buyer (first-time, investor, relocating, etc.) |
| Feedback | Long Text | Buyer's feedback on the property |
| Objections | Long Text | Any concerns or objections raised |
| Outcome | Dropdown | Interested / Not Interested / Making Offer / Needs Follow-up |
| Notes | Long Text | Additional notes |

## Google Sheet Structure

### Tab: Showings Log
All submissions in chronological order with columns matching form fields plus:
- Timestamp (auto-generated)
- Submitted By (if tracking multiple team members)

### Tab: By Listing
Pivot/filtered view grouped by property address

### Tab: Agent Directory
Running list of buyer's agents with contact info and showing count

### Tab: Objections Analysis
Aggregated view of common objections across listings

## What You Get

- ✅ Consolidated view of feedback per listing, ready to share with sellers
- ✅ Running log of which agents are active and worth following up with
- ✅ Pattern tracking on common objections across properties
- ✅ Everything in Google Sheets - easy to filter, sort, and reference

## Setup Instructions

### 1. Google Form
**Form URL (for submissions)**: https://docs.google.com/forms/d/e/1FAIpQLSd2AqWHq0_iYyWCPFkJK4_XdHX3FhlxEkvU8yVAQyPDmdSRDg/viewform
**Form Edit URL**: https://docs.google.com/forms/d/15zOW7viuMbLMH4ULe0UK5EtWzomC6WtSxeBvQ2tvN2U/edit

### 2. Google Sheet
**Sheet URL**: https://docs.google.com/spreadsheets/d/15fOCdIJzA_Mx-mar40sIV8mLevZjrEXqVM2RHBib9-Q/edit

### 3. Lindy Agent Setup

1. Go to [Lindy.ai](https://www.lindy.ai)
2. Create a new agent with the following configuration:
   - **Trigger**: Google Sheets - New Row Added
   - **Connected Sheet**: Link to the Showings Log sheet
   - **Actions**: 
     - Parse and validate the submission
     - Update the "By Listing" tab if new property
     - Update the "Agent Directory" tab
     - Optionally send a Slack/email notification for hot leads

See `lindy-agent-config.md` for detailed agent setup instructions.

## File Structure

```
garson-team-re-tracking/
├── README.md                 # This file
├── lindy-agent-config.md     # Detailed Lindy agent setup
├── form-fields.json          # Form field definitions (for reference)
└── sheet-template.md         # Sheet structure documentation
```

## Links

- **Google Form (Submit)**: https://docs.google.com/forms/d/e/1FAIpQLSd2AqWHq0_iYyWCPFkJK4_XdHX3FhlxEkvU8yVAQyPDmdSRDg/viewform
- **Google Form (Edit)**: https://docs.google.com/forms/d/15zOW7viuMbLMH4ULe0UK5EtWzomC6WtSxeBvQ2tvN2U/edit
- **Google Sheet**: https://docs.google.com/spreadsheets/d/15fOCdIJzA_Mx-mar40sIV8mLevZjrEXqVM2RHBib9-Q/edit
- **GitHub Repo**: https://github.com/mjwmedia/garson-team-re-tracking

---

Built for Garson Team by Swarm Digital
