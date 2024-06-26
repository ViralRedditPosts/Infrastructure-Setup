# Infrastructure-Setup

This repo contains code necessary to spin up general infrastructure resources for this project. This includes DynamoDB, S3, and pushing a config file to S3. 

**You must make a copy of `example_reddit.cfg` and rename it to `reddit.cfg` and replace the contents with your own values before starting.**

## How to use

1. Installs - see the [prerequisites section on this page](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build#prerequisites) for additional information, the steps are essentially:
    1. Install Terraform CLI
    2. Install AWS CLI and run `aws configure` and enter in your aws credentials.
2. Clone this repository 
3. From within this repository run the following:
  
    ```sh
    terraform init
    terraform workspace new dev
    terraform plan -var-file="dev.tfvars" -out=dev-plan.out
    terraform apply -var-file="dev.tfvars" dev-plan.out
    ```

    For deploying to prd

    ```sh
    terraform workspace new prd  # or terraform workspace select prd if already created
    terraform plan -var-file="prd.tfvars" -out=prd-plan.out
    terraform apply -var-file="prd.tfvars" prd-plan.out
    ```

## Notes

Although [Reddit-Scraping](https://github.com/ViralRedditPosts/Reddit-Scraping) depends on this repo, I decided to make this a separate repo because I wanted to reduce the likelihood that a table is dropped while developing and using the scraping infrastructure.