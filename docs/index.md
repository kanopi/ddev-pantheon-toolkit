# DDEV Pantheon Toolkit

A DDEV add-on providing commands to manage supporting organizations across Pantheon sites based on their upstream.

## Prerequisites

- **DDEV** - [Install DDEV](https://ddev.readthedocs.io/en/stable/)
- **Pantheon Account** - You must have access to a Pantheon organization
- **Terminus Authentication** - See [Installation Guide](installation.md)

## Commands Overview

### 1. `ddev find-upstreams` - Upstream Discovery
Discovers all upstreams used by sites in an organization. Essential for identifying which upstream ID to use with the add-org command.

### 2. `ddev find-people` - Team Member Discovery
Lists all team members across all sites you have access to. Creates a detailed report showing which users have access to which sites.

### 3. `ddev add-org` - Supporting Organization Management
Add a supporting organization to sites in your Pantheon organization. By default, processes all sites. Optionally filter by upstream ID. Supports:
- Process all sites by default, or filter by upstream with `--upstream`
- Dry-run mode for testing (`--dry-run`)
- CSV export for reporting (`--csv`)
- Verbose logging for debugging (`--verbose`)
- Detailed progress tracking
- Comprehensive error handling

### 4. `ddev site-inventory` - Comprehensive Site Report
Generate a detailed inventory report of all sites in your organization. Exports comprehensive information including:
- Site names and upstreams
- WordPress and PHP versions
- Public URLs (custom domains where available)
- Pantheon dashboard URLs
- Plans and status (Active/Frozen)
- Creation dates and owners
- CSV export for analysis and reporting

## Quick Start

```bash
# Install the DDEV add-on
ddev get kanopi/ddev-pantheon-toolkit

# Restart DDEV to activate the add-on
ddev restart

# Authenticate with Terminus (one-time setup)
ddev ssh
terminus auth:login
exit
```

## Documentation

- [Installation Guide](installation.md)
- [Usage Guide](usage.md)
- [Command Reference](commands.md)
- [CSV Exports](csv-exports.md)
- [Example Workflows](workflows.md)
- [Troubleshooting](troubleshooting.md)

## Support

For issues with:
- This DDEV add-on: [Open an issue on GitHub](https://github.com/kanopi/ddev-pantheon-toolkit/issues)
- Review log files and CSV exports for troubleshooting
- DDEV: https://ddev.readthedocs.io
- Terminus: https://docs.pantheon.io/terminus
- Pantheon platform: https://docs.pantheon.io

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This DDEV add-on is provided as-is for managing Pantheon sites. Use at your own discretion.
