# Changelog

## V3.0 (Kareem Ali Fork - @Kareemcanaan)

### Major Features
* **IPv6 Dual-Stack Support**: Full support for IPv6 alongside IPv4
  * Added IPv6 gateway configuration for primary and standby networks
  * Dual-stack route management in failover monitor
  * Configurable via `ipv6-enabled`, `primary-gw6`, `standby-gw6` settings
  
* **pyroute2 Integration**: Replaced shell command dependencies
  * Implemented `RouteManager` class using pyroute2 library
  * Direct kernel netlink communication for route manipulation
  * Significant performance improvements over subprocess calls
  * Automatic fallback to shell commands if pyroute2 unavailable
  * Better error handling and type safety

### Technical Improvements
* Cleaner, more maintainable code architecture
* Cross-platform compatibility improvements
* Foundation for future networking features
* Updated installation script to include pyroute2 dependency

### Documentation
* Updated README with new features and configuration examples
* Added IPv6 configuration guide
* Documented pyroute2 benefits and fallback behavior

---

## V2.97 (Original - gitbls)

* python3-icmplib in Bookworm is too old (V2 vs required V3 which supports host.jitter)
  * Always use pip3 icmplib, which is now installed into a venv: /root/.imon-venv
  * Affects: imon-install, imon@.service
* Correct typo in imon

## V2.96

* Use python3-icmplib on Bookworm
* Eliminate python deprecation messages

## V2.95

* Code cleanup
* When interface newly detected as offline, delete its default route

## V2.90

* Initial version
