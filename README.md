# 🛡️ Secure Remote Access: Personal WireGuard VPN mit DDNS

**Linux** | **Networking** | **Security** | **DNS**

> Selbst gehosteter, verschlüsselter VPN-Tunnel auf Ubuntu Server 24.04 LTS — mit automatischer DNS-Aktualisierung bei dynamischer IP und vollständiger Netzwerkkonfiguration über die Kommandozeile.

---

## 📌 Was das Projekt macht
Dieses Projekt realisiert einen vollständig selbst kontrollierten, verschlüsselten VPN-Tunnel vom Client-Gerät (Smartphone, Laptop) bis zum Heimserver. Statt eines kommerziellen Dienstes wie NordVPN läuft der Server auf einer eigenen Ubuntu-VM. Der gesamte Internetverkehr wird durch den Tunnel geleitet — öffentliche Netze sehen nur verschlüsselte Pakete. Websites sehen die Heimadresse, nicht den tatsächlichen Standort.

---

## 🏗 Architektur & Datenfluss

📱 **Client** (Android/Windows) ➔ 🔒 **WireGuard** (UDP verschlüsselt) ➔ 🌐 **DuckDNS** (Domain) ➔ 🔁 **Router** (Port 51820 UDP) ➔ 🖥️ **Ubuntu VM** (Server)

---

## 🛠 Technologiestack

* 🐧 **Ubuntu Server 24.04 LTS:** Betriebssystem ohne GUI. Gesamte Konfiguration erfolgt ausschließlich über SSH und die Kommandozeile.
* ⚡ **WireGuard:** Modernes VPN-Protokoll direkt im Linux-Kernel. Asymmetrische Kryptographie. Schneller als OpenVPN.
* 🌍 **DuckDNS (Dynamic DNS):** Kostenloser DDNS-Dienst. Ein Cron-Job aktualisiert automatisch die IP-Adresse.
* 🚪 **Port Forwarding:** Eingehender UDP-Traffic auf Port 51820 wird direkt an die Ubuntu-VM weitergeleitet.

---

## 🎯 Ziele des Projekts

1. **Sicherheit:** Schutz vor Man-in-the-Middle-Angriffen in öffentlichen WLAN-Netzen.
2. **Remote-Zugang:** Sicherer Zugriff auf Heimgeräte von überall auf der Welt aus.
3. **Praxis:** Hands-on-Erfahrung mit Linux-Netzwerkkonfiguration, Routing und Firewall-Regeln.

---

## 🔧 Gelöste Probleme während der Umsetzung

| Status | Problem & Lösung |
| :---: | :--- |
| ❌ ➔ ✅ | **IP-Weiterleitung nicht aktiv:** Kein Traffic durch den Tunnel möglich. **Lösung:** `net.ipv4.ip_forward=1` in `/etc/sysctl.conf` gesetzt. |
| ❌ ➔ ✅ | **Dynamische IP des Anbieters:** Verbindung brach bei IP-Wechsel ab. **Lösung:** Bash-Skript + Cron-Job (alle 5 Min) für DuckDNS eingerichtet. |
| 🏆 | **Ergebnis:** Stabile verschlüsselte Verbindung (~8–15 ms Latenz), kein DNS-Leak nachweisbar. |

---

## 🧠 Demonstrierte Kenntnisse
`Linux CLI` `SSH` `Netzwerk-Routing` `UDP/TCP` `Firewall (UFW)` `DNS / DDNS` `Public/Private Key` `Cron-Jobs` `NAT / Port Forwarding` `Systemd` `VirtualBox` `Troubleshooting`

---

## 📊 Messbares Ergebnis
* **Verbindungslatenz:** ~12 ms
* **DNS-Update-Intervall:** 5 min
* **DNS-Leaks:** 0
