# SQM Scripts (Pure nftables fork)

This repository contains a modernized fork of the SQM (Smart Queue Management) scripts. It is specifically designed for OpenWrt's firewall4, utilizing a pure nftables implementation and completely dropping all legacy iptables dependencies.

## Key Features

*   **Pure nftables:** Fully compatible with OpenWrt's firewall4.
*   **POSIX Compliance:** Shell scripts are strictly POSIX compliant for compatibility with OpenWrt's BusyBox ash.
*   **CAKE by Default:** Uses the CAKE integrated scheduler by default for both shaping and scheduling.

## Hardware & Performance

These scripts are optimized for high-speed links and modern hardware. They perform exceptionally well on high-speed SoCs like the NanoPi R6S/R6C (RK3588), easily pushing 750Mbps+ throughput with SQM enabled.

## Installation

Installation is managed via OpenWrt's opkg package manager.

**Note:** The package `kmod-ifb` is a mandatory dependency for ingress shaping (Download) to work correctly.

To install the package, use the following commands on your OpenWrt device:

```sh
opkg update
opkg install sqm-scripts-nft
```

## Configuration

Configuration is handled via UCI and stored in `/etc/config/sqm`. Below is a brief example of a typical UCI configuration block:

```uci
config queue 'eth1'
    option enabled '1'
    option interface 'eth1'
    option download '1000000'
    option upload '50000'
    option qdisc 'cake'
    option script 'piece_of_cake.qos'
    option linklayer 'none'
```

### Advanced CAKE Configuration

For advanced users, you can pass arbitrary configuration parameters directly to the CAKE qdisc using `ingress_extra` and `egress_extra`. This allows setting options like `memlimit`, `ack-filter`, `rtt`, etc., that are not explicitly managed by the primary SQM options.

```uci
# Example: Increasing memory limit for high-connection environments (e.g., torrenting) and enabling ACK filtering
config queue 'eth1'
    option enabled '1'
    option interface 'eth1'
    option download '1000000'
    option upload '50000'
    option qdisc 'cake'
    option script 'piece_of_cake.qos'
    option linklayer 'none'
    option ingress_extra 'memlimit 64M ack-filter'
    option egress_extra 'memlimit 64M ack-filter'
```

---
*Footnote: The codebase in this repository has been refactored, modernized, and ported to pure nftables with AI assistance. This modernization effort prioritizes transparency, code clarity, performance, and forward compatibility with contemporary Linux networking stacks.*
