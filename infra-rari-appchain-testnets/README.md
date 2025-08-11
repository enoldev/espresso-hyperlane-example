Having Hyperlane integrated with Espresso means:

- The chains interacting (source chain and destination chain) have the corresponding Hyperlane contracts deployed.
- A validator (or several validators) uses the Espresso Caff Node to read fast confirmations from the source chain's Mailbox.
- A relayer publishes the message to the destination's Mailbox.

This folder specifically covers passing messages between Rari and Appchain (bidirectional).

## The Architecture

Usually, you spin up a validator per origin chain. In this case, we want to provide the following message passing:
- From Rari to Appchain
- From Appchain to Rari

Therefore, there will be a validator that will sign messages conming from Rari, and another validator that signs messages coming from Appchain (2 validators in total). The validators interact with a single relayer, and this relayer is reposible for delivering the message to the destination chain.

The validators will read from the corresponding Espresso Caff Nodes, whose confirmations you can trust before settlement on L1 happens.

The following diagram illustrates the flow:

![](../docs/bidirectionalarch.png)

## Using the Existing Nodes

For the purpose of the Espresso accelerator, we have deployed the corresponding infra, so that people can simply use the Hyperlane Mailboxes to send and receive messages. **This infra is only for testing purposes and we do not guarantee any uptime and/or availability.**

In order to use Hyperlane with Rari and Appchain testnets (both integrated with Espresso), we have deployed the Hyperlane contracts on both chains:

- **Rari Mailbox:** `0xb0bb23B185A7Ba519426C038DEcAFaB4D0a9055b`
- **Appchain Mailbox:** `0x4C58973d0Eb3CeB8aBfd933A1C6EE6f8EA178064`

## Running Your Own Nodes

For any serious use case, you must run your own Hyperlane nodes, which should be pretty easy for the configuration below.

The `docker-compose.yaml` file is already configured with the appropiate configuration files. Three containers are created (Rari's validator, Appchain's validator and the relayer). Every container uses its own configuration file.

### Update the Configuration Files

The configuration files are using the Hyperlane contracts **deployed for testing purposes**. You will need to deploy your own Hyperlane contracts and update the smart contract addresses accordingly.

#### `config-validator-rari.json`

Configuration file of the validator that listens for new messages on Rari's Mailbox contract.

- Update the `mailbox`, `validatorAnnounce`, `merkleTreeHook`, etc fields with the corresponding Hyperlane contract addresses of your deployment **on Rari chain**.
- Update the validator's signing key:

```json
"validator": {
    "type": "hexKey",
    "key": "<PRIVATE-KEY>"
}
```

#### `config-validator-appchain.json`

Configuration file of the validator that listens for new messages on Appchain's Mailbox contract.

- Update the `mailbox`, `validatorAnnounce`, `merkleTreeHook`, etc fields with the corresponding Hyperlane contract addresses of your deployment **on Appchain chain**.
- Update the validator's signing key:

```json
"validator": {
    "type": "hexKey",
    "key": "<PRIVATE-KEY>"
}
```

#### `config-relayer.json`

Configuration file of the relayer that will deliver the messages.

- Update the `mailbox`, `validatorAnnounce`, `merkleTreeHook`, etc fields with the corresponding Hyperlane contract addresses of your deployment **on Rari AND Appchain chain**.
- Update the relayers's signing key. In this case, the same address is used for the source and destination chain and we only run a single relayer. The address must have funds in both Rari and Appchain to work as bidirectional (the destination chain will be both Rari and Appchain, depending on the path).

```json
"defaultSigner": {
    "type": "hexKey",
    "key": "<PRIVATE-KEY>"
}
```

### Use Docker to Start the Containers

Use Docker Compose to spin up the containers:

```bash
docker-compose up -d
```



