# skyerr

Structured errors with unique codes for the Skylence project.

Shared by both [sky-workflow-lint](https://github.com/skylence-be/sky-workflow-lint)
(the `.sky` linter) and the Skylence daemon binary, so every error carries a
stable, greppable code across the whole project.

## Format

```
SKY-{DOMAIN}-{NUMBER}
```

| Domain | Meaning |
|--------|---------|
| `SKY-WF-*`    | Workflow (parse, validate, load, DAG, commands) |
| `SKY-RUN-*`   | Runner (execution, DAG, steps, timeouts) |
| `SKY-WH-*`    | Webhook (parse, signature, routing) |
| `SKY-DB-*`    | Store / database |
| `SKY-CL-*`    | Claude CLI |
| `SKY-CFG-*`   | Config |
| `SKY-CLN-*`   | Clone |
| `SKY-AUTH-*`  | Auth |
| `SKY-WS-*`    | WebSocket |
| `SKY-API-*`   | API request |
| `SKY-NOTIF-*` | Notifications (email/SendGrid) |

## Usage

```go
import "github.com/skylence-be/skyerr"

return skyerr.New(skyerr.ErrConfigMissing, "model not set")
return skyerr.Wrap(skyerr.ErrNotifSendTransport, "sendgrid", err)
```

`*skyerr.Error` implements `Unwrap`, so `errors.Is` / `errors.As` work across a
wrapped chain.
