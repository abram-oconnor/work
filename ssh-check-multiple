#!/bin/bash

# Check if sshpass is installed
if ! command -v sshpass &> /dev/null; then
    echo "sshpass is not installed. Attempting to install sshpass..."
    
    # Attempt to install sshpass using yum
    sudo yum install -y sshpass
    
    # Verify installation was successful
    if ! command -v sshpass &> /dev/null; then
        echo "Failed to install sshpass. Please install it manually and try again."
        exit 1
    else
        echo "sshpass installed successfully."
    fi
fi

# Get user input for username and password
read -p "Enter username: " username
read -s -p "Enter password: " password
echo

# Get the list of IP addresses (comma or space-separated)
read -p "Enter IP addresses (separate multiple IPs with spaces or commas): " ip_list

# Convert comma-separated IPs to space-separated
ip_list=$(echo $ip_list | tr ',' ' ')

# Loop over each IP address and attempt SSH
for ip_address in $ip_list; do
    echo "Attempting SSH to $ip_address..."
    sshpass -p "$password" ssh -o StrictHostKeyChecking=no "$username@$ip_address"
    
    # Optionally add a delay between connections to avoid overwhelming the remote servers
    # sleep 1
done
