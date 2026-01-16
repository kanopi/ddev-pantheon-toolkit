# Troubleshooting

## Common Issues

### 1. "Error: Not authenticated with Terminus"

**Problem:** Commands fail because Terminus is not authenticated.

**Solution:**
```bash
ddev ssh
terminus auth:login
exit
```

Follow the prompts to authenticate with your Pantheon account.

---

### 2. "Failed to fetch sites from organization"

**Problem:** Unable to retrieve sites from the specified organization.

**Possible Causes & Solutions:**

**Verify organization name:**
```bash
ddev exec terminus org:list
```

**Check permissions:**
- Ensure you have access to the organization in the Pantheon dashboard
- Verify you're logged in with the correct account
- Confirm your account has organization-level permissions

**Re-authenticate:**
```bash
ddev ssh
terminus auth:login
exit
```

---

### 3. "No sites found using upstream"

**Problem:** When using `--upstream` flag, no sites are found.

**Possible Causes & Solutions:**

**Verify upstream ID:**
```bash
ddev find-upstreams my-organization
```

Make sure you're using the complete UUID from the output.

**Check for custom sites:**
- Some sites might not have an upstream (custom builds)
- These sites won't appear when filtering by upstream

**Try without filtering:**
```bash
ddev add-org my-organization supporting-agency
```

---

### 4. Commands not found after installation

**Problem:** After installing the add-on, commands are not available.

**Solution:**
```bash
ddev restart
```

**If issue persists:**
```bash
# Reinstall the add-on
ddev get kanopi/ddev-pantheon-toolkit
ddev restart
```

---

### 5. "Permission denied" errors

**Problem:** Script execution fails with permission errors.

**Solution:**
```bash
# Enter the DDEV container
ddev ssh

# Check script permissions
ls -la /usr/local/bin/

# If scripts aren't executable, reinstall
exit
ddev get kanopi/ddev-pantheon-toolkit
ddev restart
```

---

### 6. Slow performance with large organizations

**Problem:** Commands take a very long time to complete.

**This is expected behavior for large organizations.**

**Optimization tips:**

**Use upstream filtering:**
```bash
# Instead of processing all sites
ddev add-org \
  --upstream abc-123 \
  my-organization \
  supporting-agency
```

**Use verbose mode to monitor progress:**
```bash
ddev site-inventory --verbose --csv output.csv my-organization
```

**Run during off-hours:**
- API rate limits may affect performance during peak hours
- Consider running large operations during off-peak times

**Expected timings:**
- Small orgs (10-50 sites): 1-5 minutes
- Medium orgs (50-100 sites): 5-15 minutes
- Large orgs (100+ sites): 15+ minutes

---

### 7. CSV export file is empty or corrupted

**Problem:** Generated CSV files are empty or can't be opened.

**Solutions:**

**Check file path:**
```bash
# Verify the file was created
ls -lh filename.csv
```

**Check file contents:**
```bash
head filename.csv
```

**Verify write permissions:**
```bash
# Check current directory permissions
ls -ld .
```

**Try explicit path:**
```bash
ddev site-inventory --csv ~/site-inventory.csv my-organization
```

---

### 8. "API rate limit exceeded"

**Problem:** Commands fail due to Pantheon API rate limits.

**Solutions:**

**Wait and retry:**
- API rate limits reset after a period
- Wait 5-10 minutes and try again

**Process in smaller batches:**
```bash
# Use upstream filtering to process fewer sites
ddev add-org --upstream abc-123 my-organization supporting-agency
```

**Spread operations over time:**
- Don't run multiple heavy operations simultaneously
- Schedule large operations with time between them

---

## Logging and Debugging

### Log File Locations

Commands create detailed log files for troubleshooting:

**add-org logs:**
```bash
pantheon_org_update_YYYYMMDD_HHMMSS.log
```

**site-inventory logs:**
```bash
pantheon_site_inventory_YYYYMMDD_HHMMSS.log
```

### Viewing Log Files

```bash
# View entire log
cat pantheon_org_update_20240115_143022.log

# View last 50 lines
tail -50 pantheon_org_update_20240115_143022.log

# Search for errors
grep -i error pantheon_org_update_20240115_143022.log

# Search for specific site
grep "my-site" pantheon_org_update_20240115_143022.log
```

### Enable Verbose Mode

For real-time debugging, use the `--verbose` flag:

```bash
ddev add-org --verbose --csv output.csv my-organization supporting-agency
```

This provides:
- Real-time progress updates
- Detailed API response information
- Error messages with context
- Timing information

---

## Getting Help

### Before Opening an Issue

1. **Check log files** - Review the timestamped log file for your operation
2. **Try verbose mode** - Run the command with `--verbose` flag
3. **Verify authentication** - Re-authenticate with Terminus
4. **Check permissions** - Verify access in Pantheon dashboard
5. **Review CSV exports** - Look for patterns in the output

### Opening an Issue

When reporting issues, include:

1. **Command used** - Exact command with flags (redact sensitive info)
2. **Error message** - Complete error output
3. **Log file excerpt** - Relevant portions of the log file
4. **Environment details:**
   - DDEV version: `ddev version`
   - Terminus version: `ddev exec terminus --version`
   - Organization size (approximate number of sites)
5. **Expected vs actual behavior**

**GitHub Issues:** https://github.com/kanopi/ddev-pantheon-toolkit/issues

---

## Additional Resources

- **DDEV Documentation:** https://ddev.readthedocs.io
- **Terminus Documentation:** https://docs.pantheon.io/terminus
- **Pantheon API Documentation:** https://docs.pantheon.io/api
- **Pantheon Support:** https://docs.pantheon.io
