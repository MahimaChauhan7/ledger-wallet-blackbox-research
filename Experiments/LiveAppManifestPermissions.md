# Experiment 04 — Live App Manifest Permissions

## Question

Do the `permissions` declared by a Live App manifest control whether the application itself can load?

This experiment does not yet test whether individual privileged capability calls are authorized.

## Baseline

The Lido manifest declared permissions including:

```text
account.list
account.request
currency.list
message.sign
transaction.signAndBroadcast
wallet.userId
wallet.info
```

With the original manifest, Lido loaded normally until functionality requiring unavailable Ledger hardware became relevant.

## Experiment

The catalog response was intercepted before Ledger Wallet consumed it.

Only Lido's permission array was changed.

Original:

```json
"permissions": [
  "account.list",
  "account.request",
  "currency.list",
  "message.sign",
  "transaction.signAndBroadcast",
  "wallet.userId",
  "wallet.info"
]
```

Modified:

```json
"permissions": []
```

The modified catalog response was forwarded to Ledger Wallet.

## Observation

Lido continued to load normally.

Therefore:

```text
Original permissions
        ↓
    Lido loads

permissions=[]
        ↓
    Lido loads
```

## Conclusion

The experiment demonstrates that Lido's declared manifest permissions are not required merely for the Live App to load/render.

It does **not** demonstrate that the permissions are unenforced.

A plausible model remains:

```text
Load Live App
     |
     | no permission check required here
     v
Remote application
     |
     | requests privileged capability
     v
Permission enforcement?
     |
     v
account / wallet / signing / device
```

The location and behavior of that enforcement point remain unknown.

## Limitation

No Ledger hardware device was available.

Therefore device-dependent behavior cannot currently provide a clean permission-enforcement comparison.

## Status

**Architectural observation — not a confirmed vulnerability.**

The important unanswered question is:

> Can a Live App successfully invoke a Ledger capability that has been removed from its manifest permissions?