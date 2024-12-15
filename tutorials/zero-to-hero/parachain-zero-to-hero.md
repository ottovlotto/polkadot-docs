---
title: Parachain Zero to Hero
description: This tutorial starts with a template and guides you step-by-step through parachain development, testing, and deployment, including obtaining coretime.
---

# Parachain Zero to Hero

## Introduction

This tutorial starts with a pre-built template and guides you step-by-step through the parachain development, testing, deployment, and maintenance cycle. This tutorial is intended for developers interested in blockchain development.

By the end of this tutorial, you will be able to:

- Compile and run a local parachain node using the Polkadot SDK Parachain Template
- Build a custom pallet from scratch
- Create a unit testing suite for a custom pallet
- Add both custom and Polkadot SDK pallets to a runtime
- Write benchmarking tests and execute the benchmarking tool to calculate extrinsic weights and fees
- Upgrade the runtime of a Polkadot SDK-based blockchain without stopping the network or creating a fork
- Deploy a parachain on a public test network
- Obtain coretime for block production

## Prerequisites

Before you start the tutorial, you should: 

- Visit [Install Polkadot SDK Dependencies](/develop/parachains/install-polkadot-sdk/) and follow the instructions for your operating system to install dependencies, including Rust, and set up your development environment

!!! tip
    This tutorial focuses on the steps required to complete the project and limits conceptual content to the minimum needed to complete the tasks. This helps create a structured, experiental learning process. 

    Links to parachain guides are included at the end of the exercise for those who want to learn more about parachain concepts, customization options, and advanced features. Reading the linked guides is not required to successfully complete the tutorial.

## Set Up a Template

The Polkadot SDK Parachain Template provides a pre-configured, functional runtime you can use in your local development environment. Follow these steps to get started:

### Install Utility Tools

First, install the utility tools for working with the template as follows:

- **Chain spec builder** - Polkadot SDK utility for generating chain specifications. Install the `chain-spec-builder` binary by executing the following command:
    
    ```bash
    cargo install --git https://github.com/paritytech/polkadot-sdk --force staging-chain-spec-builder
    ```

- **Polkadot Omni Node** - white-labeled Polkadot-SDK binary. It can run the wasm blob of the parachain locally for testing and development. Install the `polkadot-omni-node` binary by executing the following command:

    ```bash
    cargo install --git https://github.com/paritytech/polkadot-sdk --force polkadot-omni-node
    ```

### Compile the Runtime

The template provides a ready-to-use development environment for building using the Polkadot SDK. Follow these steps to compile the runtime:

1. Clone the template repository:
    ```bash
    git clone https://github.com/paritytech/polkadot-sdk-parachain-template.git parachain-template
    ```

2. Navigate to the root of the template directory:
    ```bash
    cd parachain-template
    ```

3. Compile the runtime:
    ```bash
    cargo build --release
    ```

    !!!note
        Initial compilation may take several minutes, depending on your machine specifications. Always use the `--release` flag to build optimized, production-ready artifacts.

4. Upon successful compilation, you should see output similar to:
    --8<-- 'code/tutorials/polkadot-sdk/parachains/zero-to-hero/set-up-a-template/compilation-output.html'

### Start the Local Chain

With the runtime compiled, you can spin up your parachain locally to produce blocks and allow you to interact. Follow these steps to launch your parachain node in development mode:

1. Generate the chain spec file of your parachain by executing the following command:

    ```bash
    chain-spec-builder create -t development \
    --relay-chain paseo \
    --para-id 1000 \
    --runtime ./target/release/wbuild/parachain-template-runtime/parachain_template_runtime.compact.compressed.wasm \
    named-preset development
    ```
    
2. With the chain spec file in place, start the omni node in developer mode to produce and finalize blocks by executing the following command:

    ```bash
    polkadot-omni-node --chain ./chain_spec.json --dev
    ```

    !!! tip
        The `--dev` option does the following:

        - Deletes all active data (keys, blockchain database, networking information) when you stop the parachain node
        - Ensures a clean working state each time you restart the parachain node

3. Verify that your parachain node is running by reviewing the terminal output. You should see something similar to:
    --8<-- 'code/tutorials/polkadot-sdk/parachains/zero-to-hero/set-up-a-template/node-output.html'

4. Confirm that your blockchain is producing new blocks by checking if the number after `finalized` is increasing
    --8<-- 'code/tutorials/polkadot-sdk/parachains/zero-to-hero/set-up-a-template/node-block-production.html'

    !!!note
        The details of the log output are explored in other guides. For now, knowing that your parachain node is running and producing blocks is sufficient.

### Interact with the Local Chain

To interact with your parachain node using the [Polkadot.js Apps](https://polkadot.js.org/apps/#/explorer){target=\_blank} interface, follow these steps:

1. Open [Polkadot.js Apps](https://polkadot.js.org/apps/#/explorer){target=\_blank} in your web browser and click the network icon in the top left corner
    
    ![](/images/tutorials/polkadot-sdk/parachains/zero-to-hero/set-up-a-template/set-up-a-template-1.webp)

2. Connect to your local node:
    1. Scroll to the bottom and select **Development**
    2. Choose **Custom**
    3. Enter `ws://localhost:9944` in the input field
    4. Click the **Switch** button
    
    ![](/images/tutorials/polkadot-sdk/parachains/zero-to-hero/set-up-a-template/set-up-a-template-2.webp)

3. Verify connection:
    - Once connected, you should see **parachain-template-runtime** in the top left corner
    - The interface will display information about your local blockchain
    
    ![](/images/tutorials/polkadot-sdk/parachains/zero-to-hero/set-up-a-template/set-up-a-template-3.webp)

### Stop the Local Chain

Follow these steps to stop your local parachain node:

1. Return to the terminal window where the node output is displayed
2. Press `Control-C` to stop the running process
3. Verify that your terminal returns to the prompt in the `parachain-template` directory

## Build a Custom Pallet

### Create a New Project

### Add Dependencies

### Add Scaffold Pallet Structure

### Pallet Configuration

### Define Events 

### Define Storage Items

### Implement Custom Errors

### Implement Calls

### Verify Compilation

## Where to Go Next

### Parachain Guides

A deeper dive into the concepts introduced in this tutorial

<div class="grid cards" markdown>

- :octicons-goal-16:{ .lg .middle } [Set Up a Template](/tutorials/polkadot-sdk/parachains/guides/set-up-a-template/){target=\_blank}

- :octicons-goal-16:{ .lg .middle } [Build a Custom Pallet](/tutorials/polkadot-sdk/parachains/guides/build-custom-pallet.md){target=\_blank}

- :octicons-goal-16:{ .lg .middle } [TODO](#){target=\_blank}

- :octicons-goal-16:{ .lg .middle } [TODO](#){target=\_blank}



</div>

### Additional Resources

<div class="grid cards" markdown>

- :octicons-book-16:{ .lg .middle } [Chain Spec Builder Rust docs](https://paritytech.github.io/polkadot-sdk/master/staging_chain_spec_builder/index.html){target=\_blank}

- :octicons-book-16:{ .lg .middle } [Polkadot Omni Node Rust docs](https://paritytech.github.io/polkadot-sdk/master/polkadot_sdk_docs/reference_docs/omni_node/index.html){target=\_blank}

- [Polkadot.js Guides](https://wiki.polkadot.network/docs/learn-polkadot-js-guides){target=\_blank} on the Polkadot Wiki

</div>


