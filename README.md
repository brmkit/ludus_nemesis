# ludus_nemesis

An Ansible role that installs [Nemesis](https://github.com/SpecterOps/Nemesis), a streamlined pipeline created by [SpecterOps](https://specterops.io/) that ingests, enriches and triages files collected during red-team engagements and offensive operations. One of the best companion tools for red team fellows out there.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    nemesis_port: 7443
    nemesis_install_dir: /home/{{ ansible_user }}/nemesis
    tika_ocr_languages: "eng chi_sim chi_tra jpn rus deu spa"

## Example Playbook

```yaml
- hosts: nemesis_host
  roles:
    - brmkit.ludus_nemesis
  vars:
    nemesis_port: 7443
    nemesis_install_dir: /home/{{ ansible_user }}/nemesis
    tika_ocr_languages: "eng chi_sim chi_tra jpn rus deu spa"
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-nemesis"
    hostname: "{{ range_id }}-nemesis"
    template: ubuntu-24.04-x64-server-template
    vlan: 10
    ip_last_octet: 11
    ram_gb: 12
    cpus: 4
    linux: true
    testing:
      snapshot: false
      block_internet: false
    roles:
      - geerlingguy.docker
      - brmkit.ludus_nemesis
```

## License

GPLv3

## Author Information

This role was created by [brmkit](https://github.com/brmkit), for [Ludus](https://ludus.cloud/).
