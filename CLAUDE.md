# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Curated IPv4 CIDR block lists for Microsoft 365 / Microsoft Entra IP-based security controls (Named Locations, Conditional Access, and related allow/block workflows). This is a **data-only repository** with no build system, tests, or linting.

## New Session

When starting a new session, this is what you should do.

1. Read `/notes/progress`
2. Read `/notes/decisions`
3. Check recently modified files.
4. Suggest the next item to work on. 

## Directory Structure

- `lists/providers/` - Canonical provider-specific CIDR lists (source of truth)
- `lists/combined/` - Large aggregated lists (e.g., AWS IPv4 ranges)
- `lists/chunks/` - Split files for Microsoft's Named Location limits

## Key Architecture Notes

**Chunking Strategy**: Microsoft Entra Named Locations have a limit on IP addresses per location. Files exceeding ~2,000 CIDRs are split into chunked versions in `lists/chunks/<provider>/` using 001-based indexing (e.g., `provider-part-001.txt`).

**File Format**: All list files are plain text with one IPv4 CIDR per line:
```
203.0.113.0/24
198.51.100.10/32
```

**IPv4 Only**: This repository currently contains IPv4 CIDR lists only.

## Maintenance Workflow

1. Replace or regenerate provider source files in `lists/providers/`
2. Re-split large files (>2,000 CIDRs) into `lists/chunks/<provider>/`
3. Validate line counts with `wc -l` before committing
4. Update file inventory in README.md if CIDR counts change
5. Commit with date-stamped message indicating refresh source and date

## Usage Context

- `lists/providers/` - Use when one named location per provider is acceptable
- `lists/chunks/` - Use when splitting uploads into multiple named locations due to platform limits
- `lists/combined/` - Use for broad cloud provider coverage (currently AWS only)

## Notes Protorcol
 
1. When making changes or any progress, update `/notes/progress.md`
2. When making decisions put them in `/notes/decisions.md`

1. Add what what you think the next steps should be or any ideas or suggestions you come with.
2. Write any open questions you have.

## Git usage

1. Never include "Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>" when writing a commit.