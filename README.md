# Flower AI docker Compose example

```sh
docker compose up -d
docker compose logs -f jupyterlab
```

You should see a URL like `http://localhost:8888/lab?token=0123456789abcdef0123456789abcdef0123456789abcdef`

Open the URL in a browser and start a JupyterLab terminal.
Run:

```sh
export FLWR_LOG_LEVEL=DEBUG
flwr config list
flwr run quickstart-pytorch-usps test-deployment --stream
```

This should run the training example.
You should find the model in the `./outputs` directory.

## Containers

- **`superlink`**: The central coordinating service that routes messages between the `ServerApp` and the `SuperNode`s.
- **`supernode-1`**: Represents the first client edge node (configured for data partition 0) and communicates with the SuperLink.
- **`supernode-2`**: Represents the second client edge node (configured for data partition 1) and communicates with the SuperLink.
- **`serverapp-runner`**: Executes the central aggregation logic (`ServerApp`) and connects to the SuperLink.
- **`clientapp-runner-1`**: Executes the local model training and evaluation (`ClientApp`) for the first client, connecting to `supernode-1`.
- **`clientapp-runner-2`**: Executes the local model training and evaluation (`ClientApp`) for the second client, connecting to `supernode-2`.
- **`jupyterlab`**: Provides the web-based IDE and terminal to interactively run commands and trigger the federated learning workload.
