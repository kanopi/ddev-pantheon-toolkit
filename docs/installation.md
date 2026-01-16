# Installation

## Requirements

Before installing the DDEV Pantheon Toolkit, ensure you have:

- **DDEV** - [Install DDEV](https://ddev.readthedocs.io/en/stable/)
- **Pantheon Account** - You must have access to a Pantheon organization
- **Terminus Authentication** - Follow the setup below

## Installation Steps

### 1. Install the DDEV Add-on

```bash
ddev get kanopi/ddev-pantheon-toolkit
```

### 2. Restart DDEV

After installation, restart DDEV to activate the add-on:

```bash
ddev restart
```

### 3. Authenticate with Terminus

This is a one-time setup:

```bash
ddev ssh
terminus auth:login
# Follow the prompts to authenticate
exit
```

## Verification

Verify the installation by running:

```bash
ddev find-upstreams --help
```

If you see the help output, the installation was successful!

## Troubleshooting Installation

### Commands not found after installation

If commands are not available after installation:

```bash
ddev restart
```

### Authentication Issues

If you encounter authentication errors:

```bash
ddev ssh
terminus auth:login
exit
```

Make sure you have access to your Pantheon organization through the web dashboard before attempting to authenticate with Terminus.
