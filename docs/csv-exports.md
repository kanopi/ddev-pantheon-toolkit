# CSV Export Formats

All commands that generate CSV exports follow consistent formatting for easy analysis and reporting.

## add-org CSV Format

The `add-org` command (when using `--csv`) exports CSV files with the following columns:

- **Site Name**: The Pantheon site name
- **Site ID**: The site's UUID
- **Upstream ID**: The upstream UUID
- **Current Status**: Status before the script ran
- **Action Taken**: What the script did
- **Notes**: Additional information

**Example:**
```csv
Site Name,Site ID,Upstream ID,Current Status,Action Taken,Notes
my-site,abc-123,upstream-456,No supporting org,Added,Successfully added supporting org
another-site,def-789,upstream-456,Already present,Skipped,Supporting org already exists
```

---

## site-inventory CSV Format

The `site-inventory` command exports CSV files with the following columns:

- **Site Name**: The Pantheon site name
- **Upstream**: Upstream name or UUID
- **WordPress Version**: Core version (WordPress sites only)
- **PHP Version**: PHP version on live environment
- **Public URL**: Custom domain or platform domain
- **Pantheon Dashboard URL**: Direct link to dashboard
- **Plan**: Site plan name
- **Status**: Active or Frozen
- **Created date**: Site creation timestamp
- **Owner**: Owner email address

**Example:**
```csv
Site Name,Upstream,WordPress Version,PHP Version,Public URL,Pantheon Dashboard URL,Plan,Status,Created date,Owner
my-wp-site,WordPress,6.4.2,8.2,https://example.com,https://dashboard.pantheon.io/...,Basic,Active,2023-01-15,owner@example.com
drupal-site,Drupal 10,,8.2,https://site.pantheon.io,https://dashboard.pantheon.io/...,Performance,Active,2023-03-20,admin@example.com
```

---

## find-people CSV Format

The `find-people` command exports CSV files with the following columns:

- **Site**: The Pantheon site name
- **Email**: Team member's email address
- **Role**: Their role on the site

**Example:**
```csv
Site,Email,Role
my-site,admin@example.com,admin
my-site,developer@example.com,developer
another-site,admin@example.com,team
```

---

## Working with CSV Files

### View in Terminal
```bash
cat filename.csv
```

### Open in Spreadsheet Applications
- Microsoft Excel
- Google Sheets
- LibreOffice Calc
- Apple Numbers

### Command Line Tools
```bash
# View first 10 rows
head -10 filename.csv

# Search for specific content
grep "wordpress" filename.csv

# Count rows
wc -l filename.csv
```

### Security Considerations

CSV exports may contain sensitive information:
- Site names and IDs
- Email addresses
- Site ownership information
- Infrastructure details

**Best Practices:**
- Store CSV files securely
- Don't commit CSV files to public repositories
- Share only with authorized team members
- Delete CSV files when no longer needed
