Ansible Role: Uptime-Kuma-docker
================================

Install Uptime-Kuma Docker Compose project.

- https://github.com/louislam/uptime-kuma

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

uptime_kuma_project_name: uptime-kuma

# Docker project dynamic vars (uses `docker_project_name` prefix, adapt if overriden)

uptime_kuma_traefik_loadbalancer_server_port: 3001
uptime_kuma_traefik_middlewares:
  - "internal-access@file"
  - "allow-frames@file"
  - "{{ docker_project_slug }}-cors@docker"

# Main service additional docker-compose options (ex: cpu_shares, deploy, ...)
uptime_kuma_compose_service_additional_options: |
  #ports:
  #  - "3001:3001"


# Uptime-Kuma project variables

# louislam/uptime-kuma container version
uptime_kuma_version: 1
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: true
  gather_subset:
    - "!all"
    - "!min"
    - user_id

  roles:
    - djuuu.uptime_kuma_docker
```

License
-------

Beerware License
