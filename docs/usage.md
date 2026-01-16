# Usage Guide

## Discovering Team Members Across Sites

To generate a comprehensive CSV report of all team members across all your Pantheon sites:

```bash
ddev find-people
```

This command will:
1. Prompt you to authenticate with Terminus if needed
2. Retrieve a list of all sites you have access to
3. For each site, gather the team member list
4. Export the results to `~/site_list_people.csv`

The CSV file will be saved in your home directory with the following columns:
- **Site**: The Pantheon site name
- **Email**: Team member's email address
- **Role**: Their role on the site (admin, team, developer, etc.)

You can:
- View in terminal: `cat ~/site_list_people.csv`
- Open in Excel, Google Sheets, or any spreadsheet application
- Process with data analysis tools
- Filter and sort to find specific users or sites

## Generating Site Inventory Reports

To create a comprehensive inventory of all sites in your organization:

```bash
ddev site-inventory my-organization
```

This will output CSV data to stdout with the following columns:
- **Site Name**: The Pantheon site name
- **Upstream**: Upstream name (or UUID if name unavailable)
- **WordPress Version**: Core version for WordPress sites
- **PHP Version**: Current PHP version on the live environment
- **Public URL**: Custom domain (if configured) or platform domain
- **Pantheon Dashboard URL**: Direct link to site dashboard
- **Plan**: Current plan name
- **Status**: Active or Frozen
- **Created date**: When the site was created
- **Owner**: Email of the site owner

### Export to CSV File

To save the report to a file:

```bash
ddev site-inventory --csv site-inventory.csv my-organization
```

### Verbose Mode

For detailed logging during report generation:

```bash
ddev site-inventory --csv site-inventory.csv --verbose my-organization
```

You can then:
- Open the CSV in Excel, Google Sheets, or any spreadsheet application
- Filter by upstream to see all sites using specific frameworks
- Sort by plan to analyze your organization's site distribution
- Identify frozen sites that may need attention
- Track WordPress and PHP versions for upgrade planning
- Audit site ownership and access

## Managing Supporting Organizations

### Basic Usage - All Sites

By default, the command adds the supporting organization to **all sites** in your organization:

```bash
ddev add-org my-organization supporting-agency
```

### Filtering by Upstream

If you only want to add the supporting organization to sites using a specific upstream, first discover available upstreams:

```bash
ddev find-upstreams my-organization
```

This will output something like:
```
Upstream ID: 8a129104-9ae2-4700-8c23-c7d8f2b8a456
  Name: WordPress
  Framework: wordpress
  Sites using this upstream: 15
  Site list: site1, site2, site3...

Upstream ID: 7b234567-8901-2345-6789-abcdef123456
  Name: Drupal 9
  Framework: drupal9
  Sites using this upstream: 8
  Site list: site4, site5, site6...
```

Then use the `--upstream` flag to filter:

```bash
ddev add-org \
  --upstream 8a129104-9ae2-4700-8c23-c7d8f2b8a456 \
  my-organization \
  supporting-agency
```

### Dry Run Mode

Test what changes would be made without actually making them:

```bash
ddev add-org \
  --dry-run \
  --csv results.csv \
  --verbose \
  my-organization \
  supporting-agency
```

Or with upstream filtering:

```bash
ddev add-org \
  --dry-run \
  --upstream 8a129104-9ae2-4700-8c23-c7d8f2b8a456 \
  --csv results.csv \
  my-organization \
  supporting-agency
```

### Production Run with CSV Reporting

```bash
ddev add-org \
  --csv production_update.csv \
  my-organization \
  supporting-agency
```

## Getting Upstream IDs

### Method 1: Using the discovery command (recommended)
```bash
ddev find-upstreams my-organization
```

### Method 2: Using Terminus directly
```bash
# List organization upstreams
ddev exec terminus upstream:list my-organization

# Get info for a specific site
ddev exec terminus site:info my-site --field=upstream
```

### Method 3: Via Pantheon Dashboard
1. Go to the organization dashboard
2. Click on "Custom Upstreams"
3. Copy the UUID from the URL or page

## Performance Considerations

- The commands make API calls for each site, which can take time for large organizations
- For organizations with 100+ sites, expect commands to run for several minutes
- The `site-inventory` command is particularly intensive as it fetches detailed information for each site including domains, WordPress versions, and dashboard URLs
- Use `--verbose` mode to see real-time progress
- Consider using `--dry-run` first for large operations (when available)

## Security Notes

- Never share Terminus machine tokens
- Review the supporting organization permissions before adding
- Use dry-run mode to verify changes before applying
- Keep CSV exports secure as they contain site information
