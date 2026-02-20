---
id: precall
name: Precall Export
version: 0.1
---
# Purpose
Export upcoming customer engagement data for precall readiness into an Excel report and generate an email draft with a schedule update.

# When to use
- Asked to export engagements or generate a precall engagement report
- Asked to send a precall engagement update to a manager

# Preconditions
- Access to WorkIQ with upcoming engagement data
- Scratch directory available at `docs/processes/precall/scratch/`
- Export script available at `docs/processes/precall/exports/engagement_export.py`
- Write access to `docs/processes/precall/exports/`

# Steps
1) steps/01-gather-engagement-data.md
2) steps/02-build-json-data.md
3) steps/03-run-export-script.md
4) steps/04-report-results.md

# Quality gates
- ../../blocks/rubrics/quality-gate.md

# Output format
- Must produce: outputs/output-contract.md (and any deliverables listed therein)
