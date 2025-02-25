# Syde Actions

[![GitHub Release](https://img.shields.io/github/v/release/inpsyde/actions)](https://github.com/inpsyde/actions/releases)
[![Status](https://img.shields.io/badge/status-active-brightgreen.svg)](https://github.com/inpsyde/actions)
[![License](https://img.shields.io/github/license/inpsyde/actions)](./LICENSE)

A collection of multi-purpose GitHub Actions.

> [!IMPORTANT]  
> **Supported Runners:** **Ubuntu (Linux) runners only.** The actions are incompatible with macOS or
> Windows runners.

## Available Actions

### [Set up WireGuard](./setup-wireguard/README.md)

**Description:** Configures and initiates a secure WireGuard VPN connection.

**Usage:**

```yml
- uses: inpsyde/actions/setup-wireguard@v1
  with:
    wireguard-configuration: ${{ secrets.WIREGUARD_CONFIGURATION }}
```

## Copyright and License

This package is [free software](https://www.gnu.org/philosophy/free-sw.en.html) distributed under the terms of the GNU General Public License version 2 or (at your option) any later version. For the full license, see [LICENSE](./LICENSE).
