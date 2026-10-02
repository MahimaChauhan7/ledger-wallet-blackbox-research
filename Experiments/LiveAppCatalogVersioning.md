# Experiment 03 — Live App Catalog Versioning

## Question

Does the Live App catalog return different application manifests depending on the Ledger Wallet version supplied by the client?

## Experiment A — Client Version Header

The normal header contained:

```text
X-Ledger-Client-Version: lld/4.21.1
```

It was changed to:

```text
X-Ledger-Client-Version: lld/1.0.0
```

The conditional cache header was removed where necessary to obtain a full response.

## Observation

No obvious meaningful catalog difference was observed for the tested values.

Caching behavior was also observed, so this experiment alone cannot establish how the origin server handles every possible client version.

---

## Experiment B — llVersion

The filtered catalog request contained:

```text
llVersion=4.21.1
```

The value was changed to:

```text
llVersion=1.0.0
```

Everything else was kept constant.

## Observation

The responses produced the same observed representation/ETag during the controlled comparison.

## Conclusion

For the specific values tested:

```text
llVersion=1.0.0
        |
        v
Catalog

llVersion=4.21.1
        |
        v
Same observed catalog representation
```

No meaningful version-dependent catalog difference was demonstrated.

This does **not** prove that `llVersion` is universally ignored.

Other versions, applications, server states, or compatibility boundaries may behave differently.