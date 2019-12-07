# 101-terraform-workshop
Repository for terraform workshop given by Anuj Jain @ajain-ee.


# step-1 : verify local setup
1. Run **terraform version** on the command line and verify it is 0.12.16. 
2. Get your AWS account access key and access secret ready.
3. Fork repository https://github.com/ajain-ee/101-terraform-workshop.git .
4. Checkout branch “step-1”.
5. Replace aws key and aws secret variable 
6. Run **terraform init**
7. Run **terraform plan**
8. Commit your changes on branch step-1.
9. Merge step-1 branch into master

# step-2 : Launch first ec2 instance on AWS
1. Checkout branch "step-2" and rebase with master. 
2. Extract hardcode access_key into variables like this:
   
   ```
    variable "aws_access_key" {
      default = ""
    }
    access_key = var.aws_access_key
    ``` 
3. Replace all other hardcoded values as well with variables.    
4. Set ami value to appropriate ami available in choice of region. 
   I am setting public ubuntu available in eu-east-1 "ami-04b9e92b5572fa0d1"
5. Set keyname and public_key value is your any open-ssh formatted public key. Using
   this key you can ssh into ec2 box.
6. Set subnet id from default vpc in your aws region.
7. Run **terraform plan**
8. Run **terraform apply**
9. Verify ec2 instance by doing ssh into ec2-instance using command.
   `
   ssh -i <path-to-private-key> ubuntu@public-ip-address-of-ec2-instance
   `    
10. Commit and Merge step-2 branch into master.   

# step-3 : Store terraform state into S3
1. Checkout branch "step-3" and rebase with master. 
2. Create a bucket "terraform-workshop" in you account. 
3. Set the following variables in terraform backend configuration
   ```
   backend "s3" {
       bucket = "terraform-workshop"
       region = ""
       key = "workshopstate/terraform.tfstate"
   }    
   ```     
4. Run **terraform init**, terraform will prompt your for state migration from local
   to remote location. press yes for migration. 
   
5. Run **terraform plan**
6. Run **terraform apply**
7. Commit and Merge step-3 branch into master.       

# step-4 : Store terraform state into S3
1. Checkout branch "step-4" and rebase with master. 
2. Run **terraform destroy** and approve the destruction and start fresh.
3. update the key value pairs with your openssh public key, this will be used to ssh into ec2 instance launch in public subnet.
4. Run **terraform plan** 
5. Run **terraform apply**
6. Go to AWS Console and verify your vpc and subnets are created.
7. Go EC2 service and verify 2 instance are running.
8. SSH into public ec2 instance with ssh key.
9. Commit and Merge step-4 branch into master.       

# step-4 : install apache2 using ec2 instance user data
1. Checkout branch "step-5" and rebase with master. 
2. Check the install-apache.tpl and see it usage in ec2 instance first instance user data.
3. Run **terraform plan** 
4. Run **terraform apply**
5. Get the public ip and terrform output and open ip in browser. You should greeting message from install apache file in browser.
6. Commit and Merge step-5 branch into master.