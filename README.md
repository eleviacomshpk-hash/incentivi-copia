# Copia del catalogo incentivi.gov.it

incentivi.gov.it (MIMIT) refuses connections from some networks, our Hetzner server's among
them, but answers GitHub's. This folder is a tiny public repository: a GitHub Action reads the
catalog once a day and publishes the open and upcoming bandi in the portal's own format
(`incentivi.json`). The radar bandi (`apps/server/src/bandi.ts`) reads it when the portal itself
does not answer.

The data is open data under the Italian Open Data License 2.0 (IODL 2.0): reuse is allowed
with attribution, "Fonte: incentivi.gov.it (MIMIT)".

## Set it up (once)

1. Create a **public** GitHub repository, e.g. `helloworker/incentivi-copia`.
2. Copy this folder's content into it (keep `.github/workflows/copia.yml`) and push.
3. In the repository, Actions → "Copia del catalogo incentivi.gov.it" → Run workflow. After a
   minute `incentivi.json` appears.
4. On the server, add to `/etc/helloworker/shared.env` (read by every workspace):
   `BANDI_COPY_URL=https://raw.githubusercontent.com/<owner>/<repo>/main/incentivi.json`
   then run `bash deploy/install.sh`.

The radar then reads, in order: the portal, this copy, the public radar-bandi copy.
