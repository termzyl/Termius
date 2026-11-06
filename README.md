# Termius

## Introduction

Termius is a cross-platform SSH client designed for secure remote server access, terminal management, and infrastructure administration. Available for Windows, macOS, Linux, Android, and iOS, Termius provides a unified environment for managing SSH connections, executing remote commands, transferring files, and maintaining server configurations. It is commonly used by system administrators, DevOps engineers, developers, and IT professionals working with Linux servers, cloud infrastructure, and distributed systems.

The application supports SSH authentication using passwords and public-key cryptography, including reusable credentials stored in its integrated keychain. Users can organize remote hosts into groups, configure connection parameters, and establish encrypted sessions without repeatedly entering server addresses or authentication details. SSH host key verification helps detect unexpected changes in remote server identities.

Termius includes an integrated terminal with command autocomplete, session management, and reusable command snippets. Its SFTP functionality enables secure file uploads, downloads, and remote directory navigation over SSH. Port forwarding provides encrypted access to network services that are not directly exposed to external connections.

For infrastructure management across multiple devices, Termius offers encrypted synchronization of connection settings and credentials through its vault functionality. Workspace features help organize multiple terminal sessions for recurring administrative tasks.

Typical use cases include remote Linux server administration, application deployment, troubleshooting, configuration management, log inspection, and secure database access. Feature availability may vary by platform and subscription plan, particularly for advanced synchronization, collaboration, and productivity capabilities.

## How to Configure Termius SSH Connections and SSH Key Authentication

Configuring an SSH connection in Termius requires a reachable remote server, an SSH service, and valid authentication credentials. The default SSH port is TCP 22, although administrators may configure an alternative port to meet infrastructure requirements.

To establish a remote SSH connection:

1. Open Termius and navigate to the Hosts section.
2. Create a new host entry and assign a descriptive label, such as `production-web-01`.
3. Enter the server's IP address or DNS hostname.
4. Specify the SSH port and remote username.
5. Select password authentication or an SSH key identity.
6. Save the host configuration and initiate the connection.
7. Verify the server's SSH host key fingerprint before trusting it.

For production environments, SSH key authentication is generally preferable to reusable passwords. Termius provides a Keychain for managing SSH keys and authentication identities. Administrators can import an existing private key or create an appropriate key pair, then configure the remote account to recognize the corresponding public key.

On a Linux server, public keys are normally stored in:

`~/.ssh/authorized_keys`

The SSH daemon must permit public-key authentication, and directory permissions must satisfy the server's security requirements.

For environments containing multiple servers, organize hosts into logical groups such as development, staging, and production. This reduces configuration errors and simplifies connection management.

If authentication fails, verify the username, SSH service status, network connectivity, key permissions, and server authentication settings. Connection timeouts typically indicate firewall, routing, DNS, or network availability problems rather than invalid credentials.

## Termius SFTP File Transfer, SSH Port Forwarding, and Remote Server Management

Termius provides integrated tools for transferring files, accessing private network services, and executing recurring server administration commands. These capabilities support common DevOps workflows without requiring separate terminal and file transfer applications.

The built-in SFTP client operates over SSH, allowing administrators to browse remote directories and securely upload or download files. For example, a developer can connect to a Linux application server, navigate to `/var/www/html`, upload deployment assets, and inspect the resulting directory structure.

File operations depend on the remote user's filesystem permissions. Administrative changes to protected directories may require a separate privileged shell session.

SSH port forwarding enables encrypted communication with services accessible from a remote server. Local port forwarding is particularly useful for accessing internal databases or monitoring interfaces.

For example, a local forwarding configuration can map:

- Local endpoint: `127.0.0.1:15432`
- Remote destination: `127.0.0.1:5432`
- SSH gateway: `database-gateway`

Once the tunnel is established, a local PostgreSQL client can connect through port `15432` to reach the remote database service without exposing PostgreSQL directly to the internet.

Termius also supports reusable command snippets for common maintenance operations. Commands such as `systemctl status nginx`, `journalctl -u nginx`, and `df -h` can be saved for repeated execution during troubleshooting.

For multi-server administration, saved hosts, terminal sessions, and workspace organization simplify switching between environments. Administrators should verify the active host before executing destructive commands and restrict SSH credentials and forwarding permissions according to operational security policies.
