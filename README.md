# 🛡️ VPN-server med OpenVPN på Ubuntu/Debian Guide

Detta är en steg-för-steg guide för att installera och konfigurera en OpenVPN-server på ett Ubuntu- eller Debian-baserat system.

---

## Steg 1: Serverförberedelse och Uppdatering

Se till att ditt system är uppdaterat innan installationen påbörjas.

1.  **Logga in** på din server med SSH.
2.  **Uppdatera systemet:**
    ```bash
    apt update && apt upgrade -y
    ```
3.  **Installera OpenVPN:**
    ```bash
    apt install openvpn -y
    ```

## Steg 2: Ladda ner och kör OpenVPN-installationsskriptet

Vi använder ett rekommenderat officiellt installationsskript för en enkel och säker konfiguration.

1.  **Ladda ner skriptet:**
    ```bash
    wget [https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh](https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh)
    ```
2.  **Gör skriptet körbart:**
    ```bash
    chmod +x openvpn-install.sh
    ```
3.  **Kör installationsskriptet:**
    ```bash
    ./openvpn-install.sh
    ```

## Steg 3: Svara på Skriptfrågorna (Konfiguration)

Skriptet kommer att ställa flera frågor för att konfigurera din VPN-server. Här är en rekommenderad konfiguration:

| Fråga | Rekommenderat Svar | Kommentar |
| :--- | :--- | :--- |
| IP-adress/publikt DNS-namn | *Detta ska skriptet försöka fylla i automatiskt.* | Kontrollera att det är rätt extern IP-adress. |
| Protokoll (UDP/TCP) | Välj **UDP** (Rekommenderas för hastighet). | Tryck oftast bara Enter. |
| Port | Välj **1194** (Standardport) eller en valfri port. | Ange porten du vill använda. |
| DNS-server | Välj **1** (Current system resolvers) eller **3** (Google). | Rekommenderas: Välj **3** för Google DNS. |
| Klientnamn | Välj ett namn för din första klient, t.ex. `laptop`. | Detta blir namnet på din `.ovpn` fil. |

## Steg 4: Hämta Klientkonfigurationsfilen

När installationen är klar kommer skriptet att berätta var din `.ovpn` fil (klientkonfiguration) sparats.

1.  **Hitta din `.ovpn` fil:** Filen sparas i din hemkatalog, t.ex. `/root/laptop.ovpn`.
2.  **Överför filen** till din lokala dator (den du vill ansluta med). Använd ett program som **SCP** eller **SFTP** (t.ex. med **WinSCP** eller **FileZilla**) för att kopiera filen.

*Exempel med SCP:*
```bash
scp root@<din-server-ip>:/root/laptop.ovpn /lokal/katalog/
