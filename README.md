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
      - ludus_nemesis
    role_vars:
      docker_daemon_options:
        min-api-version: '1.24'
      docker_edition: ce
      docker_users:
        - localuser
```

> [!WARNING]
> There is a issue with the last version of Docker and the traefik container in Nemesis, so you must explicitly set `min-api-version` in the daemon config to avoid failures. [\[1\]](https://www.docker.com/blog/docker-engine-version-29/) [\[2\]](https://community.traefik.io/t/traefik-stops-working-it-uses-old-api-version-1-24/29019/11)

## License

GPLv3

## Author Information

This role was created by [brmkit](https://github.com/brmkit), for [Ludus](https://ludus.cloud/).
