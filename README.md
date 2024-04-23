# Server Secuity Best Practices

*1. Establish and Use a Secure Connection*

When connecting to a remote server, it is essential to establish a secure channel for communication.

The SSH (Secure Shell) Protocol is the best way to establish a protected connection. Unlike the previously used Telnet, SSH access encrypts all data transmitted in the exchange. To gain remote access using the SSH protocol, you must install the SSH Daemon and an SSH Client to issue commands and manage servers.

By default, SSH uses port 22. Changing the default port number is an easy way to reduce the chances of hackers attacking your server. Therefore, the best practice for SSH is to use a random port number between 1024 and 32,767.

Please see steps on how to change SSH port

2. Create a new user account and grant it sudo privileges
When you first install Ubuntu Server, the default user account is called “root”. This account has full access to all system files and settings. However, it’s not recommended to use this account for day-to-day activities because if someone were to gain access to your server, they would have unrestricted access to everything.

By creating a new user account with sudo privileges, you can limit the amount of damage that could be done in the event of an attack. You can also easily revoke or change the permissions of the new user account without affecting the root account.

Please see steps on how to create a new user account and grant it sudo privileges

3. Use SSH Keys Authentication
Instead of a password, you can authenticate an SSH server using a pair of SSH keys, a better alternative to traditional logins. The keys carry substantially more bits than a password, and current computers cannot easily crack them. For example, the popular RSA 2048-bit encryption is equivalent to a 617-digit password.

The SSH key pair consists of a public key and a private key.

The public key has several copies, one of which remains on the server, while others are shared with users. Anyone with the public key has the ability to encrypt data, while only the user with the corresponding private key can read this data.

The private key must not be shared with anyone and must be kept secure. When establishing a connection, the server asks for evidence that the user has the private key before allowing privileged access.

Please see steps on Generate SSH Keys

4. Disabling password authentication on your server
If you were able to log into your account using SSH without a password, you have successfully configured SSH-key-based authentication to your account. However, your password-based authentication mechanism is still active, meaning that your server is still exposed to brute-force attacks.

Before completing the steps in this section, make sure that you either have SSH-key-based authentication configured for the root account on this server, or preferably, that you have SSH-key-based authentication configured for a non-root account on this server with sudo privileges. This step will lock down password-based logins, so ensuring that you will still be able to get administrative access is crucial.

Note: If you provided an SSH key when creating your DigitalOcean droplet, password authentication may have been automatically disabled. You can still verify this by reading on.

Please see steps on how to disabling password authentication on your server


5. Set up a firewall

A firewall is a security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It helps protect your server from malicious attacks, unauthorized access, and other threats.

Setting up a firewall in Ubuntu is easy with the Uncomplicated Firewall (UFW). UFW is an interface for managing iptables, which is the Linux kernel’s built-in packet filtering framework. To set up a firewall using UFW, you’ll need to install it first. Then, you can configure the firewall by setting up rules for allowing or denying certain types of traffic. Finally, you can enable the firewall so that it starts protecting your server.

Please see steps on how to set up a firewall


6. Install fail2ban to protect SSH
SSH is the most common way to access a server, and it’s also one of the most vulnerable. Hackers can use brute force attacks to guess passwords and gain access to your system.

Fail2ban is an open source tool that monitors log files for failed login attempts and then blocks the IP address associated with those attempts. This helps protect your server from malicious actors who are trying to gain unauthorized access. It’s easy to install and configure, so there’s no excuse not to have it running on your Ubuntu server.

Please see steps on how to install fail2ban to protect SSH

7. Close Hidden Open Ports
Open ports may reveal network architecture information while extending attack surfaces. Therefore, ports that aren’t absolutely essential should be closed with haste. The netstat command can be used to determine which ports are listening while also revealing the details of connections that may currently be available.

The below command lines can be utilized to find specific ports:

All TCP ports — “netstat -at”
All UDP ports — “netstat -au”
All listening ports — “netstat -l”
Information for all ports — “netstat -s”

We can use UFW to deny hidden ports or whitelist ip for specific ports. Please refer to this UFW documentation:

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04
