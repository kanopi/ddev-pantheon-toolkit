# Command Reference

## find-people

Lists all team members across all sites you have access to.

**Usage:**
```bash
ddev find-people
```

**Output:**
- Creates `~/site_list_people.csv` with site, email, and role information

**CSV Columns:**
- **Site**: The Pantheon site name
- **Email**: Team member's email address
- **Role**: Their role on the site

---

## find-upstreams

Discovers all upstreams used by sites in an organization.

**Usage:**
```bash
ddev find-upstreams <organization>
```

**Arguments:**
- `organization` - Your Pantheon organization name

**Output:**
- Lists all upstreams with their IDs, names, frameworks, and site counts

---

## add-org

Add a supporting organization to sites in your Pantheon organization.

**Usage:**
```bash
ddev add-org [OPTIONS] <organization> <supporting-org>
```

**Arguments:**
- `organization` - Your Pantheon organization name
- `supporting-org` - The supporting organization to add

**Options:**

| Option | Description |
|--------|-------------|
| `-u, --upstream ID` | Filter by upstream ID (optional, processes all sites if not specified) |
| `-d, --dry-run` | Perform a dry run without making changes |
| `-c, --csv FILE` | Export results to a CSV file |
| `-v, --verbose` | Enable verbose output for debugging |

**Examples:**

Process all sites:
```bash
ddev add-org my-organization supporting-agency
```

Filter by upstream:
```bash
ddev add-org --upstream 8a129104-9ae2-4700-8c23-c7d8f2b8a456 my-organization supporting-agency
```

Dry run with CSV export:
```bash
ddev add-org --dry-run --csv results.csv --verbose my-organization supporting-agency
```

**Logging:**
- Creates `pantheon_org_update_YYYYMMDD_HHMMSS.log` in current directory

---

## site-inventory

Generate a detailed inventory report of all sites in your organization.

**Usage:**
```bash
ddev site-inventory [OPTIONS] <organization>
```

**Arguments:**
- `organization` - Your Pantheon organization name

**Options:**

| Option | Description |
|--------|-------------|
| `-c, --csv FILE` | Export results to CSV file (default: stdout) |
| `-v, --verbose` | Enable verbose output for debugging |

**Examples:**

Output to stdout:
```bash
ddev site-inventory my-organization
```

Export to CSV:
```bash
ddev site-inventory --csv site-inventory.csv my-organization
```

With verbose logging:
```bash
ddev site-inventory --csv site-inventory.csv --verbose my-organization
```

**CSV Columns:**
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

**Logging:**
- Creates `pantheon_site_inventory_YYYYMMDD_HHMMSS.log` in current directory
