---
layout: "documents"
page_title: "Kubernetes cluster"
sidebar_current: "getting-started-networking-installation-k8s"
description: |-
  Setting up Kubernetes cluster
---

# Installing Contiv with Kubernetes

####Pre-requisites
Machines running CentOS 7.2, connected to network, with at least two
interfaces (3 if possible).

Before starting, please be sure to set http/https proxies if your network requires it.
*(Note that `https_proxy` should be set to point to a `http://` URL (not `https://`).
This is an ansible requirement.)*

Pick a machine that is on the management network and has ansible installed
to run the following steps.

The setup scripts use python module *netaddr* and linux utility `bzip2`. If these are not
installed on the machine where you are executing these steps, you must install them
before proceeding. *(E.g. `yum install bzip2; pip install netaddr`)*

Note on *login_userid*: Ansible requires ssh to access the nodes in the cluster for
configuration. This requires a single userid that can log into each of the machines
AND has sudo permission.

###Step 1 Clone the contiv/demo repo

```
git clone https://github.com/contiv/demo
```

###Step 2 Clone the contrib repo

```
cd demo/k8s;

git clone https://github.com/jojimt/contrib -b contiv
```


###Step 3 Fill in cluster info
edit `cluster_defs.json`

See `cluster_defs.json.README` for instructions

If you need ACI integration, edit *aci.yml*. See [here](aci.html) for more details.

###Step 4 Prepare machines

```
./prepare.sh <login_userid>
```
Supply login password when prompted.

###Step 5 Create cluster

```
./setup_k8s_cluster.sh <login_userid>
```
Supply login password when prompted.


**Note**: If you need Layer 3 BGP support use

```
./setup_k8s_cluster <login_userid> contivFwdMode="routing"
```

###Step 6 Verify cluster
```
./verify_cluster.sh <login_userid>
```
Supply login password when prompted.