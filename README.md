# terraform_eks
Creates an EKS cluster with auto scaling of node group. 

There are two modules 1) for networking 2) for EKS

Example Usage:

module "vpc" {
  source           = "./vpc"
  vpc_cidr         = CIDR of VPC - e.g."10.1.0.0/16"
  max_subnet       = Total subnets to creat - 2
  public_sn_count  = Total Public Subnets - 2
}

module "eks" {
  source         = "./eks"
  vpc_id         = ID of your VPC - module.vpc.vpc_id
  key_pair       = Key Pair to ssh to nodes - e.g "my_key_pair"
  instance_types = Instance type - ["t3.small"]
  desired_size   = 2
  min_size       = 1
  max_size       = 5
  public_subnets = module.vpc.public_subnets
}
