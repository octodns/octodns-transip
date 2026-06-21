# Developer Agent Guide for octoDNS TransIP Provider

This repository contains the TransIP provider for octoDNS. It enables planning, syncing, and applying DNS record states to the TransIP API using the official `transip` Python SDK library.

> [!IMPORTANT]
> **Core Workflow and Guidelines**
>
> All agents working on this repository must read and follow the general instructions and workflow guidelines defined in the core octoDNS `AGENTS.md` file.
> - **Local check**: Look for the file at `../octodns/AGENTS.md`.
> - **Remote check**: If the local file is not available, fetch it from GitHub: [octoDNS Core AGENTS.md](https://github.com/octodns/octodns/raw/refs/heads/main/AGENTS.md).
>
> You must align your code structure, style, pull request guidelines, and overall development workflows with the instructions specified there.

## Repository & Module Information

### Key Components

- **Provider Class**: [TransipProvider](file:///home/ross/octodns/octodns-transip/octodns_transip/__init__.py#L52-L486) (defined in [octodns_transip/__init__.py](file:///home/ross/octodns/octodns-transip/octodns_transip/__init__.py)). This is the core provider wrapping domain DNS entry and nameserver mapping logic.
- **Client & SDK**: Uses `transip.TransIP` to make requests to the TransIP v6 API, utilizing `DnsEntry` and `Nameserver` objects from `transip.v6.objects`.
- **Authentication**: Authenticates using the account login (`account`) and an RSA private key. The private key can be passed directly as a string (`key`), or read from a local file (`key_file`). Supports configuring read-only global keys (`global_key=True`).

### Key Workflows & Features

1. **Supported Record Types**: `A`, `AAAA`, `CNAME`, `MX`, `NS`, `SRV`, `TXT`, `SSHFP`, `CAA`, `TLSA`, `NAPTR`, `ALIAS`, `DS`.
2. **Root NS Record TTL Constraint**: TransIP root nameservers do not support configurable TTLs. To avoid planning loop changes (constant TTL updates), the provider forces a static TTL of `3600` (`ROOT_NS_TTL`) on root NS records.
3. **Minimum TTL**: Enforces a minimum TTL limit of `120` seconds (`MIN_TTL = 120`).
4. **Apex Normalization**: Maps apex/root record names using the `@` symbol (`ROOT_RECORD = '@'`) to match TransIP requirements.
5. **Root Name Server Support**: Fully supported (`SUPPORTS_ROOT_NS=True`).
6. **Dynamic Routing**: Not supported (`SUPPORTS_DYNAMIC=False`, `SUPPORTS_GEO=False`).
7. **Dynamic Subnets**: Not supported (`SUPPORTS_DYNAMIC_SUBNETS=False`).
8. **Pool Value Status**: Not supported (`SUPPORTS_POOL_VALUE_STATUS=False`).

## Development & Testing

- **Setup Script**: Run `./script/bootstrap` to create a virtual environment, install dependencies (including `black`, `isort`, `pyflakes`, `transip`, and `pytest`), and configure pre-commit hooks.
- **Test Suite**: Run unit tests using `pytest` via `./script/test` (or `pytest tests/`). Test files are located in [tests/](file:///home/ross/octodns/octodns-transip/tests).
- **Code Coverage**: Verify code coverage using `./script/coverage`.

## Key Constraints & Behaviors

- **Python Version**: Targets Python `>=3.9`.
- **Formatting**: Code formatting is enforced via `black` (version `>=26.0.0,<27.0.0`) and `isort`.
