# Execution Environment Creation with Podman

This repository provides the necessary configuration and scripts to build and run an Ansible execution environment using **Podman**. The environment is designed to work with Red Hat's `ansible-automation-platform-2.5-for-rhel-9-x86_64-rpms` or `ansible-developer-1.2-for-rhel-9-x86_64-rpms` repositories, which require a valid Red Hat subscription for access.

## Prerequisites

Before using this repository, ensure the following are installed on your system:

### Install Podman and Container Tools

To install **Podman** and its associated tools, use the `container-tools` group package. This will include **Podman**, **Buildah**, **Skopeo**, and related utilities.

```bash
sudo dnf install -y container-tools
```

### Install Ansible

Ensure that Ansible is installed via Red Hat's ansible-automation-platform-2.5-for-rhel-9-x86_64-rpms or ansible-developer-1.2-for-rhel-9-x86_64-rpms repository. You'll need a valid Red Hat subscription to access these repositories.

```bash
sudo subscription-manager repos --enable=ansible-automation-platform-2.5-for-rhel-9-x86_64-rpms
sudo dnf install -y ansible-navigator ansible-builder ansible-core
```
### Podman Login to Container Registry

You need to log in to Red Hat's registry (registry.redhat.io)

```bash
podman login registry.redhat.io --username <your_username>
```

### Build the execution environment container

```bash
ansible-builder build --tag quay.io/automationiberia/osbuildee:1.0
```

### Log in to your container registry and push the image

```bash
podman login quay.local --username silvinux --tls-verify=false
podman push quay.io/automationiberia/osbuildee:1.0 --tls-verify=false
```

### Copy to disconnected environment

```bash
podman save -o osbuildee-1.0.tar quay.io/automationiberia/osbuildee:1.1
```



