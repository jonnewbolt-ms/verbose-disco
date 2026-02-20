# Step 03: Run the export script

Execute the Python export script:

```shell
python docs/processes/precall/exports/engagement_export.py --data docs/processes/precall/exports/engagements_data.json
```

Confirm that the script outputs files to `docs/processes/precall/exports/`:
- engagements_YYYY-MM-DD.xlsx
- engagement_update_YYYY-MM-DD.eml (or .msg if Outlook COM is available)
