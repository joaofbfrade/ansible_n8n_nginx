# Ansible Script to deply N8N with Nginx as reverse proxy

This README provides a guide on how to use the provided Ansible playbook to deploy and configure Docker containers for n8n (a workflow automation tool) and Nginx as a reverse proxy.

## Requirements

- **Ansible**: You must have Ansible installed on your local machine or on a control node that will execute the playbook.

## Setup

1. **Variables**: Define necessary variables in the `vars.yml` file. This file should include any user-specific or environment-specific variables.

2. **Certificates**: Place your SSL certificates in the `certs` directory relative to your playbook directory. These certificates will be used by the Nginx container to serve HTTPS traffic.

## Running the Playbook

Execute the playbook using the following command:

```bash
ansible-playbook your-playbook-name.yml
```

This command will start the deployment process as defined in the playbook tasks. Here's a brief overview of what each task accomplishes:

- **Install Docker Engine and CLI**: Installs Docker and Docker Compose on the target host.
- **Start Docker Service**: Ensures the Docker service is started and enabled to start on boot.
- **Docker Setup**: Pulls the required Docker images for nginx and n8n, creates a Docker network and volumes for persistent storage.
- **Run Containers**: Deploys n8n and Nginx containers. N8n will be accessible through Nginx which acts as a reverse proxy, forwarding requests to n8n on port 5678.
- **Nginx Configuration**: Deploys a custom Nginx configuration tailored to act as a reverse proxy for n8n, and ensures that the default Nginx configuration is absent.

## Additional Notes

- Ensure the playbook is run with administrative privileges (`become: yes`) to allow Ansible to perform operations that require root access.
- Modify the `n8n.conf` and SSL certificate paths as per your setup requirements or security policies.
- The playbook assumes all tasks execute on `localhost`. If deploying to remote hosts, update the `- hosts` field in the playbook and ensure you have SSH access configured.
