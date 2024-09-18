# GitHub Action: WireGuard Setup

This GitHub Action configures and initiates a secure WireGuard VPN connection in your workflow.

```yml
- uses: inpsyde/setup-wireguard@v1
  with:
    # The full content of your WireGuard configuration file (`.conf`).
    WIREGUARD_CONFIGURATION: ''
```

## Features

- Installs WireGuard on the runner
- Configures WireGuard using a provided configuration file
- Sets up a secure connection with `wg-quick`

## Example

```yml
- name: Set up WireGuard
  uses: inpsyde/setup-wireguard@v1
  with:
    WIREGUARD_CONFIGURATION: ${{ secrets.WIREGUARD_CONFIGURATION }}
```

## Security Considerations

The WireGuard configuration file must be stored as a secret in the calling GitHub repository. Do not
hardcode sensitive information directly in workflow filess.
This action applies strict file permissions to the configuration file to ensure it remains secure
during execution.

## Copyright and License

This package is [free software](https://www.gnu.org/philosophy/free-sw.en.html) distributed under
the terms of the GNU General Public License version 2 or (at your option) any later version. For the
full license, see [LICENSE](./LICENSE).
