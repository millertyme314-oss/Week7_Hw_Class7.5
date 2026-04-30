# Week7_Hw_Class7.5
A step-by-step deployment of cloud infrastructure via Terraform &amp; troublshooting

## Programs & Tools used:
- GitBash
- Google Chrome browser
    - (Github.com)
    - (Hashicorp website)
- Google Cloud console
- Terraform
- Visual Studio Code
- Windows Notepad
- Windows Snipping tool

## Mission:
Deployment demonstration process to build muscle memory and prevent errors.

Process:
    
    1.  Authenticate: gcloud auth application-default login
    2.  Copy File: Create a new .tf file in VS Code and paste the "Raw" content from the repo.
    3.  Review & Modify: Verify the code and make necessary changes (e.g., project ID, port numbers).
    4.  Deploy: Run terraform plan → terraform apply.

Resources Deployed:

    NAT Router: A GCP router is a prerequisite for the NAT service.
    Firewall Rules: Deployed incrementally for SSH (22/TCP), HTTP (80/TCP), HTTPS (443/TCP), and ESP (500/UDP).
    Compute Instance (VM): A VM with an inline startup script to install Nginx.
    Outputs: An outputs.tf file to retrieve the VM's name, IP, and SSH command directly from the terminal.

## Troubleshooting:
Deployment 

## Deliverables:
Deployment 
