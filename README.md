# spinup-ai

## Pre-Requisites

Before using this repository, ensure you have the following:

### 1. OpenShift Cluster

- You must have access to a running OpenShift cluster.
- You need the `kubeadmin` credentials for cluster administration.

### 2. Ansible and ansible-playbook

- Install Ansible on your local machine (macOS/Linux):
  ```sh
  pip install --user ansible
  ```
- Or, using Homebrew on macOS:
  ```sh
  brew install ansible
  ```
- Verify installation:
  ```sh
  ansible --version
  ansible-playbook --version
  ```

### 3. OpenShift CLI (`oc`)

- Install the OpenShift CLI
  - [Official documentation](https://docs.openshift.com/container-platform/latest/cli_reference/openshift_cli/getting-started-cli.html).
  - Download [Link](https://access.redhat.com/downloads/content/290/ver=4.18/rhel---9/4.18.13/x86_64/product-software)
- Verify installation:
  ```sh
  oc version
  ```

---

## Repository Layout

- **components/**  
  Contains kustomize manifests and configuration files for deploying cluster components such as cluster prerequisites, admin user, GPU operators, RHOAI operators etc.

- **demos/**  
  Demo files for running inference and showcasing RHOAI capabilites.

- **playbooks/**  
  Ansible playbooks for automating the setup and configuration of the Openshift cluster with RHOAI components, including user creation, prerequisites, GPU setup, Serverless and Servicemesh and other orchestration scripts.

---

## Ansible Playbooks

Below are the main Ansible files under the `playbooks/` directory (top-level only):

### Setup

- **cluster-setup.ansible.yml**  
  Orchestrates the full cluster setup:

  - Cluster pre-reqs
  - Add user with cluster-admin role
  - Provision and configure GPU node
  - Install NFD and NIVIDIA GPU operator
  - Install Serverless and Servicemesh operator
  - Install RHOAI and depdendent components

  **Run with:**

  ```sh
  ansible-playbook playbooks/setup-cluster.ansible.yml
  ```

- **gpu-setup.ansible.yml**  
  Provision and configure GPU node:

  - Add GPU node
  - Install NFD and NVIDIA GPU operator
  - Install NVIDIA DCGM dashboard
  - Configure timeslicing in GPU
  - Taint GPU nodes

  **Run with:**

  ```sh
  ansible-playbook playbooks/gpu-setup.ansible.yml
  ```

- **minio-setup.ansible.yml**  
  Provision MINIO object storage

  **Run with:**

  ```sh
  ansible-playbook playbooks/minio-setup.ansible.yml
  ```

### Demos

- **demo-vllm.ansible.yml**  
  Demo model serving on vLLM:

  - Install MINIO storage
  - Create DataScience project
  - Create data-connections
  - Create ServingRuntime
  - Create InferenceService

  **Run with:**

  ```sh
  ansible-playbook playbooks/demo-vllm.ansible.yml
  ```
