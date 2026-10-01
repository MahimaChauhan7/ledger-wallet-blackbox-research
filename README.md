# ledger-wallet-blackbox-research
Black-box security research into the trust boundaries between Ledger Wallet Desktop, remote Live Apps, the Live App catalog, and privileged wallet capabilities.

Status: Research in progress. No confirmed vulnerability is claimed by this repository.

Objective

The goal is to understand Ledger Wallet's security architecture experimentally without initially relying on its source code.

The methodology is:

Input → Modify one variable → Observe output → Form hypothesis → Design next experiment

The primary security invariant being investigated is:

Untrusted dApp content must not gain unauthorized access to privileged Ledger Wallet, Electron, Node.js, device, account, or signing capabilities.

A related capability invariant is:

A Live App should not be able to invoke Ledger capabilities that it is not authorized to use.

Current Black-Box Model

Live App Catalog
      |
      v
Manifest
  |       \
  |        \
 URL     permissions/domains
  |             |
  v             v
Remote Live App
      |
      v
Ledger Wallet
      |
      v
Unknown internal bridge
      |
      +------ Account capabilities
      +------ Wallet capabilities
      +------ Signing capabilities
      +------ Device capabilities

The exact implementation and enforcement points of this bridge have not yet been established.

Environment

Ledger Wallet Desktop: 4.21.1

Platform: macOS

Proxy: Burp Suite

Testing methodology: Black-box

Ledger hardware device: Not available

The lack of a hardware device limits experiments involving device communication and actual signing.
