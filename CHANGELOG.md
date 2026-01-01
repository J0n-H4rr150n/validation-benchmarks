# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed
- Forked from xbow-engineering/validation-benchmarks
- Beginning systematic fixes for benchmark issues

---

### XBEN-001-24 - IDOR Trading Platform Authorization
**Date**: 2026-01-01
**Status**: Fixed
**Tested On**: Windows 11

#### Issues Found
- Invalid port syntax in docker-compose.yml causing build failure
  - Error: `invalid port '3306:3306': invalid syntax`
  - Root cause: `expose` directive incorrectly used port mapping syntax
- Missing recommended build command with proper FLAG in README

#### Changes Made
- Fixed docker-compose.yml port configuration
  - Changed `expose: - 3306:3306` to `expose: - 3306`
  - The `expose` directive only accepts internal container ports, not host:container mappings
- Added recommended build command section to README.md
  - FLAG: `xben-001-24_idor_trading_platform_authorization`
  - Full command: `docker compose down && make clean && make build FLAG="xben-001-24_idor_trading_platform_authorization" && make run`

#### Files Modified
- `benchmarks/XBEN-001-24/docker-compose.yml`
- `benchmarks/XBEN-001-24/README.md`

#### Result
✅ Benchmark builds and runs successfully

---

## Notes on Versioning

Since this is a fork focused on fixes, we'll track changes by benchmark ID rather than semantic versions.
Each benchmark fix will be documented below with:
- **Benchmark ID**: The XBEN-XXX-24 identifier
- **Issue**: What was broken
- **Fix**: What was changed
- **Files Modified**: List of affected files

---

<!-- Template for new entries:

### XBEN-XXX-24 - [Brief Description]
**Date**: YYYY-MM-DD
**Branch**: fix/xben-xxx-brief-description

#### Issue
- Describe what was broken

#### Fix
- Describe what was changed

#### Files Modified
- path/to/file1
- path/to/file2

---

-->
