# GeoLite2 Database Repository

[![GitHub Release](https://img.shields.io/github/v/release/jowinjohnchemban/GeoLite.mmdb?style=flat-square)](../../releases)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/jowinjohnchemban/GeoLite.mmdb/.github/workflows/GeoLite.yml?style=flat-square&label=Update)](../../actions)
[![Stars](https://img.shields.io/github/stars/jowinjohnchemban/GeoLite.mmdb?style=flat-square)](../../stargazers)
[![Forks](https://img.shields.io/github/forks/jowinjohnchemban/GeoLite.mmdb?style=flat-square)](../../network/members)
[![Last Commit](https://img.shields.io/github/last-commit/jowinjohnchemban/GeoLite.mmdb?style=flat-square)](../../commits)

Automated distribution of [MaxMind GeoLite2](https://dev.maxmind.com/geoip/geoip2/geolite2/) geolocation databases with regular updates via GitHub Actions.

> **Note:** Replace `jowinjohnchemban/GeoLite.mmdb` in badges above with your repository path

## Overview

This repository automatically downloads and publishes the latest MaxMind GeoLite2 databases every three days. The workflow handles:

- **ASN Database** - Autonomous System Number geolocation data
- **City Database** - City-level geographic and network information
- **Country Database** - Country-level geographic data

All databases are in MaxMind DB format (`.mmdb`) for efficient IP geolocation lookups.

## Download Options

### GitHub Releases
Latest databases are available in [GitHub Releases](../../releases):
- [GeoLite2-ASN.mmdb](../../releases)
- [GeoLite2-City.mmdb](../../releases)
- [GeoLite2-Country.mmdb](../../releases)

### Direct Download Branch
Files are also available on the `download` branch:
- [GeoLite2-ASN.mmdb](../../raw/download/GeoLite2-ASN.mmdb)
- [GeoLite2-City.mmdb](../../raw/download/GeoLite2-City.mmdb)
- [GeoLite2-Country.mmdb](../../raw/download/GeoLite2-Country.mmdb)

## Requirements

To use this repository's automation, you need:
- A [MaxMind account](https://www.maxmind.com/en/account/login) with GeoLite2 access
- Your MaxMind License Key stored as a GitHub secret (`LICENSE_KEY`)

## Environment Variables

The workflow relies on the following environment variables and secrets:

- `LICENSE_KEY` — Required GitHub secret containing your MaxMind GeoLite2 license key.
- `GITHUB_TOKEN` — Automatically provided by GitHub Actions for repository access. No manual setup is required.

### Optional environment settings

If you want to override or extend the workflow, you can add the following custom repository secrets or environment variables:

- `RELEASE_NAME_PREFIX` — Optional prefix for release names.
- `RELEASE_BODY_TEMPLATE` — Optional release notes template (if you later customize the workflow to support it).

> Tip: Keep secrets private and never commit them to the repository.

## Workflow Details

The GitHub Actions workflow:
1. Downloads latest databases from MaxMind
2. Validates successful downloads
3. Creates releases tagged with the update date (YYYY.MM.DD)
4. Maintains the download branch with latest files
5. Cleans up old releases (keeps 2 most recent)
6. Cleans up old workflow runs (keeps 2 most recent, 7-day retention)

**Update Schedule:** Every 3 days at 01:00 UTC

## GitHub API Integration

You can programmatically access the latest databases using GitHub API:

### Latest Release Assets
```bash
# Get latest release metadata
curl -s https://api.github.com/repos/jowinjohnchemban/GeoLite.mmdb/releases/latest

# Download latest ASN database
curl -L -o GeoLite2-ASN.mmdb \
  $(curl -s https://api.github.com/repos/jowinjohnchemban/GeoLite.mmdb/releases/latest | \
  grep 'browser_download_url.*GeoLite2-ASN' | cut -d'"' -f4)
```

### Check Release Information
```bash
# List all releases
curl -s https://api.github.com/repos/jowinjohnchemban/GeoLite.mmdb/releases

# Get specific release by date
curl -s https://api.github.com/repos/jowinjohnchemban/GeoLite.mmdb/releases/tags/2026.06.27
```

### Repository Statistics
```bash
# Repository info
curl -s https://api.github.com/repos/jowinjohnchemban/GeoLite.mmdb

# Workflow runs
curl -s https://api.github.com/repos/jowinjohnchemban/GeoLite.mmdb/actions/runs

# Latest workflow run
curl -s https://api.github.com/repos/jowinjohnchemban/GeoLite.mmdb/actions/runs?status=success&limit=1
```

## License

- **Database Contents:** © [MaxMind, Inc.](https://www.maxmind.com/) - All rights reserved
- **Database License:** [GeoLite2 End jowinjohnchemban License Agreement](https://www.maxmind.com/en/geolite2/eula)
- **Distribution License:** [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/)

## Disclaimer

This repository is for distributing public GeoLite2 databases. jowinjohnchembans are responsible for:
- Obtaining proper licensing from MaxMind
- Complying with MaxMind's terms of service
- Adhering to applicable copyright and licensing terms

