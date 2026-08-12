# APIC-LAB

Ansible playbooks for automating Cisco ACI fabric configuration via the APIC REST API, designed to run on Ansible Tower (AWX).

## What this playbook does

`Tenant.yml` creates the following ACI objects in order:

1. Tenant
2. VRF
3. Bridge Domain 
4. Subnet 
5. Application Profile
6. Endpoint Group 

## Repository structure

```
APIC-LAB/
├── Tenant.yml                   # Main playbook
├── ansible.cfg                  # Ansible configuration
├── group_vars/
│   └── all.yml                  # Non-secret variables (edit these before running)
└── collections/
    ├── requirements.yml         # Collection install instructions
    ├── cisco-aci-2.13.0.tar.gz
    ├── ansible-netcommon-8.6.1.tar.gz
    └── ansible-utils-6.0.3.tar.gz
```

## Prerequisites

- Ansible Tower (AWX) with the `awx-ee` execution environment
- A Tower inventory with your APIC hosts defined
- A Tower credential with your APIC username and password

## Variables

All variables are defined in `group_vars/all.yml`. Update the placeholder values before running:

| Variable | Description |
|---|---|
| `tenant_name` | Name of the ACI Tenant |
| `vrf_name` | Name of the VRF |
| `bd_name` | Name of the Bridge Domain |
| `subnet_gateway` | Gateway IP with prefix e.g. `192.168.1.1/24` |
| `subnet_scope` | `private` or `public` |
| `ap_name` | Name of the Application Profile |
| `epg_name` | Name of the Endpoint Group |


## Collection install note

The `cisco.aci` collection and its dependencies are bundled as tarballs in the `collections/` directory. This allows Tower to install them without requiring outbound internet access to Ansible Galaxy.
