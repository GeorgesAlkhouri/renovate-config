# renovate-config

Gemeinsame Renovate-Presets für alle Repos von GeorgesAlkhouri.
Funktioniert mit der Mend Renovate App und mit Self-Hosted Renovate.

## Nutzung

`renovate.json` im Ziel-Repo:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>georgesalkhouri/renovate-config",
    "github>georgesalkhouri/renovate-config:python(3.13)",
    "github>georgesalkhouri/renovate-config:docker"
  ]
}
```

Im Repo selbst stehen nur noch Spezialitäten: eigene Regex-Manager, Pins einzelner Pakete, Zeitpläne, Ausnahmen beim Automerge.

## Presets

| Preset | Inhalt |
|---|---|
| `default` | `config:best-practices`, Semantic Commits, Zeitzone Europe/Berlin, keine PR-Limits, 7 Tage Wartezeit (Releases ohne Zeitstempel werden nicht blockiert), keine Wartezeit für Digests, Lockfile-Pflege und eigene Images `ghcr.io/georgesalkhouri/**`, Sicherheits-Updates sofort mit Label `security`, Gruppe „GitHub Actions" (non-major), Automerge für minor/patch/digest ab Version 1.0 und für Lockfile-Pflege, Major immer manuell, pre-commit-Manager an. |
| `python(<linie>)` | Hält Python auf einer Linie (pep621, Dockerfile, setup-python). Gruppe „python dependencies" für pep621. Beispiel: `:python(3.13)`. |
| `docker` | Versionierung für linuxserver.io-Images, Gruppe „docker base images" für Dockerfiles. |

## Hinweise

- Änderungen an `main` wirken sofort in allen Repos. Die CI prüft jede Änderung mit `renovate-config-validator`.
- Testen vor dem Merge: im Ziel-Repo auf einen Branch zeigen, z. B. `github>georgesalkhouri/renovate-config#mein-branch` bzw. mit Parameter `github>georgesalkhouri/renovate-config:python#mein-branch(3.13)` (Branch vor dem Parameter).
