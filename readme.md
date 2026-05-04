# Ubuntu Network Troubleshooting Lab

## Overview

This repository documents a hands-on Ubuntu network troubleshooting lab focused on diagnosing connectivity issues from the Linux command line.

The lab covers IP configuration, routing, DNS resolution, SSH access, firewall rules, listening ports, service availability, and packet capture basics.

## Scenario

A user reports that they cannot connect to an Ubuntu server. The issue could involve SSH, DNS, firewall rules, incorrect IP configuration, a stopped service, or a blocked port.

## Objectives

- Verify IP configuration
- Check routing
- Test basic network connectivity
- Troubleshoot DNS resolution
- Confirm listening ports
- Check service status
- Review firewall rules
- Use packet capture for deeper troubleshooting
- Document the root cause and resolution

## Environment

- OS: Ubuntu Server
- Platform: Local VM / Cloud VM
- Tools: `ip`, `ping`, `traceroute`, `dig`, `resolvectl`, `ss`, `curl`, `nc`, `ufw`, `tcpdump`, `systemctl`, `journalctl`

## Skills Demonstrated

- Linux network troubleshooting
- SSH diagnostics
- DNS troubleshooting
- Firewall validation
- Port and service checks
- Packet capture basics
- Root cause analysis
- Technical documentation

## Investigation Workflow

### 1. Check IP configuration

```bash
ip addr
ip route
