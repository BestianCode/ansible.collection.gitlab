# BestianCode GitLab Collection

Ansible collection. It ships production-ready roles for running your own GitLab platform:

- **`gitlab`** – installs and configures the GitLab Omnibus package (forked from
  `hifis.toolkit.gitlab`).
- **`gitlab_runner`** – provisions, registers, and manages GitLab Runners (forked
  from `hifis.toolkit.gitlab_runner`).

Use them together to stand up GitLab application nodes and CI runners with a
single collection.

## Installation

Install from Ansible Galaxy (or your artifact cache):

```bash
ansible-galaxy collection install bestiancode.gitlab
```

Alternatively, pin it in `requirements.yml`:

```yaml
collections:
  - name: bestiancode.gitlab
```

Then run:

```bash
ansible-galaxy collection install -r requirements.yml --force
```

## Repository layout

```text
roles/
  gitlab/        # GitLab Omnibus installation + configuration
  gitlab_runner/ # Runner lifecycle management and registration
```

## Playbook

Create a playbook that targets each host group:

```yaml
---
- name: Install GitLab application
  hosts: gitlab_primary
  become: true
  collections:
    - bestiancode.gitlab
  roles:
    - gitlab

- name: Register GitLab runners
  hosts: gitlab_runners
  become: true
  collections:
    - bestiancode.gitlab
  roles:
    - gitlab_runner
```

## Additional documentation

- [`roles/gitlab/README.md`](roles/gitlab/README.md) – full GitLab variable
  reference, supported distributions, and advanced configuration examples.
- [`roles/gitlab_runner/README.md`](roles/gitlab_runner/README.md) – complete
  runner documentation (Docker, shell, Docker Machine, Flatcar, SSH keys,
  session server, etc.).

Issues and discussions live at
<https://github.com/BestianCode/ansible.collection.gitlab>.
