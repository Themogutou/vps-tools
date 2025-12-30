# 🌐 VPS DNS 优化工具 (bwhDNS)

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0-blue.svg" alt="Version">
  <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License">
  <img src="https://img.shields.io/badge/platform-Linux-orange.svg" alt="Platform">
  <img src="https://img.shields.io/badge/shell-bash-brightgreen.svg" alt="Shell">
</p>

<p align="center">
  <b>专为 VPS 设计的 DNS 优化与防篡改脚本，解决 DNS 重置问题</b>
</p>

---

## ✨ 功能特性

| 功能 | 说明 |
|------|------|
| 🚀 **快速 DNS** | 自动配置 Google (8.8.8.8) 和 Cloudflare (1.1.1.1) DNS |
| 🔒 **防篡改锁定** | 使用 `chattr +i` 锁定配置文件，防止被系统覆盖 |
| 🛡️ **服务禁用** | 自动禁用干扰 DNS 的 `systemd-resolved` 服务 |
| 🔄 **重启持久化** | 写入 `/etc/rc.local`，确保重启后 DNS 配置依然有效 |
| 🔧 **自动兼容** | 自动处理符号链接，支持 apt/yum/dnf/pacman 包管理器 |

---

## 🛠️ 解决的问题

很多 VPS（特别是搬瓦工 BandwagonHost）在重启或 DHCP 更新时，会自动重置 `/etc/resolv.conf`，导致：
- ❌ DNS 变回运营商默认的慢速 DNS
- ❌ 之前修改的 DNS 设置失效
- ❌ 访问部分网站变慢或解析失败

**本脚本通过多重锁定机制，彻底解决此问题！**

---

## 📦 一键使用

```bash
# 使用 curl
bash <(curl -sL https://raw.githubusercontent.com/Themogutou/vps-tools/main/bwhDNS.sh)
```

或

```bash
# 使用 wget
wget -qO- https://raw.githubusercontent.com/Themogutou/vps-tools/main/bwhDNS.sh | bash
```

---

## 💻 脚本执行逻辑

1. **依赖检查**：自动安装 `curl` 和 `sudo`
2. **符号链接处理**：如果 `/etc/resolv.conf` 是软链接，删除并创建实文件
3. **写入 DNS**：
   - nameserver 8.8.8.8
   - nameserver 1.1.1.1
4. **文件锁定**：执行 `chattr +i /etc/resolv.conf` 变为不可修改
5. **服务调整**：禁用 `systemd-resolved`
6. **持久化**：添加启动脚本到 `/etc/rc.local`

---

## 📊 适用系统

- ✅ Debian / Ubuntu
- ✅ CentOS / AlmaLinux / Rocky Linux
- ✅ Arch Linux
- ✅ 其他主流 Linux 发行版

---

## ⚠️ 注意事项

- 本脚本需要 **root** 权限运行
- 执行后 `/etc/resolv.conf` 将被锁定，如需手动修改请先解锁：
  ```bash
  chattr -i /etc/resolv.conf
  ```

---

## 📜 开源协议

本项目采用 [MIT License](LICENSE) 开源协议。

---

<p align="center">
  <b>⭐ 如果觉得好用，请给个 Star！⭐</b>
</p>
