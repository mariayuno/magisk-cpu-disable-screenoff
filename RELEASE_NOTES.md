## v3.7 — Installer & Runtime Hardening

Bug fixes and hardening across the installer, service, and WebUI. No new features — just making everything more robust and correct.

### Fixes
- **Installer** — version banner now reads directly from `module.prop` (was hardcoded v2.9)
- **Installer** — `config.sh` now actually deployed to module directory on install (was in zip but never extracted)
- **Installer** — fresh-install default config no longer contains removed variables (`TOAST`, `NOTIFY_BAR`, stale `SETTLE_DELAY=1`)
- **Installer** — cleans up logcat FIFO and background process before replacing files
- **Installer** — sysfs hotplug check reads `CORES_OFF` from config instead of hardcoding cores 2-7
- **service.sh** — log rotation now gzips old logs (`.1.gz`, `.2.gz`) instead of raw `mv`; bounded disk use
- **service.sh** — `apply_governors` / `apply_freq_caps` / `apply_freq_on` now detect actual CPU count at runtime; works on 6, 10, 12-core devices
- **service.sh** — active core count in status JSON uses sysfs read instead of `nproc` (avoids process fork)
- **service.sh** — EXIT trap restores freq caps and cleans up `orig_freq` files if service stops during screen-off
- **WebUI** — poll intervals relaxed (status: 10s→15s, log: 5s→8s, freq: 10s→15s)

### Installation
Flash `CPU-Screen-Off-v3.7.zip` via Magisk Manager or KernelSU. Existing `postboot.sh` and `cpu_screenoff.conf` are preserved on update.

See [README](https://github.com/rexackermann/magisk-cpu-disable-screenoff/blob/main/README.md) for full configuration reference and changelog.
