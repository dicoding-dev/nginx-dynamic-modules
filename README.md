# Nginx Dynamic Modules

Pre-built Nginx dynamic modules compiled from source for multiple OS and architecture combinations.

## Modules

| Module | Source |
|--------|--------|
| `ngx_http_cookie_flag_filter_module.so` | [nginx_cookie_flag_module](https://github.com/AirisX/nginx_cookie_flag_module) |
| `ngx_http_headers_more_filter_module.so` | [headers-more-nginx-module](https://github.com/openresty/headers-more-nginx-module) |

## Build Matrix

- **OS**: Ubuntu Jammy (22.04), Ubuntu Noble (24.04)
- **Arch**: amd64, arm64

## Usage

Download the matching tarball from [Releases](../../releases) and load the modules in your `nginx.conf`:

```nginx
load_module modules/ngx_http_cookie_flag_filter_module.so;
load_module modules/ngx_http_headers_more_filter_module.so;
```

## Triggering a Build

**Tag push** — creates a release automatically:

```bash
git tag v1.28.0-1
git push origin v1.28.0-1
```

**Manual dispatch** — builds artifacts only (no release):

Go to Actions → Build Nginx Dynamic Modules → Run workflow, and enter the nginx version.

## Release Artifacts

Each release contains tarballs per OS/arch combination:

- `nginx-modules-jammy-amd64.tar.gz`
- `nginx-modules-jammy-arm64.tar.gz`
- `nginx-modules-noble-amd64.tar.gz`
- `nginx-modules-noble-arm64.tar.gz`
