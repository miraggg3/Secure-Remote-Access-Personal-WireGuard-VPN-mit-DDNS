# Secure Remote Access: Personal WireGuard VPN mit DDNS

![Linux](https://img.shields.io/badge/Linux-Ubuntu_24.04-orange)
![WireGuard](https://img.shields.io/badge/VPN-WireGuard-88171A)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

Selbst gehosteter, verschlüsselter VPN-Tunnel auf Ubuntu Server 24.04 LTS — mit automatischer DNS-Aktualisierung bei dynamischer IP und vollständiger Netzwerkkonfiguration über die Kommandozeile.

---

## Was der Projekt macht

Dieser Projekt realisiert einen vollständig selbst kontrollierten, verschlüsselten VPN-Tunnel vom Client-Gerät (Smartphone, Laptop) bis zum Heimserver. Statt eines kommerziellen Dienstes wie NordVPN läuft der Server auf einer eigenen Ubuntu-VM.

Der gesamte Internetverkehr wird durch den Tunnel geleitet — öffentliche Netze sehen nur verschlüsselte Pakete. Websites sehen die Heimadresse, nicht den tatsächlichen Standort.

---

## Architektur & Datenfluss

```
[Client: Android / Windows]
        |
        | WireGuard UDP (verschlüsselt)
        v
[DuckDNS: example-vpn.duckdns.org]
        |
        | DNS → dynamische Heim-IP
        v
[Heimrouter: Port Forwarding 51820 UDP]
        |
        v
[Ubuntu VM: WireGuard Server]
        |
        v
[Internet]
```

---

## Technologiestack

| Komponente | Beschreibung |
|---|---|
| **Ubuntu Server 24.04 LTS** | Betriebssystem ohne GUI. Gesamte Konfiguration ausschließlich über SSH und Kommandozeile. |
| **WireGuard** | Modernes VPN-Protokoll direkt im Linux-Kernel. Asymmetrische Kryptographie mit Public/Private-Key-Paaren. Schneller und schlanker als OpenVPN oder IPsec. |
| **DuckDNS (DDNS)** | Kostenloser Dynamic-DNS-Dienst. Cron-Job aktualisiert automatisch die IP-Adresse hinter dem Domainnamen, wenn der Heimanbieter eine neue IP vergibt. |
| **Port Forwarding** | Konfiguration am Heimrouter: eingehender UDP-Traffic auf Port 51820 wird direkt an die interne IP der Ubuntu-VM weitergeleitet. |
| **UFW (Uncomplicated Firewall)** | Firewall-Regeln auf dem Ubuntu-Server: nur Port 51820 UDP offen, alle anderen eingehenden Verbindungen blockiert. |

---

## Ziele des Projekts

**Sicherheit** — Schutz vor Man-in-the-Middle-Angriffen in öffentlichen WLAN-Netzen (Airports, Cafés). Vollständige Verkehrsverschlüsselung ohne Abhängigkeit von kommerziellen VPN-Anbietern.

**Remote-Zugang** — Sicherer Zugriff auf Heimgeräte (Router-Admin, andere Rechner im LAN) von überall auf der Welt.

**Praxis** — Hands-on-Erfahrung mit Linux-Netzwerkkonfiguration, IP-Routing, Kryptographie und Firewall-Regeln in einer realen Umgebung.

---

## Gelöste Probleme während der Umsetzung

### Problem 1: IP-Weiterleitung nicht aktiv

Nach der WireGuard-Installation war kein Traffic durch den Tunnel möglich. Verbindung wurde aufgebaut, aber kein Internetzugang.

**Ursache:** IP-Forwarding unter Linux ist standardmäßig deaktiviert.

**Lösung:**
```bash
# In /etc/sysctl.conf gesetzt:
net.ipv4.ip_forward=1

# Sofort aktiviert ohne Neustart:
sudo sysctl -p
```

---

### Problem 2: Verbindungsabbruch nach IP-Wechsel des Anbieters

Der Heimanbieter vergibt dynamisch neue IP-Adressen — nach jedem Wechsel war der VPN nicht mehr erreichbar.

**Lösung:** Cron-Job eingerichtet, der alle 5 Minuten die aktuelle IP automatisch an DuckDNS meldet:

```bash
# /etc/cron.d/duckdns
*/5 * * * * root curl -s "https://www.duckdns.org/update?domains=example-vpn&token=<TOKEN>&ip=" > /dev/null
```

Domain `example-vpn.duckdns.org` bleibt dauerhaft erreichbar, unabhängig von IP-Änderungen.

---

### Ergebnis

VPN-Tunnel funktioniert stabil von Android- und Windows-Clients. Kein DNS-Leak nachweisbar (getestet mit dnsleaktest.com).

---

## Messbares Ergebnis

| Metrik | Wert |
|---|---|
| Verbindungslatenz (Heimnetz) | ~12 ms |
| DNS-Update-Intervall | 5 Minuten |
| DNS-Leaks | 0 |
| Getestete Clients | Apple iPhone, Windows 11 Pro |

---

## Demonstrierte Kenntnisse

`Linux CLI` `SSH` `Netzwerk-Routing` `UDP/TCP` `Firewall / UFW` `DNS / DDNS` `Public/Private Key` `NAT / Port Forwarding` `Hyper-V-Manager` `Troubleshooting`
