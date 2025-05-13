# Personal Development Configuration

A collection of my personal development environment configurations, including SSH setups, Go private repository access, Ruby configurations, and GitHub identity management settings.

## Table of Contents

* [Prerequisites](#prerequisites)
* [Setup Instructions](#setup-instructions)
    + [SSH Configuration](#ssh-configuration)
    + [Go Private Repository Access](#go-private-repository-access)
    + [Ruby Setup](#ruby-setup)
    + [GitHub Identity Management](#github-identity-management)
* [Troubleshooting](#troubleshooting)

## Prerequisites

Before starting the setup process:

### Required Tools

| Tool | Version |
|------|---------|
| Git | ≥ 2.35.0 |
| Go | ≥ 1.20.0 |
| Ruby | ≥ 3.2.0 |

### System Requirements

* Unix-like operating system (Linux/MacOS)
* Terminal emulator
* Text editor

## Setup Instructions

### SSH Configuration

1. Generate SSH key pair:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

2. Configure SSH identities:
```bash
# ~/.ssh/config
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
```

3. Add SSH keys to ssh-agent:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```

### Go Private Repository Access

1. Create authentication configuration:
```json
// $HOME/go/.auth.json
{
    "auth": {
        "example.com": {
            "auth": "base64 encoded username:password"
        }
    }
}
```

2. Set GOPRIVATE environment variable:
```bash
export GOPRIVATE=example.com/private/*
```

### Ruby Setup

1. Install required gems:
```bash
gem install bundler
gem install pry-byebug
```

2. Configure gem sources:
```yaml
# ~/.gemrc
---
install: --no-document
update: --no-document
sources:
  - https://rubygems.org
```

### GitHub Identity Management

1. Configure global Git settings:
```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

2. Verify SSH connections:
```bash
ssh -T github-personal
ssh -T github-work
```

## Troubleshooting

### Common Issues

#### SSH Connection Problems
If SSH connections fail:
```bash
# Check SSH agent status
ssh-add -l

# Test connection with verbose output
ssh -vT github-personal
```

#### Go Authentication Errors
If Go modules fail to authenticate:
```bash
# Clear Go module cache
rm -rf $GOPATH/pkg/mod/cache/*

# Re-authenticate
go clean -modcache
```

## Contributing

This repository contains personal configuration files. While you're welcome to use it as a reference, please fork the repository for your own use rather than submitting pull requests.
