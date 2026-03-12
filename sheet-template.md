# Google Sheet Template Structure

## Sheet Name
`Garson Team RE Tracking`

## Tabs

### 1. Form Responses (Auto-generated)
This tab is automatically created when you link a Google Form. Contains raw form submissions.

### 2. Showings Log
The main processed database of all showings.

| Column | Description |
|--------|-------------|
| A: Timestamp | When the form was submitted |
| B: Processed | When the Lindy agent processed it |
| C: Property Address | Full address |
| D: Showing Date | Date of showing |
| E: Showing Time | Time of showing |
| F: Buyer's Agent Name | Agent name |
| G: Buyer's Agent Phone | Phone number |
| H: Buyer's Agent Email | Email address |
| I: Brokerage | Agent's brokerage |
| J: Buyer Profile | Description of buyer |
| K: Feedback | Buyer feedback |
| L: Objections | Concerns/objections |
| M: Outcome | Outcome status |
| N: Follow-up Needed | Follow-up items |
| O: Notes | Additional notes |
| P: Submitted By | Team member |
| Q: Status | Processing status (New/Processed/Action Needed) |

**Header Row Formatting**:
- Bold
- Background: #4285F4 (Google Blue)
- Text: White
- Freeze row 1

### 3. By Listing
Filtered view grouped by property address.

| Column | Description |
|--------|-------------|
| A: Property Address | Address (grouped) |
| B: Total Showings | Count of showings |
| C: Date Range | First showing - Last showing |
| D: Outcomes Summary | Count by outcome type |
| E: Common Feedback | Most mentioned positive points |
| F: Common Objections | Most mentioned concerns |
| G: Hot Leads | Agents showing strong interest |

### 4. Agent Directory
Master list of all buyer's agents encountered.

| Column | Description |
|--------|-------------|
| A: Agent Name | Full name |
| B: Phone | Phone number |
| C: Email | Email address |
| D: Brokerage | Company |
| E: First Contact | Date of first showing |
| F: Last Contact | Date of most recent showing |
| G: Showings Count | Total number of showings |
| H: Properties Shown | List of properties they've seen |
| I: Notes | Any notes about this agent |
| J: Relationship Status | Cold/Warm/Active/VIP |

### 5. Objections Analysis
Track patterns in buyer objections.

| Column | Description |
|--------|-------------|
| A: Objection Category | Type (Price, Location, Size, Condition, etc.) |
| B: Specific Objection | Detailed objection |
| C: Frequency | How often mentioned |
| D: Properties Affected | Which listings |
| E: Actionable | Yes/No - can we address this? |
| F: Resolution | What was done / suggested fix |

### 6. Dashboard (Optional)
Summary metrics and charts.

**Key Metrics**:
- Total Showings (All Time)
- Showings This Week/Month
- Active Listings
- Hot Leads Count
- Top Agents by Activity
- Most Common Objections

## Conditional Formatting Rules

### Showings Log
1. **Hot Lead Highlight**
   - Condition: Outcome = "Making Offer" OR "Very Interested - Likely Offer"
   - Format: Background #B7E1CD (light green)

2. **Needs Follow-up**
   - Condition: Follow-up Needed is not empty
   - Format: Background #FCE8B2 (light yellow)

3. **New/Unprocessed**
   - Condition: Status = "New"
   - Format: Bold text

### Agent Directory
1. **VIP Agents**
   - Condition: Showings Count >= 5 OR Relationship Status = "VIP"
   - Format: Background #B7E1CD (light green)

## Data Validation

### Outcome Dropdown
```
Very Interested - Likely Offer
Interested - Want to See Again
Lukewarm - Keeping Options Open
Not Interested
Making Offer
Needs Follow-up
```

### Status Dropdown
```
New
Processed
Action Needed
Archived
```

### Relationship Status Dropdown
```
Cold
Warm
Active
VIP
```

## Named Ranges (for formulas/Lindy)

- `ShowingsData` → Showings Log!A2:Q1000
- `AgentDirectory` → Agent Directory!A2:J500
- `PropertyList` → Unique property addresses
- `AgentEmails` → Agent Directory!C2:C500

## Sample Formulas

### Showings Count per Property
```
=COUNTIF(ShowingsData[Property Address], A2)
```

### Days Since Last Showing
```
=DATEDIF(MAX(FILTER(ShowingsLog!D:D, ShowingsLog!C:C=A2)), TODAY(), "D")
```

### Agent Showing Count
```
=SUMPRODUCT((ShowingsLog!F:F=A2)*1)
```
