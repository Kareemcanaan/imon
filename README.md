# imon - Internet Monitor
Four different internet monitoring tools, all in a single, easy-to-use service.

## 🚀 Recent Improvements (v3.0 - This Fork)

**Contributions by Kareem Ali (@Kareemcanaan):**

### ✅ IPv6 Dual-Stack Support
- Full IPv6 monitoring alongside IPv4
- Dual-stack failover for modern networks
- Configurable IPv6 gateways for primary and standby networks
- Seamless handling of both protocol versions

### ✅ pyroute2 Integration
- **Replaced shell command dependencies** with native Python `pyroute2` library
- Significantly improved performance and reliability
- Cross-platform compatibility improvements
- Automatic fallback to shell commands if pyroute2 unavailable
- Cleaner, more maintainable code

### Technical Benefits
- **Faster route manipulation**: Direct kernel netlink communication vs subprocess overhead
- **Better error handling**: Native Python exceptions instead of parsing shell output  
- **Type safety**: Structured data instead of string parsing
- **Future-proof**: Foundation for additional networking features

---

## Overview

imon implements 4 independent network monitoring functions in a multi-threaded Python app.

* **Dynamic DNS (DDNS) Monitor** — Monitors your external IP address. If it changes, your action script is called.
* **Network Failover Monitor** — Provides high-availability internet connection using primary/secondary standby model with dual-stack support.
* **Ping monitor** — Retrieve ping statistics at regular intervals.
* **Up/down IP Address Monitor** — Monitors connectivity and logs outages.

imon logs to the system log by default and can call a script you provide for further event processing.

## Installation

### Prerequisites

```bash
# Install Python dependencies
sudo apt install python3-pip --yes --no-install-recommends
sudo python -m venv /root/.imon-venv
sudo /root/.imon-venv/bin/pip3 install icmplib requests pyroute2
```

### Quick Install

```bash
sudo curl -L https://raw.githubusercontent.com/Kareemcanaan/imon/main/imon-install | bash
```

### Manual Installation

```bash
sudo curl https://raw.githubusercontent.com/Kareemcanaan/imon/main/imon -o /usr/local/bin/imon
sudo curl https://raw.githubusercontent.com/Kareemcanaan/imon/main/imon-configure -o /usr/local/bin/imon-configure
sudo curl https://raw.githubusercontent.com/Kareemcanaan/imon/main/imon-action.sample -o /usr/local/bin/imon-action.sample
sudo curl https://raw.githubusercontent.com/Kareemcanaan/imon/main/imon@.service -o /etc/systemd/system/imon@.service
sudo chmod 755 /usr/local/bin/{imon,imon-configure,imon-action}
```

## IPv6 Configuration

To enable IPv6 monitoring in your failover configuration, add these fields to `/etc/default/imon-<instance>`:

```json
{
    "failover": {
        "enable": true,
        "ipv6-enabled": true,
        "primary-gw6": "fe80::1",
        "standby-gw6": "fe80::2",
        ...
    }
}
```

## Configuration

Run `sudo imon-configure` to create an instance configuration file. Test interactively:

```bash
sudo /root/.imon-venv/bin/python /usr/local/bin/imon --nosyslog --instance myinstance
```

Enable the service:

```bash
sudo systemctl enable --now imon@myinstance
```

## Features

### Failover Monitor (Enhanced)

The failover monitor now supports:
- **Dual-stack routing**: Manages both IPv4 and IPv6 default routes
- **pyroute2 backend**: Fast, reliable route manipulation
- **Intelligent failover**: Prefer primary or ensure connectivity
- **Post-failover validation**: Verify connectivity after switching

### Other Monitors

- **ddns**: Monitor external IP changes
- **updown**: Track connectivity to specific hosts
- **ping**: Regular latency and packet loss statistics

## Credits

- **Original Author**: Benn (@gitbls) - [github.com/gitbls/imon](https://github.com/gitbls/imon)
- **IPv6 & pyroute2 Contributions**: Kareem Ali (@Kareemcanaan)

## License

MIT License - See LICENSE file

---

For complete documentation, see the [original project](https://github.com/gitbls/imon).
