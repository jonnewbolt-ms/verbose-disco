# Step 02: Build the JSON data file

Use the staged scratch data to assemble the JSON schema below.

Write the final JSON file to:
`docs/processes/precall/exports/engagements_data.json`.

```json
{
  "engagements": [
    {
      "customer": "Customer Name",
      "topic": "Engagement Topic",
      "date": "YYYY-MM-DD",
      "duration": "X hours",
      "attendees": ["Person 1", "Person 2"],
      "internal_call": "Scheduled (date) | Not yet scheduled | None found",
      "customer_call": "Scheduled (date) | Not yet scheduled | None found",
      "agenda": "Present | Missing | High-level overview | Not applicable",
      "status": "In Progress | Scheduled | In Planning",
      "notes": "Any relevant notes"
    }
  ],
  "boss_name": "Tracey Cooley",
  "boss_email": "trcooley@microsoft.com",
  "author_name": "Bryan Roberts"
}
```
