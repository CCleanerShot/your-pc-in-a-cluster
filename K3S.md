# K3S Setup

## Setup Steps

### 1. Initialize Head Node (Server)

SSH into the head node and run:

bash

```bash
# Install K3S server
curl -sfL https://get.k3s.io | sh -

# Verify installation
sudo k3s kubectl get node

# Start K3S server (if not already running)
sudo systemctl start k3s

# Check status
sudo systemctl status k3s
```

### 2. Get Server Token

On the head node:

bash

```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

Save this token - you'll need it for worker nodes.

### 3. Join Worker Nodes

On each worker node, run:

bash

```bash
curl -sfL https://get.k3s.io | \
  K3S_URL= <ip-address-of-head-node>:6443 \
  K3S_TOKEN=<your-token-here> \
  sh -
```

### 4. Verify Cluster

Back on the head node:

bash

```bash
sudo k3s kubectl get nodes
```

