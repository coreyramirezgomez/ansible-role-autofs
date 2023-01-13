AutoFS
=========

Install and configure autofs.

## Requirements

- Full privileges to install packages on target host.
- Full privileges to write to protected files under /etc/

## Example Playbook

    - hosts: afp_hosts
      roles:
        - role: crg.autofs
          autofs_mounts:
            "docs":
              mounts:
                - target_path: "/misc/docs"
                  source_servers:
                    - "10.0.0.10"
                  source_path: "/mnt/docs"
                  connection_opts: "-rw,soft,intr,rsize=8192,wsize=8192"
              target_root_path: "/-" # denotes direct mount.
            "home":
              mounts:
                - target_path: "*"
                  source_servers:
                    - "nfs.example.net"
                  source_path: "/mnt/homes/&"
              target_root_path: "/home"
