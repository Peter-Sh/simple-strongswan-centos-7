# Setup your own ipsec vpn server using strongswan

This ansible role helps to setup simple strongswan vpn on a dedicated centos-7 server.

I've made it for private usage, but decided to publish it to help my friends to setup vpn servers.

Use it on your own risk.

The work is based on this [post](https://habr.com/post/250859/) (russian) by ValdikSS.

## Installation

Create `requiments.yml` file or add this lines to existing file.

```
# req.yml
- src: git+https://github.com/Peter-Sh/simple-strongswan-centos-7.git
  version: master
```

Install the role:
```
ansible-galaxy install -r req.yml
```

## Usage

Simple playbook example.


The example playbook will:
* setup strongswan server using RSA based certificates for authentication.
* setup NAT and packet forwarding in iptables.

Certificates are expected to be in `pki_dir` and created with [easy-rsa-ipsec tool](https://github.com/ValdikSS/easy-rsa-ipsec) by ValdikSS.
You can setup your PKI using this tool or a simple [role](https://github.com/Peter-Sh/simple-strongswan-setup-pki).

At least ca.crt and server certificate for `your.vps.domain.name` should be created.

```
- hosts: your.vps.domain.name
  tasks:
  roles:
  - role: simple-strongswan-centos-7
    swan_fqdn: your.vps.domain.name
    pki_dir: /home/user/easy-rsa/easyrsa3/pki
```
