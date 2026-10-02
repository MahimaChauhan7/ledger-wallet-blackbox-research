# Experiment 02 — Swap Live App Parameters

## Question

What information does Ledger Wallet provide to the remote Swap Live App, and how does the application respond when individual parameters are modified?

## Observation

Ledger Wallet loaded:

```text
swap-live-app.ledger.com
```

with query parameters including:

```text
isEmbedded
swapEntryPoint
swapApiBase
platform
currentVersion
```

Two naturally occurring contexts were observed.

### Main/sidebar context

```text
isEmbedded=false
swapEntryPoint=main_page
```

### Portfolio context

```text
isEmbedded=true
swapEntryPoint=portfolio_embed
```

This indicates that the same remote application receives information describing the context in which Ledger Wallet opened it.

## swapApiBase Experiment

The original value was:

```text
swapApiBase=https://swap.ledger.com/v5
```

In Burp Repeater it was changed to:

```text
swapApiBase=https://example.com
```

The server returned HTTP 200 and the modified value appeared in the application's Next.js state/search parameters.

## Observation

The application accepted the arbitrary URL as client-side state.

However, during runtime testing, no request to `example.com` was observed.

## Conclusion

The experiment demonstrates:

```text
User-controlled query value
        ↓
Swap application
        ↓
Application state
```

It does **not** demonstrate:

```text
Arbitrary URL
    ↓
Runtime network request
```

Therefore this is currently an architectural observation rather than a security vulnerability.