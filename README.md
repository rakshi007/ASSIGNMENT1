# ASSIGNMENT1
Nimesa Technology Pvt. Ltd
# main.tf

provider "aws" {
  region = "us-east-1a" \}

resource "aws_vpc" "my_vpc" {
  cidr_block = "10.0.0.0/16" 
}

resource "aws_subnet" "public_subnet" {
  vpc_id     = vpc-0b62696160717da94
  cidr_block = "10.0.0.0/24" 
  Map_public_ip_on_launch = true
}

resource "Aws_subnet" "Private_subnet" {
  vpc_id     = vpc-0b62696160717da94
  cidr_block = "10.0.1.0/24" 
}

resource "aws_security_group" "my_security_group" {
  name_prefix = "PublicSG"
  
  
  ingress {
    from_port   = 22
    po_port     = 80
    protocol    = "TCP"
    cidr_blocks = ["0.0.0.0/0"] 
  }


  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "ALL"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

resource "aws_instance" "my_instance" {
  ami           = "ami-051f7e7f6c2f40dc1" # Replace with your desired AMI ID
  instance_type = "t2.micro"
  subnet_id     = subnet-0bce63ab0421564d5
  root_block_device {
    volume_type           = "gp2"
    volume_size           = 8
    delete_on_termination = true
  }

  tags = {
    Name    = "MyEC2Instance"
    purpose = "Assignment"
  }

  Security_groups = []
}
