# Set up WireGuard

[![Test "Set up WireGuard" Action](https://img.shields.io/github/actions/workflow/status/inpsyde/actions/test-setup-wireguard.yml)](https://github.com/inpsyde/actions/actions/workflows/test-setup-wireguard.yml)

This GitHub Action configures and initiates a secure WireGuard VPN connection in the calling
workflow.

```yml
- uses: inpsyde/actions/setup-wireguard@v1
  with:
    # The full content of the WireGuard configuration file (`.conf`).
    wireguard-configuration: ''
```

## Features

- Validates the provided WireGuard configuration to prevent the execution of arbitrary commands
- Installs WireGuard on the runner
- Configures WireGuard using the provided configuration
- Sets up a secure connection with `wg-quick`

## Example

```yml
- name: Set up WireGuard
  uses: inpsyde/actions/setup-wireguard@v1
  with:
    wireguard-configuration: ${{ secrets.WIREGUARD_CONFIGURATION }}
```

## Security Considerations

The WireGuard configuration must be stored as a secret in the calling GitHub repository. **Do not
hardcode sensitive information directly in workflow files.**

### Validation of Configuration

To enhance security, this action includes validation logic that disallows certain directives in the
WireGuard configuration that could execute arbitrary shell commands. Specifically, the following
directives are disallowed:

- PreUp
- PostUp
- PreDown
- PostDown

These directives can execute shell commands when the WireGuard interface is brought up or down,
posing a security risk if misused. If the configuration includes any of these directives, the action
will fail with an error message:

```text
Error: Configuration contains disallowed directives (PreUp, PostUp, PreDown, PostDown).
```

Ensure the WireGuard configuration does not include these directives. Only include the necessary
configuration options within the [Interface] and [Peer] sections.

### Example of a Valid Configuration

```ini
[Interface]
Address = 10.0.0.1/24
PrivateKey = Q29uZ3JhdHVsYXRpb25zLCB5b3UgZm91bmQgYW4gZWFzdGVyIGVnZyE=
ListenPort = 51820

[Peer]
PresharedKey = V2UgYXJlIGhpcmluZyEgQ2hlY2sgaGVyZSBzeWRlLmNvbS9jYXJlZXI=
PublicKey = U3lkZSDigJMgRXVyb3Bl4oCZcyBiaWdnZXN0IFdQIGFnZW5jeSE=
AllowedIPs = 0.0.0.0/0
Endpoint = peer.example.com:51820
PersistentKeepalive = 25
```
