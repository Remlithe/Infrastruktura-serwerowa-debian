# 🏢 Company Intranet & Active Directory Infrastructure

Kompleksowy projekt środowiska klient-serwer opartego na systemach operacyjnych Linux (Debian 11) oraz Windows 10/11. Projekt symuluje w pełni funkcjonalną, bezpieczną sieć firmową (domenę `firma.local`) z centralnym zarządzaniem tożsamością, usługami sieciowymi oraz autorskim systemem kontroli wersji.

## 🛠️ Wykorzystane Technologie

* **Serwer:** Debian 11 (CLI)
* **Klient:** Windows 10/11 (32/64-bit)
* **Zarządzanie domeną:** Samba 4 (Active Directory Domain Controller)
* **Sieć i bezpieczeństwo:** WireGuard (VPN), UFW (Firewall), ISC-DHCP-Server
* **Usługi produkcyjne:** Gitea (Git server + SQLite3), Apache2 (Web Server), CUPS (Print Server)
* **Archiwizacja:** BorgBackup + Cron
* **Wirtualizacja:** Oracle VirtualBox (sieć NAT + Sieć wewnętrzna)

## ⚙️ Główne funkcjonalności

1. **Active Directory (Samba AD DC):**
   * Centralne zarządzanie użytkownikami i stacjami roboczymi w domenie `firma.local`.
   * Skonfigurowany wewnętrzny serwer DNS na potrzeby uwierzytelniania Kerberos.

2. **Zarządzanie siecią (DHCP & VPN):**
   * Automatyczna adresacja IPv4 i IPv6 dla stacji klienckich.
   * Wdrożony protokół WireGuard umożliwiający bezpieczny, szyfrowany dostęp z zewnątrz (tunelowanie VPN).

3. **Udostępnianie zasobów:**
   * **Pliki:** Zasoby sieciowe udostępniane przez protokół SMB z wymuszonym szyfrowaniem ruchu (`smb encrypt = required`).
   * **Drukarki:** Udostępnianie drukarek w sieci lokalnej przy pomocy serwera CUPS.
   * **Intranet:** Firmowa strona WWW serwowana przez Apache2.

4. **Kontrola wersji (Gitea):**
   * Lekki, lokalny serwer Git działający jako usługa `systemd`.
   * Baza danych oparta na SQLite3, w pełni odizolowana konfiguracja uprawnień (dedykowany użytkownik `git`).

5. **Bezpieczeństwo i Backup:**
   * Skonfigurowana zapora sieciowa UFW filtrująca ruch i otwierająca wyłącznie niezbędne porty (m.in. 53, 80, 51820, SMB).
   * Automatyczne, deduplikowane kopie zapasowe zasobów współdzielonych realizowane cyklicznie przez narzędzie BorgBackup.

## 🚀 Uruchomienie i testy

Projekt został zaprojektowany z myślą o uruchomieniu w środowisku wirtualnym (np. VirtualBox). 
Testy integracyjne wykonane na maszynie klienckiej (Windows) potwierdzają:
* Poprawne pobieranie adresacji z serwera DHCP.
* Sukces dołączenia do domeny AD.
* Dostęp do szyfrowanych udziałów sieciowych SMB oraz firmowego intranetu.
* Możliwość klonowania repozytoriów Git bezpośrednio z lokalnego serwera Gitea.

## 📦 Środowisko testowe (.ova)
Gotowe maszyny wirtualne z zainstalowanym i skonfigurowanym systemem można pobrać tutaj:
* [Pobierz serwer Debian 11 (.ova) - Dysk Google](twój_link_tutaj)
* [Pobierz stację kliencką Windows 10 (.ova) - Dysk Google](twój_link_tutaj)

*Hasła dostępowe:*
* **Debian root:** `zaq1@WSX`
* **Windows / AD:** nie posiada hasła
