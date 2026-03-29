# Setup Notes

## Setup Context
- Project Name: Phase 2, Project 2 — ASG Segmentation Lab
- Date: March 29, 2026

## Prerequisites
- Access requirements:
  - Active Azure subscription
  - Access to the Azure Portal
  - Stable internet connection
  - A local project folder or repository for saving screenshots and notes
- Tools needed:
  - Azure Portal
  - Azure VM Run Command
  - Web browser
  - Linux commands used inside the VMs:
    - `curl`
    - `nginx`
    - `netcat`
- Required permissions/roles:
  - Permission to create and delete resource groups
  - Permission to create and manage VMs, VNets, NSGs, ASGs, NICs, disks, SSH keys, and public IPs
  - Permission to update NSG rules, ASG membership, and subnet associations

## Baseline Checks
- Current state:
  - No completed ASG segmentation validation existed before the setup.
  - The project required a frontend VM, backend VM, VNet, subnet, NSG, and ASGs to be created and connected first.
- Check command(s):
  - Azure Portal checks for:
    - Resource group existence
    - VNet and subnet existence
    - VM creation status
    - NSG creation status
    - ASG creation status
    - Frontend public IP presence
    - Backend no-public-IP design
- Expected baseline output:
  - The required Azure resources are not yet fully created or configured.
  - The environment is ready for build and configuration.

## Setup Steps
1. Step: Create the resource group and core network and compute resources
   - Action/Command:
     - Create resource group `rg-p2p2-asgseg-lab`
     - Create virtual network `vnet-p2p2-asgseg-lab`
     - Create the subnet inside `vnet-p2p2-asgseg-lab`
     - Create frontend VM `vm-p2p2-asgseg-frontend`
     - Create backend VM `vm-p2p2-asgseg-backend`
     - Create NSG `nsg-p2p2-asgseg-lab`
     - Create ASGs:
       - `asg-p2p2-asgseg-frontend`
       - `asg-p2p2-asgseg-backend`
   - Expected Output:
     - The core resource group and required Azure resources are created successfully.
     - The frontend VM is created with a public IP.
     - The backend VM is created without a public IP.

2. Step: Configure segmentation wiring
   - Action/Command:
     - Associate `nsg-p2p2-asgseg-lab` with the lab subnet
     - Assign the frontend NIC to ASG `asg-p2p2-asgseg-frontend`
     - Assign the backend NIC to ASG `asg-p2p2-asgseg-backend`
     - Create allow rule `allow-frontend-to-backend-http` on `nsg-p2p2-asgseg-lab`
       - Source ASG: `asg-p2p2-asgseg-frontend`
       - Destination ASG: `asg-p2p2-asgseg-backend`
       - Port: `80`
       - Protocol: `TCP`
       - Action: `Allow`
       - Priority: `100`
   - Expected Output:
     - The NSG is associated with the subnet.
     - The frontend NIC is mapped to the frontend ASG.
     - The backend NIC is mapped to the backend ASG.
     - HTTP traffic from the frontend to the backend is explicitly allowed.

3. Step: Install a simple HTTP service on the backend VM
   - Action/Command:
     - Use Run Command on `vm-p2p2-asgseg-backend`
     - Run:
       ```bash
       sudo apt update
       sudo apt install -y nginx
       sudo systemctl enable nginx
       sudo systemctl start nginx
       sudo systemctl status nginx --no-pager
       curl http://localhost
       ```
   - Expected Output:
     - `nginx` is installed successfully on the backend VM.
     - The `nginx` service becomes active and running.
     - `curl http://localhost` returns the default `nginx` page.

4. Step: Validate the allowed traffic path
   - Action/Command:
     - Use Run Command on `vm-p2p2-asgseg-frontend`
     - Run:
       ```bash
       curl http://10.20.1.5
       ```
   - Expected Output:
     - The frontend VM reaches the backend VM private IP `10.20.1.5` on port 80.
     - The backend `nginx` page is returned.

5. Step: Create stronger blocked-path proof
   - Action/Command:
     - Add deny rule `deny-frontend-to-backend-ssh` on `nsg-p2p2-asgseg-lab`
       - Source ASG: `asg-p2p2-asgseg-frontend`
       - Destination ASG: `asg-p2p2-asgseg-backend`
       - Port: `22`
       - Protocol: `TCP`
       - Action: `Deny`
       - Priority: `110`
     - Use Run Command on `vm-p2p2-asgseg-frontend`
     - Run:
       ```bash
       nc -zvw 5 10.20.1.5 22
       ```
   - Expected Output:
     - The frontend VM cannot reach the backend VM on SSH port 22.
     - The connection attempt times out, confirming that unintended traffic is blocked.

## Configuration Details
- Naming pattern:
  - Resource Group:
    - `rg-p2p2-asgseg-lab`
  - Virtual Network:
    - `vnet-p2p2-asgseg-lab`
  - Network Security Group:
    - `nsg-p2p2-asgseg-lab`
  - Application Security Groups:
    - `asg-p2p2-asgseg-frontend`
    - `asg-p2p2-asgseg-backend`
  - Virtual Machines:
    - `vm-p2p2-asgseg-frontend`
    - `vm-p2p2-asgseg-backend`
  - Public IP:
    - `vm-p2p2-asgseg-frontend-ip`
- Region:
  - Southeast Asia
- Tags:
  - Not shown in the provided screenshot
- SKU/Cost choices:
  - Temporary lab-grade resources were used for short-term testing.
  - The frontend VM was given a public IP.
  - The backend VM was intentionally kept private without a public IP.

## Validation
- Verification command(s):
  - Backend local `nginx` validation:
    ```bash
    curl http://localhost
    ```
  - Frontend-to-backend allowed-path validation:
    ```bash
    curl http://10.20.1.5
    ```
  - Frontend-to-backend blocked-path validation:
    ```bash
    nc -zvw 5 10.20.1.5 22
    ```
- Screenshot path(s):
  - `resource-group.png`
  - `vnet-subnet.png`
  - `nsg.png`
  - `asg-frontend.png`
  - `asg-backend.png`
  - `vm-frontend.png`
  - `vm-backend.png`
  - `vm-asg-frontend.png`
  - `vm-asg-backend.png`
  - `nsg-associate-subnet.png`
  - `nsg-rule-allow-frontendtobackend-http.png`
  - `success-frontend-backend-connection.png`
  - `nsg-rule-deny-port22.png`
  - `denied-port22.png`
- Success criteria:
  - The frontend VM NIC is assigned to the Frontend ASG.
  - The backend VM NIC is assigned to the Backend ASG.
  - `nsg-p2p2-asgseg-lab` is associated with the subnet.
  - `vm-p2p2-asgseg-frontend` has public IP `vm-p2p2-asgseg-frontend-ip`.
  - `vm-p2p2-asgseg-backend` has no public IP.
  - `nginx` is running on the backend VM.
  - The frontend reaches the backend on port 80.
  - The frontend cannot reach the backend on port 22 after the deny rule is applied.

## Risks and Notes
- Risk:
  - Azure’s default `AllowVnetInBound` rule can still allow same-VNet traffic if no explicit deny rule blocks it.
  - Mitigation:
    - Do not overclaim that the custom allow rule alone proves segmentation.
    - Use explicit deny validation on port 22 for stronger proof.

- Risk:
  - Private `.pem` key files may be accidentally uploaded to a public repository.
  - Mitigation:
    - Do not upload `.pem` files.
    - Add `*.pem` and `*.key` to `.gitignore`.
    - Treat previously exposed old keys as compromised and do not reuse them.
