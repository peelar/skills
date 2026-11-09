# Signals

Each search is a lead, not a finding. Add `--glob` for the repo's languages.

## Backend

- **Status fields:** `rg -n '\b(status|state|phase|stage|step)\b\s*[:=?]'`
- **Lifecycle timestamps:** `rg -n '\b(revoked|deleted|completed|expires|confirmed|cancelled|used|locked|failed)(At|_at)\b'`
- **Presence checks:** `rg -n '!= null|!== undefined|=== undefined|if \(!\w+\.\w+\)'`
- **Boolean flags:** `rg -n '\b(is|has|was)[A-Z]\w*\s*[:?]'`
- **Locks, leases, expiry and retries:** `rg -in 'lock|lease|pending|ttl|expire|retention|attempt|retr(y|ies)'`
- **Records that stand for a step** (a code, ticket, session or transaction), grouped by record name: `rg -n '\.(take|delete|put|create|insert|upsert)\('`
- **Repeated guards**, for each candidate entity: `rg -n '<entity>\.\w+ &&'`

## Frontend

- **Boolean soup:** `rg -n 'useState<boolean>|useState\((true|false)\)|\[is[A-Z]\w*, set'`
- **State clusters:** `rg -c 'useState\('`, then read each component with three or more.
- **Step indices:** `rg -n '\b(step|stage|screen|view|mode)\b' --glob '*.{tsx,jsx,vue,svelte}'`
- **Effect chains:** `rg -n 'useEffect\('`, then read each effect that calls a setter.
- **Request status by hand:** `rg -n 'setLoading|setError|setData|setPending'`
- **URL and storage state:** `rg -n 'searchParams|localStorage|sessionStorage|document\.cookie'`
- **Pages that mirror a backend record:** pages that render one view per backend status.

Rule a hit out when its entity has one fragment written in one place, or already has an explicit machine (a tagged union with one transition function, a reducer over a discriminated union, or a library such as XState).
