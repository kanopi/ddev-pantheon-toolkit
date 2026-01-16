# Example Workflows

## Workflow 1: Add supporting organization to ALL sites

This workflow adds a supporting organization to every site in your Pantheon organization.

```bash
# 1. Authenticate with Terminus (one-time setup)
ddev ssh
terminus auth:login
exit

# 2. Do a dry run first to see what would change
ddev add-org \
  --dry-run \
  --csv all_sites_dryrun.csv \
  --verbose \
  acme-corp \
  partner-agency

# 3. Review the CSV file and console output
cat all_sites_dryrun.csv

# 4. If everything looks good, run it for real
ddev add-org \
  --csv all_sites_update.csv \
  acme-corp \
  partner-agency

# 5. Check the results
cat all_sites_update.csv
```

---

## Workflow 2: Add supporting organization to sites with specific upstream

This workflow targets only sites using a particular upstream (e.g., Drupal 10 sites).

```bash
# 1. Authenticate with Terminus (one-time setup if not already done)
ddev ssh
terminus auth:login
exit

# 2. Find the upstream ID you want to target
ddev find-upstreams acme-corp
# Output shows Drupal 10 upstream: abc123-def456-789012

# 3. Do a dry run first to see what would change
ddev add-org \
  --dry-run \
  --upstream abc123-def456-789012 \
  --csv drupal10_sites_dryrun.csv \
  --verbose \
  acme-corp \
  partner-agency

# 4. Review the CSV file and console output
cat drupal10_sites_dryrun.csv

# 5. If everything looks good, run it for real
ddev add-org \
  --upstream abc123-def456-789012 \
  --csv drupal10_sites_update.csv \
  acme-corp \
  partner-agency

# 6. Check the results
cat drupal10_sites_update.csv
```

---

## Workflow 3: Generate comprehensive site inventory

This workflow creates a detailed inventory of all sites for reporting and analysis.

```bash
# 1. Authenticate with Terminus (if not already done)
ddev ssh
terminus auth:login
exit

# 2. Generate the inventory with verbose output
ddev site-inventory \
  --csv site-inventory.csv \
  --verbose \
  acme-corp

# 3. Review the inventory
cat site-inventory.csv

# 4. Open in spreadsheet application for analysis
# (Open site-inventory.csv in Excel, Google Sheets, etc.)
```

**Use Cases for Site Inventory:**
- Identify sites needing PHP or WordPress updates
- Find frozen sites requiring attention
- Audit site ownership
- Analyze plan distribution
- Track custom domain usage
- Generate reports for stakeholders

---

## Workflow 4: Audit team member access

This workflow helps you understand who has access to which sites across your organization.

```bash
# 1. Authenticate with Terminus (if not already done)
ddev ssh
terminus auth:login
exit

# 2. Generate the team member report
ddev find-people

# 3. Review the report
cat ~/site_list_people.csv

# 4. Open in spreadsheet application for analysis
# (Open ~/site_list_people.csv in Excel, Google Sheets, etc.)
```

**Use Cases for Team Member Reports:**
- Audit access across all sites
- Identify users with access to multiple sites
- Find sites where specific users have access
- Prepare for offboarding team members
- Review role assignments

---

## Workflow 5: Combined audit and update

This workflow combines inventory generation, team auditing, and supporting organization management.

```bash
# 1. Authenticate (if not already done)
ddev ssh
terminus auth:login
exit

# 2. Generate site inventory
ddev site-inventory --csv inventory.csv acme-corp

# 3. Generate team member report
ddev find-people

# 4. Find available upstreams
ddev find-upstreams acme-corp

# 5. Review all reports before making changes
cat inventory.csv
cat ~/site_list_people.csv

# 6. Add supporting organization with dry run
ddev add-org \
  --dry-run \
  --csv update_dryrun.csv \
  --verbose \
  acme-corp \
  partner-agency

# 7. Review dry run results
cat update_dryrun.csv

# 8. Execute actual update
ddev add-org \
  --csv update_results.csv \
  acme-corp \
  partner-agency

# 9. Verify results
cat update_results.csv
```

---

## Tips for All Workflows

1. **Always authenticate first** - Run `terminus auth:login` before any operations
2. **Use dry-run mode** - Test changes before applying them (when available)
3. **Enable verbose output** - Use `--verbose` to see detailed progress
4. **Export to CSV** - Use `--csv` for reporting and auditing
5. **Review log files** - Check timestamped log files for detailed operation history
6. **Work incrementally** - For large organizations, consider filtering by upstream
7. **Backup data** - Keep CSV exports for records and rollback reference
