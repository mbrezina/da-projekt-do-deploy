# da-projekt-do-deploy
Example of DigitalOcean deployment for Czechitas DA: Projekt


## How to create environment using Terraform

#### Prepare your DigitalOcean account

1. Sign-up
1. Create an API token: Account -> API -> Tokens/Keys -> Generate New Token
1. Create an SSH key: Account -> Settings -> Security -> Add SSH Key. 
This key will be used to authenticate SSH connection to the server. 
You will need name of this key later.


#### Install and configure Terraform

1. Install [Terraform](https://www.terraform.io/) - in short after you get the zip file, unzip it move the binary file terraform to the /usr/local/bin/ directory.
1. Install SSH agent and import your SSH key to it. It must be running when you execute `terraform apply`. 
Terraform will establish SSH connection to the new server, and it doesn't support password protected SSH keys. So we need SSH agent. 
You can check whether the ssh agent is already running on your computer with this Bash script that can bet put in the commandline:

    if ps -p $SSH_AGENT_PID > /dev/null
    then
    echo "ssh-agent is already running"
    else
    eval ssh-agent -s
    fi

1. Create 'terraform' directory and move into it
1. Run `terraform init` - this will initialize local state storage.
1. You will use 2 files  

(1) variables.tf:

// your DigitalOcean API token
variable "do_token" {
  default = "your_token"
}
