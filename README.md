<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: var(--font-sans); color: var(--color-text-primary); }
  .wrap { padding: 1.5rem 0; max-width: 780px; }
  .badge-row { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 1.5rem; }
  .badge { font-size: 12px; font-weight: 500; padding: 4px 12px; border-radius: 999px; }
  .badge-teal { background: #E1F5EE; color: #0F6E56; }
  .badge-blue { background: #E6F1FB; color: #185FA5; }
  .badge-purple { background: #EEEDFE; color: #534AB7; }
  .badge-amber { background: #FAEEDA; color: #854F0B; }
  .section { margin-bottom: 2rem; }
  .section-title { font-size: 13px; font-weight: 500; color: var(--color-text-secondary); text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 0.75rem; }
  .project-title { font-size: 22px; font-weight: 500; margin-bottom: 0.5rem; line-height: 1.3; }
  .subtitle { font-size: 15px; color: var(--color-text-secondary); margin-bottom: 1.5rem; line-height: 1.6; }
  .card { background: var(--color-background-primary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); padding: 1rem 1.25rem; margin-bottom: 0.75rem; }
  .card-title { font-size: 14px; font-weight: 500; margin-bottom: 0.4rem; }
  .card-body { font-size: 13px; color: var(--color-text-secondary); line-height: 1.6; }
  .grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem; }
  .grid3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0.75rem; }
  .metric { background: var(--color-background-secondary); border-radius: var(--border-radius-md); padding: 1rem; }
  .metric-label { font-size: 12px; color: var(--color-text-secondary); margin-bottom: 4px; }
  .metric-value { font-size: 20px; font-weight: 500; }
  .arch-row { display: flex; align-items: center; gap: 0; margin-bottom: 0.75rem; flex-wrap: wrap; gap: 6px; }
  .arch-node { background: var(--color-background-secondary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-md); padding: 8px 14px; font-size: 13px; font-weight: 500; text-align: center; }
  .arch-arrow { font-size: 16px; color: var(--color-text-secondary); }
  .arch-label { font-size: 11px; color: var(--color-text-secondary); margin-top: 2px; font-weight: 400; }
  .problem-row { display: flex; gap: 12px; margin-bottom: 0.75rem; align-items: flex-start; }
  .problem-icon { width: 28px; height: 28px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 13px; flex-shrink: 0; margin-top: 1px; }
  .icon-red { background: #FCEBEB; color: #A32D2D; }
  .icon-teal { background: #E1F5EE; color: #0F6E56; }
  .divider { border: none; border-top: 0.5px solid var(--color-border-tertiary); margin: 1.5rem 0; }
  .skill-tag { display: inline-block; font-size: 12px; padding: 3px 10px; border-radius: 4px; border: 0.5px solid var(--color-border-tertiary); color: var(--color-text-secondary); margin: 3px; }
  @media (max-width: 500px) { .grid2, .grid3 { grid-template-columns: 1fr; } }
</style>

<div class="wrap">

  <div class="section">
    <div class="badge-row">
      <span class="badge badge-teal">Linux</span>
      <span class="badge badge-blue">Networking</span>
      <span class="badge badge-purple">Security</span>
      <span class="badge badge-amber">DNS</span>
    </div>
    <div class="project-title">Secure Remote Access: Personal WireGuard VPN mit DDNS</div>
    <div class="subtitle">Selbst gehosteter, verschlüsselter VPN-Tunnel auf Ubuntu Server 24.04 LTS — mit automatischer DNS-Aktualisierung bei dynamischer IP und vollständiger Netzwerkkonfiguration über die Kommandozeile.</div>
  </div>

  <hr class="divider">

  <div class="section">
    <div class="section-title">Was der Projekt macht</div>
    <div class="card">
      <div class="card-body">Dieser Projekt realisiert einen vollständig selbst kontrollierten, verschlüsselten VPN-Tunnel vom Client-Gerät (Smartphone, Laptop) bis zum Heimserver. Statt eines kommerziellen Dienstes wie NordVPN läuft der Server auf einer eigenen Ubuntu-VM. Der gesamte Internetverkehr wird durch den Tunnel geleitet — öffentliche Netze sehen nur verschlüsselte Pakete. Websites sehen die Heimadresse, nicht den tatsächlichen Standort.</div>
    </div>
  </div>

  <div class="section">
    <div class="section-title">Architektur &amp; Datenfluss</div>
    <div class="arch-row">
      <div>
        <div class="arch-node">📱 Client<br><span class="arch-label">Android / Windows</span></div>
      </div>
      <div class="arch-arrow">→</div>
      <div>
        <div class="arch-node">🔒 WireGuard<br><span class="arch-label">UDP verschlüsselt</span></div>
      </div>
      <div class="arch-arrow">→</div>
      <div>
        <div class="arch-node">🌐 DuckDNS<br><span class="arch-label">vlad-vpn.duckdns.org</span></div>
      </div>
      <div class="arch-arrow">→</div>
      <div>
        <div class="arch-node">🔁 Router<br><span class="arch-label">Port 51820 UDP</span></div>
      </div>
      <div class="arch-arrow">→</div>
      <div>
        <div class="arch-node">🖥️ Ubuntu VM<br><span class="arch-label">WireGuard Server</span></div>
      </div>
    </div>
  </div>

  <hr class="divider">

  <div class="section">
    <div class="section-title">Technologiestack</div>
    <div class="grid2">
      <div class="card">
        <div class="card-title">Ubuntu Server 24.04 LTS</div>
        <div class="card-body">Betriebssystem ohne GUI. Gesamte Konfiguration erfolgt ausschließlich über SSH und die Kommandozeile. Verwaltet Netzwerkschnittstellen, Routing und Firewall.</div>
      </div>
      <div class="card">
        <div class="card-title">WireGuard</div>
        <div class="card-body">Modernes VPN-Protokoll direkt im Linux-Kernel. Asymmetrische Kryptographie mit Public/Private-Key-Paaren. Wesentlich schneller und schlanker als OpenVPN oder IPsec.</div>
      </div>
      <div class="card">
        <div class="card-title">DuckDNS (Dynamic DNS)</div>
        <div class="card-body">Kostenloser DDNS-Dienst. Ein Cron-Job auf dem Server aktualisiert automatisch die IP-Adresse hinter dem Domainnamen, wenn der Heimanbieter eine neue IP vergibt.</div>
      </div>
      <div class="card">
        <div class="card-title">Port Forwarding</div>
        <div class="card-body">Konfiguration am Heimrouter: eingehender UDP-Traffic auf Port 51820 wird direkt an die interne IP-Adresse der Ubuntu-VM weitergeleitet.</div>
      </div>
    </div>
  </div>

  <div class="section">
    <div class="section-title">Ziele des Projekts</div>
    <div class="grid3">
      <div class="card">
        <div class="card-title">Sicherheit</div>
        <div class="card-body">Schutz vor Man-in-the-Middle-Angriffen in öffentlichen WLAN-Netzen (Airports, Cafés). Vollständige Verkehrsverschlüsselung.</div>
      </div>
      <div class="card">
        <div class="card-title">Remote-Zugang</div>
        <div class="card-body">Sicherer Zugriff auf Heimgeräte (Router-Admin, andere Rechner) von überall auf der Welt aus.</div>
      </div>
      <div class="card">
        <div class="card-title">Praxis</div>
        <div class="card-body">Hands-on-Erfahrung mit Linux-Netzwerkkonfiguration, Routing, Kryptographie und Firewall-Regeln.</div>
      </div>
    </div>
  </div>

  <hr class="divider">

  <div class="section">
    <div class="section-title">Gelöste Probleme während der Umsetzung</div>
    <div class="problem-row">
      <div class="problem-icon icon-red">✕</div>
      <div class="card" style="flex:1; margin-bottom:0">
        <div class="card-title">Problem: IP-Weiterleitung nicht aktiv</div>
        <div class="card-body">Nach der WireGuard-Installation war kein Traffic durch den Tunnel möglich. Ursache: IP-Forwarding unter Linux standardmäßig deaktiviert. Lösung: <code>net.ipv4.ip_forward=1</code> in <code>/etc/sysctl.conf</code> gesetzt und dauerhaft aktiviert.</div>
      </div>
    </div>
    <div class="problem-row">
      <div class="problem-icon icon-red">✕</div>
      <div class="card" style="flex:1; margin-bottom:0">
        <div class="card-title">Problem: Verbindung nach IP-Wechsel des Anbieters unterbrochen</div>
        <div class="card-body">Der Heimanbieter vergibt dynamisch neue IP-Adressen. Lösung: Cron-Job eingerichtet, der alle 5 Minuten die aktuelle IP an DuckDNS meldet. Domain bleibt dauerhaft erreichbar.</div>
      </div>
    </div>
    <div class="problem-row">
      <div class="problem-icon icon-teal">✓</div>
      <div class="card" style="flex:1; margin-bottom:0">
        <div class="card-title">Ergebnis: Stabile verschlüsselte Verbindung</div>
        <div class="card-body">VPN-Tunnel funktioniert stabil von Android und Windows-Clients. Latenz im Heimnetz: ~8–15 ms. Vollständige DNS-Auflösung über den Tunnel — kein DNS-Leak nachweisbar.</div>
      </div>
    </div>
  </div>

  <hr class="divider">

  <div class="section">
    <div class="section-title">Demonstrierte Kenntnisse</div>
    <div>
      <span class="skill-tag">Linux CLI</span>
      <span class="skill-tag">SSH</span>
      <span class="skill-tag">Netzwerk-Routing</span>
      <span class="skill-tag">UDP/TCP</span>
      <span class="skill-tag">Firewall / UFW</span>
      <span class="skill-tag">DNS / DDNS</span>
      <span class="skill-tag">Public/Private Key</span>
      <span class="skill-tag">Cron-Jobs</span>
      <span class="skill-tag">NAT / Port Forwarding</span>
      <span class="skill-tag">Systemd</span>
      <span class="skill-tag">VirtualBox / VM</span>
      <span class="skill-tag">Troubleshooting</span>
    </div>
  </div>

  <div class="section">
    <div class="section-title">Messbares Ergebnis</div>
    <div class="grid3">
      <div class="metric">
        <div class="metric-label">Verbindungslatenz</div>
        <div class="metric-value">~12 ms</div>
      </div>
      <div class="metric">
        <div class="metric-label">DNS-Update-Intervall</div>
        <div class="metric-value">5 min</div>
      </div>
      <div class="metric">
        <div class="metric-label">DNS-Leaks</div>
        <div class="metric-value">0</div>
      </div>
    </div>
  </div>

</div>
