# Security Fixes

This document summarizes the patched vulnerabilities and provides file locations for the reported vulnerabilities listed below: 

---

### #111
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:** POST /api/invite/csv
- **Affected Parameter:** `organizationId`

### #108
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:** POST /api/invite/csv
- **Affected Parameter:** `organizationId`
- **Vulnerability Type:** Broken Access Control (IDOR)

### #98
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:** POST /api/storages/link-global/1818/823/s3
- **Vulnerability Type:** Broken Access Control (IDOR)

### #97
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:** GET /api/storages/s3-server/1
- **Vulnerability Type:** Broken Access Control (IDOR)

### #95
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:**
    - GET /api/storages/azure/5
- **Vulnerability Type:** Broken Access Control (IDOR)

### #94
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:**
    - GET /api/storages/s3/ID
- **Vulnerability Type:** Broken Access Control (IDOR)

### #93
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:** 
    - GET /api/storages/s3/18
- **Vulnerability Type:** Broken Access Control (IDOR)

### #59
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:** 
   - GET https://app.aixblock.io/api/current-user/whoami
- **Vulnerability Type:** Privilege Escalation

### #47
- **Affected sub-domain:** https://app.aixblock.io/
- **Affected Endpoint:** 
    - GET /api/organizations/{Organization-ID}/memberships
- **Vulnerability Type:** Broken Access Control (IDOR)

---

## Fixed issues

- **IDOR vulnerabilities on storage detail endpoints** (#93, #94, #95, #97)
  - **File:** `aixblock_core/io_storages/api.py`
    - Added project permission checks in `ImportStorageDetailAPI.get_object` and `ExportStorageDetailAPI.get_object`.

- **IDOR on organization member listing** (#47)
  - **File:** `aixblock_core/organizations/api.py`
    - `OrganizationMemberListAPI.get_queryset` now verifies the requesting user belongs to the organization.

- **Unrestricted organization invitations** (#111, #108)
  - **File:** `aixblock_core/organizations/api.py`
    - `OrganizationInviteAPIByCSV.post` validates that the requester is an admin of the specified organization.

- **Privilege Escalation and Excessive data exposure in `whoami` endpoint** (#59)
  - **File:** `aixblock_core/users/api.py`
    - `UserWhoAmIAPI` uses `UserCompactSerializer` instead of `UserSerializer`.

---

## Paths and line references

| File                        | Lines                  |
|-----------------------------|------------------------|
| `io_storages/api.py`        | see lines around 103 and 279 |
| `organizations/api.py`      | lines around 158-170 and 426-437 |
| `users/api.py`              | lines around 362-371   |
| `core/permissions.py`       | lines around 112-121   |

