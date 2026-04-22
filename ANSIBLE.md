# Ansible Usage

## Variables

```yaml
nginx_modules_version: "v1.28.0-1"
nginx_modules_dir: /usr/lib/nginx/modules
```

Derive OS and arch from host facts:

```yaml
- name: Set OS codename and arch
  ansible.builtin.set_fact:
    nginx_modules_os: "{{ ansible_distribution_release }}"
    nginx_modules_arch: "{{ 'arm64' if ansible_architecture == 'aarch64' else 'amd64' }}"
```

## Download and Install

```yaml
- name: Download and extract nginx modules
  ansible.builtin.unarchive:
    src: "https://github.com/<owner>/<repo>/releases/download/{{ nginx_modules_version }}/nginx-modules-{{ nginx_modules_os }}-{{ nginx_modules_arch }}.tar.gz"
    dest: "{{ nginx_modules_dir }}"
    remote_src: true
    owner: root
    group: root
    mode: "0644"
  notify: Reload nginx
```

Replace `<owner>/<repo>` with your GitHub repository path.

## Nginx Configuration

```nginx
load_module modules/ngx_http_cookie_flag_filter_module.so;
load_module modules/ngx_http_headers_more_filter_module.so;
```

## Handler

```yaml
- name: Reload nginx
  ansible.builtin.systemd:
    name: nginx
    state: reloaded
```
