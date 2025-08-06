# Counter Application

This is a sample application that showcases how to use Hyperlane to perform cross-chain message passing. Specifically, this example uses Rari testnet and Appchain testnet (along with the Hyperlane contract deploy on each chain). The flow is the following:

1. The user triggers the “increment” of the counter on Rari (source chain).
2. Hyperlane relays the message to Appchain.
3. The counter is incremented on Appchain (destination chain).

In order for this to work, you will need a Hyperlane validator and relayer correctly configured to perform `Rari -> Appchain` message passing.

## Hyperlane Mailbox

- **Rari Mailbox:** `0xb0bb23B185A7Ba519426C038DEcAFaB4D0a9055b`
- **Appchain Mailbox:** `0x4C58973d0Eb3CeB8aBfd933A1C6EE6f8EA178064`
