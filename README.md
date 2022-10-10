[![CI](https://github.com/de-it-krachten/ansible-role-hashicorp/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-hashicorp/actions?query=workflow%3ACI)


# ansible-role-hashicorp

Install hashicorp products 



## Dependencies

#### Roles
None

#### Collections
- community.general

## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# product name
hashicorp_product: "{{ role_name }}"

# product platform
hashicorp_platform: "{{ ansible_system | lower }}"

# product architecture
hashicorp_arch: "{{ 'amd64' if ansible_architecture == 'x86_64' else ansible_architecture }}"

# product install mode (binary or package)
hashicorp_install_mode: package

# product zip filename
hashicorp_zip: >-
  {{ hashicorp_product }}_{{ hashicorp_product_version }}_{{ hashicorp_platform }}_{{ hashicorp_arch }}.zip

# product download url
hashicorp_product_url: >-
  https://releases.hashicorp.com/{{ hashicorp_product }}/{{ hashicorp_product_version }}/{{ hashicorp_zip }}
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'hashicorp'
  hosts: all
  tasks:
    - name: Include role 'hashicorp' (package)
      include_role:
        name: hashicorp
      vars:
        hashicorp_product: "{{ item }}"
      loop:
        - terraform
        - vagrant
        - terraform
        - packer
        - consul
        - vault
        - nomad

    - name: Include role 'hashicorp' (binary)
      include_role:
        name: hashicorp
      vars:
        hashicorp_product: "{{ item }}"
        hashicorp_install_mode: binary
      loop:
        - terraform
        - vagrant
        - terraform
        - packer
        - consul
        - vault
        - nomad
</pre></code>
