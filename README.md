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
Problem: The VM's Nginx server was not accessible via its external IP.

Diagnosis: curl localhost on the VM succeeded, confirming the issue was not the script itself, but how Terraform parsed it.

    Root Causes:  
    1.  Indentation: The EOT marker in the HereDoc operator was misaligned, causing a parsing error.
    2.  Line Endings: The script used Windows CRLF line endings, which Linux VMs do not recognize.

Solution:
    
    1.  Fix Indentation: Align EOT with the start of the metadata block (no spaces).
    2.  Change Line Endings: In VS Code, change the file's line ending from CRLF to LF.
    3.  Re-deploy: Use terraform taint to force a VM recreation, then terraform apply.

*Best Practice: Use the file() function to read startup scripts from a separate .sh file, avoiding these parsing issues.*

## Deliverables:
- Successful deployment of terraform showing the output and file created
- In one folder called “infra” or “terraform” or similar containing terraform code
- Provider terraform configuration file
- Use a .gitignore
- GCP VPC terraform configuration file
- Text file made by terraform from the local_file resource
- Output block of your VPC’s name in GCP
