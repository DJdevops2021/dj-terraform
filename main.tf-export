#main.tf
#Cofigure the AWS provider
provider "aws" {
   region = "us-west-2"
}
#create a VPC
resource "aws_vpc" "myvpc1" {
  cidr_block = "10.0.0.0/16"
  tags = {
      Name = "vpc25"
      environment = "dev"
  }
}
resource "aws_instance" "webserver" {
    ami = "ami-0b28dfc7adc325ef4"
    instance_type = "t2.micro"
    tags = {
    Name = "WebServer1"
    Envrionment = "stage"
  }
}
resource "aws_s3_bucket" "jomias3" {
  bucket = "jomiadevops"
  acl    = "private"

  tags = {
    Name        = "myjomiabucket"
    Environment = "Dev"
  }
}
# Block-8: **Modules Block**
# AWS EC2 Instance Module

module "ec2_cluster" {
  source                 = "terraform-aws-modules/ec2-instance/aws"
  version                = "~> 2.0"

  name                   = "my-modules-demo"
  instance_count         = 2

  ami                    = "ami-0b28dfc7adc325ef4"
  instance_type          = "t2.micro"
  key_name               = "terra"
  monitoring             = true
  vpc_security_group_ids = ["sg-0ac99d9f135a1befd"]
  subnet_id              = "subnet-0fb1e6a385530dbe9"
  user_data              = file("tomcat.sh")
  tags = {
    Terraform   = "true"
    Environment = "dev"
  }
}

resource "aws_instance" "app" {
    ami = "ami-08a5b9e0df0f9bc82"
    instance_type = "t2.micro"
}
resource "aws_instance" "application" {
    ami = "ami-0b28dfc7adc325ef4"
    instance_type = "t2.micro"
    tags = {
      Name = "DJ"
    }
}

