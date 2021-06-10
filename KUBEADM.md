# Kubeadm cheatsheet

Get kubeadm version:

```bash
kubeadm version -o short
```

Initialize a cluster:

```bash
# get version from kubeadm version
kubeadm init --kubernetes-version $(kubeadm version -o short)
```

After cluster is initialized, copy client configuration and certificates. Also set the KUBECONFIG env var:

```bash
sudo cp /etc/kubernetes/admin.conf $HOME/
sudo chown $(id -u):$(id -g) $HOME/admin.conf
export KUBECONFIG=$HOME/admin.conf
```

List tokens:

```bash
kubeadm token list
```

Node: join cluster:

```bash
kubeadm join --token=<token_from_kubeadm_token_list> <ip_address>:<port>
```