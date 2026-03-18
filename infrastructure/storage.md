# Storage

> Central documentation of all storage locations, volumes, and backup configurations.

## Overview

| Storage Name | Type     | Location       | Capacity | Used By        | Backup |
|-------------|----------|----------------|----------|----------------|--------|
| _example_   | _SSD/NAS/Cloud_ | _describe_ | _500 GB_ | _service name_ | _yes_  |

<!-- Add storage entries as they are documented -->

## Storage Details

### [Storage Name]

- **Type:** Local SSD / NAS / Cloud Storage (S3, etc.) / External Drive
- **Location:** Host, cloud region, or physical location
- **Capacity:** Total size
- **Used By:** Services or systems that use this storage
- **Mount / Path:** _mount point or bucket name_
- **Backup:**
  - **Enabled:** Yes / No
  - **Frequency:** Daily / Weekly / _describe_
  - **Destination:** _where backups are stored_
  - **Retention:** _how long backups are kept_
  - **Last Verified:** _date of last backup test_
- **Encryption:** Yes / No — _details_
- **Status:** Active / Full / Decommissioned
- **Notes:** _any additional context_

<!-- Copy the section above for each storage location -->

## Backup Summary

| Storage      | Backup Enabled | Frequency | Destination      | Last Verified |
|-------------|---------------|-----------|------------------|---------------|
| _example_   | yes           | daily     | _backup location_ | _YYYY-MM-DD_ |

