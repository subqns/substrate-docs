# Start a Node

## **Pre Requirements**

1. [Prepare your browser to work with Cere Block Viewer](https://cere-network.gitbook.io/cere-network/tools/block-viewer/prepare-a-browser-to-work-with-cere-block-viewer)
2. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. [Install Docker](https://docs.docker.com/get-docker/)
4. [Install Docker Compose 1.25.0+](https://docs.docker.com/compose/install/)
5. [Install & Configure Network Time Protocol \(NTP\) Client - Linux only](https://cere-network.gitbook.io/cere-network/node/install-and-update/install-and-configure-network-time-protocol-ntp-client)

## **Start a Node**

To run a Node on your host, please follow the steps below.

1. Clone the [repository](https://github.com/Cerebellum-Network/nodes-installation-scripts) and go to its folder:

   ```text
    git clone git@github.com:Cerebellum-Network/nodes-installation-scripts.git
    cd nodes-installation-scripts
   ```

2. Add permissions to the `chain-data` folder:

   ```text
    chmod -R 777 ./chain-data
   ```

3. Open the following ports in your firewall so that inbound traffic from the Internet can reach your Node:
   1. Validator Node:
      1. `30333` - Specifies the port that your node will listen for p2p traffic on
   2. Full / Archive Node:
      1. `9933` - Specifies the port that your node will listen for incoming RPC traffic on
      2. `9944` - Specifies the port that your node will listen for incoming WebSocket traffic on
      3. `30333` - Specifies the port that your node will listen for p2p traffic on
4. Run the script to confirm your environment is ready for a Node. If some check fails the Node can work incorrectly. From the root directory run \(Linux only\).
   1. Validator Node:

      ```text
       ./scripts/env-host-check.sh --validator
      ```

   2. Full / Archive Node:

      ```text
       ./scripts/env-host-check.sh --full
      ```

      You can see result by green `✔` \(successfully\) or red ✘ \(failed\). In case of having errors, please refer [here](https://cere-network.gitbook.io/cere-network/node/install-and-update/how-to-fix-environment-errors) to resolve.
5. Specify `NODE_NAME` parameter in the [configs/.env.testnet](https://github.com/Cerebellum-Network/nodes-installation-scripts/blob/master/configs/.env.testnet#L4). The value for the `NODE_NAME` will be used to distinguish nodes in the [Telemetry dashboard](https://telemetry.polkadot.io/#list/Cerebellum%20Network%20Testnet).
6. Run the command to start a Node. Since this moment your Node will run in the background.
   1. Validator Node:

      ```text
       docker-compose --env-file ./configs/.env.testnet up -d add_validation_node_custom
      ```

   2. Full Node:

      ```text
       docker-compose --env-file ./configs/.env.testnet up -d full_node
      ```

   3. Archive Node:

      ```text
       docker-compose --env-file ./configs/.env.testnet up -d archive_node
      ```
7. Run the command to confirm Node has been started successfully.

   ```text
    docker-compose logs -f | grep "Local node identity is"
   ```

    You should have at least one line in the output. Below is an example:

   ```text
    Mar 03 14:42:23.973  INFO Local node identity is: 12D3KooWLafVQ2XGQS8A3rdj9t8rX5UFcVGxtx8a9vgQsYJi7Rdz (legacy representation: 12D3KooWLafVQ2XGQS8A3rdj9t8rX5UFcVGxtx8a9vgQsYJi7Rdz)
   ```

   If you can not see the output in more than 2 minutes you should check node logs. Use the [instructions](https://cere-network.gitbook.io/cere-network/node/install-and-update/node-logs) to know more about logs and their set up.

8. [Launch Cere Block Viewer](https://block-viewer.cere.network/?rpc=ws%3A%2F%2Flocalhost%3A9944#/explorer). You can check the Node's `syncing` status. To do this go to the `Network` -&gt; `Explorer` -&gt; `Node info`. It should be equal to `yes` or `no` \(synced already\).

![node-syncing](https://staticassetsshare.s3-us-west-2.amazonaws.com/validator/node-syncing.png)

Congratulations! You've successfully started a Node on your host.   
  
Please, follow the "Become a Validator or Full / Archive Node" instructions to finish setting up.

