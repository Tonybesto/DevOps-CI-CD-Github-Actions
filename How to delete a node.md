To delete the Kubernetes control plane that you created using the `kubeadm init` command, you can follow these steps:

1. Drain the control plane node:
   ```
   kubectl drain <control-plane-node-name> --delete-local-data --force --ignore-daemonsets
   ```
   Replace `<control-plane-node-name>` with the name of your control plane node.

2. Reset the `kubeadm` configuration on the control plane node:
   ```
   sudo kubeadm reset
   ```
   This command will remove the control plane components and the `kubelet` configuration on the node.

3. Remove the Kubernetes configuration files:
   ```
   rm -rf $HOME/.kube
   sudo rm -f /etc/kubernetes/admin.conf
   ```
   This will remove the Kubernetes configuration files that were created during the `kubeadm init` process.

4. (Optional) If you have any Kubernetes resources deployed, you can delete them using the following command:
   ```
   kubectl delete all --all
   ```
   This will delete all resources in the current namespace.

After following these steps, the Kubernetes control plane that you created with the `kubeadm init` command will be deleted. Keep in mind that this will also remove any Kubernetes resources and configurations that were created on the node.