# Hyperlane with Espresso

Having Hyperlane integrated with Espresso means:

- The chains interacting (source chain and destination chain) have the corresponding Hyperlane contracts deployed.
- A validator (or several validators) uses the Espresso Caff Node to read fast confirmations from the source chain's Mailbox.
- A relayer publishes the message to the destination's Mailbox.

This repository contains resources on using Espresso-instrumented Hyperlane.

- `espresso-app`: sample application that uses Hyperlane to pass messages.
- `infra-rari-appchain`: contains the configurations to use Hyperlane on both Rari and Appchain testnets.



