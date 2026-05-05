# Supermetrics CLI — Linux Package Repository

This repository hosts APT (Debian/Ubuntu) and YUM/DNF (RHEL/Fedora/Amazon Linux) package repositories for the [Supermetrics CLI](https://github.com/supermetrics-public/supermetrics-cli).

Packages are published automatically via GitHub Pages on each CLI release. This repo requires no manual maintenance.

## Install

### APT (Debian / Ubuntu)

```bash
  curl -fsSL https://supermetrics-public.github.io/linux-packages/pubkey.gpg \
    | sudo gpg --dearmor -o /usr/share/keyrings/supermetrics.gpg

  echo "deb [signed-by=/usr/share/keyrings/supermetrics.gpg] https://supermetrics-public.github.io/linux-packages/ stable main" \
    | sudo tee /etc/apt/sources.list.d/supermetrics.list

  sudo apt-get update && sudo apt-get install supermetrics
```

### YUM / DNF (RHEL / Fedora / Amazon Linux)

```bash
  sudo tee /etc/yum.repos.d/supermetrics.repo <<EOF
  [supermetrics]
  name=Supermetrics CLI
  baseurl=https://supermetrics-public.github.io/linux-packages/yum/
  gpgcheck=1
  gpgkey=https://supermetrics-public.github.io/linux-packages/pubkey.gpg
  enabled=1
  EOF

  sudo yum install supermetrics
```

### Alpine / manual download

  Download .deb, .rpm, or .apk packages directly from GitHub Releases.

## How it works

  The CLI release workflow sends a repository_dispatch event to this repo after each release. The update-repo workflow then:

  1. Downloads .deb and .rpm packages from the GitHub Release
  2. Builds APT repo metadata with reprepro (GPG-signed)
  3. Builds YUM repo metadata with createrepo_c (GPG-signed)
  4. Deploys to GitHub Pages

## Other installation methods

  See the main [Supermetrics CLI repo](https://github.com/supermetrics-public/supermetrics-cli) for Homebrew, go install, and building from source.
