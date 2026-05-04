# Week7_Hw_Class7.5
A step-by-step deployment of cloud infrastructure via Terraform &amp; troubleshooting

## Programs & Tools used:
- GitBash
- Google Chrome browser
    - (Github.com [Theo's SEIR-1 Repo])
    - (Hashicorp website [Terraform Registry])
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

    - NAT Router: A GCP router is a prerequisite for the NAT service.
    - Firewall Rules: Deployed incrementally for SSH (22/TCP), HTTP (80/TCP), HTTPS (443/TCP), and ESP (500/UDP).
    - Compute Instance (VM): A VM with an inline startup script to install Nginx.
    - Outputs: An outputs.tf file to retrieve the VM's name, IP, and SSH command directly from the terminal.

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
- Successful deployment of terraform showing the output and file created [(here)](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/successful-deploy-tf.png)
- In one folder called “infra” or “terraform” or similar containing terraform code [(here)](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/infra-folder.png)
- Provider terraform configuration file with the latest version of the Google provider [(here)](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/providers-proof-file.png)
- Use a .gitignore {remote backend is commented out} [(here)](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/gitignore-no-backend.png)
- GCP VPC terraform configuration file using example code from the Terraform Registry  [(here)](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/vpc-proof.png)
- [Text file](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/fav_food_text_file.png) made by terraform from the [local_file resource](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/local_file-resource.png) with your favorite food in it
- Output block of your VPC’s name in GCP using Terraform [(here)](https://github.com/millertyme314-oss/Week7-visual-proof/blob/main/Vpc-name-output-block.png)
