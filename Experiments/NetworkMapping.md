# Experiment 01 — Network Mapping

## Question

What external services does Ledger Wallet communicate with when loading its application and Live App functionality?

## Method

Ledger Wallet Desktop was launched through Burp Suite as an HTTP(S) proxy.

Traffic was observed without initially modifying requests.

## Observations

Several services appeared in Ledger Wallet traffic.

The most relevant to the Live App investigation were:

```text
live-app-catalog.ledger.com
swap-live-app.ledger.com
swap.ledger.com
```

The catalog endpoint returned JSON containing Live App definitions.

Observed manifest fields included:

```text
id
name
url
homepageUrl
platforms
apiVersion
manifestVersion
branch
currencies
permissions
domains
visibility
params
dapp
```

## Inferred Architecture

The observations suggest the following high-level architecture:

```text
Ledger Wallet
     |
     | GET catalog
     v
Live App Catalog
     |
     | manifest
     v
Ledger Wallet
     |
     | load remote application
     v
Live App
```

Some manifests additionally declare wallet-related capabilities.

## Important Limitation

Network traffic alone does not reveal how privileged Live App capabilities are implemented.

Capabilities such as:

```text
wallet.info
account.list
message.sign
transaction.sign
```

did not appear as obvious corresponding HTTP endpoints during these observations.

They may therefore cross another internal application boundary that is not visible as ordinary HTTP traffic.

This remains a hypothesis.

## Result

The experiment identified the Live App catalog as an important trust/configuration boundary for further black-box testing.