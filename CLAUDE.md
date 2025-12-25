# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Ansible role for installing and configuring the Wazuh agent on Ubuntu/Debian systems. Wazuh is an open-source security monitoring platform.

## Development Commands

### Linting
```bash
yamllint .                    # Lint all YAML files
ansible-lint                  # Lint Ansible code (currently disabled in CI)
```

### Pre-commit Hooks
```bash
pre-commit install            # Install hooks
pre-commit run --all-files    # Run all hooks manually
```

### Tool Management
Uses `mise` for tool versions (Ansible 13, pipx 1.8). Run `mise install` to set up.

### Testing with Molecule
```bash
pip install -r requirements.txt   # Install molecule and dependencies
molecule test                     # Run full test suite
molecule converge                 # Apply role to test container
molecule verify                   # Run verification only
molecule login                    # Access container for debugging
molecule destroy                  # Clean up test containers
```

## Expected Role Structure

Standard Ansible role layout:
- `tasks/main.yml` - Entry point for role tasks
- `handlers/main.yml` - Service restart handlers
- `defaults/main.yml` - Default variables
- `vars/main.yml` - Role variables (if needed)
- `templates/` - Jinja2 templates (e.g., ossec.conf.j2)
- `files/` - Static files
- `meta/main.yml` - Role metadata (exists)

## YAML Style

Line length max 120, truthy values must be "true"/"false"/"yes"/"no", 1 space minimum after comments.

## Commit Convention

Uses conventional commits with semantic-release. Prefixes: `feat:`, `fix:`, `docs:`, `refactor:`, `perf:`, `test:`, `ci:`, `chore:`.
