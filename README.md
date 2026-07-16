# SHIERTECH — Azure Lighthouse delegation templates

Templates SHIERTECH clients use to grant SHIERTECH **read-only** access for managed-service reporting, via [Azure Lighthouse](https://learn.microsoft.com/azure/lighthouse/) (delegated resource management — free, no Azure charge).

## copilot-spend-delegation.json

Grants SHIERTECH **Cost Management Reader** (read-only cost/billing data — no resource access, no write access of any kind) on the subscription you choose. Used to report your Microsoft Copilot pay-as-you-go spend inside your SHIERTECH vCIO dashboard.

**What it can do:** read cost and billing meter data on the delegated subscription.
**What it can never do:** read your resources' contents, change anything, or extend its own access — the roles are fixed inside the template and only you can change or revoke the delegation.

### Deploy (one click)

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSHIERTECH%2Flighthouse-templates%2Fmain%2Fcopilot-spend-delegation.json)

Sign in with an account that has **Owner** on the subscription, pick the subscription, and use `spObjectId` = `d22e0264-963f-4a12-a221-616d61a9f3ab` (SHIERTECH service principal — same value for every client). Leave `staffGroupObjectIds` empty unless SHIERTECH asks otherwise.

### Deploy (CLI)

```bash
az deployment sub create \
  --location eastus \
  --template-file copilot-spend-delegation.json \
  --parameters spObjectId=d22e0264-963f-4a12-a221-616d61a9f3ab
```

### Revoke (any time, client-side only)

Azure portal → **Service providers** → **Delegations** → delete the SHIERTECH delegation. CLI: `az managedservices assignment delete --assignment <id>`. SHIERTECH cannot revoke or modify the delegation from its side.

---

Questions: support@shiertech.com
