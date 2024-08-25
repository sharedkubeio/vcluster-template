# vcluster-template
Template FluxCD GitOps repository for [vCluster](https://www.vcluster.com/docs) deployment on `g1.large` (3vCPU, 12GB Memory) zone size.

## Usage

1. Clone this repository
2. In `helmrelease.yaml`, change `sk-blockyjungle` to your own namespace name.
3. Merge your changes.
4. Create `g1.large` (3vCPU, 12GB Memory) type of Sharedkube Zone.
5. Configure FluxCD in the UI to sync your forked repository.
6. Log in to your zone following the [guide](https://docs.sharedkube.io/getting-started).
7. Wait for the deployment to finish.
8. Export vcluster kubeconfig:
    ```bash
    kubectl get secret vc-vcluster --template={{.data.config}} | base64 -D > vcluster.kubeconfig
    ```
9. Use the kubeconfig to access the vcluster.
    ```bash
   export KUBECONFIG=./vcluster.kubeconfig
   kubectl get pods # You are now in the vcluster
   kubectl create namespace test # You can do whatever you want here 
   ```

## How to leave the vcluster context

1. `unset KUBECONFIG`

## How to remove the vcluster from Sharedkube Zone

1. Disable FluxCD sync in the UI.
2. `helm uninstall vcluster`
3. Done.
