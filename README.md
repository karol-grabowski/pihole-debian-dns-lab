
# 🛡️ Konfiguracja Pi-hole jako Serwera DNS w Odizolowanej Podsieci (Debian 12)

![Debian](https://img.shields.io/badge/OS-Debian%2012-A81D24?style=flat&logo=debian&logoColor=white)
![Pi-hole](https://img.shields.io/badge/DNS-Pi--hole-Red?style=flat&logo=pi-hole&logoColor=white)
![VirtualBox](https://img.shields.io/badge/Virtualization-VirtualBox-Blue?style=flat&logo=virtualbox&logoColor=white)

## Opis Projektu
Projekt obejmuje wdrożenie i konfigurację dedykowanego serwera DNS (DNS Sinkhole) opartego na systemie **Debian 12** oraz oprogramowaniu **Pi-hole** w środowisku wirtualnym (VirtualBox). 

Celem wdrożenia było zabezpieczenie maszyny klienckiej przed złośliwym oprogramowaniem, śledzeniem oraz niepożądanymi treściami poprzez filtrowanie zapytań DNS na poziomie infrastruktury z wykorzystaniem oficjalnych feedów bezpieczeństwa od **CERT Polska**.

---

## Architektura i Konfiguracja Środowiska

Środowisko składa się z dwóch maszyn wirtualnych z systemem **Debian 12** pracujących w jednej podsieci:

1. **Maszyna 1 (Serwer DNS / Pi-hole):**
   * Zainstalowane i skonfigurowane środowisko Pi-hole.
   * Dostęp do panelu administracyjnego z poziomu przeglądarki.
   * Dodana oficjalna czarna lista domen identyfikowanych jako złośliwe dostarczana przez **CERT Polska** (`http://hole.cert.pl/domains/domains_hosts.txt`).
   * Przeprowadzona aktualizacja bazy blokowania za pomocą mechanizmu *Gravity Update* w menu `Tools -> Update Gravity`.

2. **Maszyna 2 (Klient):**
   * Wyłączone automatyczne uzyskiwanie adresów serwera DNS (DHCP).
   * Ręcznie skonfigurowany statyczny adres DNS wskazujący bezpośrednio na serwer Pi-hole (Maszyna 1).

---

## Zrzuty Ekranu / Dokumentacja

<img width="1148" height="820" alt="Panel główny Pi-hole" src="https://github.com/user-attachments/assets/bf3ff8f5-8a1f-4e29-bdcf-26fa96bbf62f" />

*Rysunek 1: Panel główny Pi-hole z widocznymi statystykami zablokowanych domen.*

<img width="1156" height="780" alt="Dodanie czarnej listy CERT Polska" src="https://github.com/user-attachments/assets/c4d49952-8110-4c9f-b0c4-d1a1ec5d3d62" />

*Rysunek 2: Dodanie czarnej listy CERT Polska w sekcji Adlists oraz aktualizacja bazy Gravity.*

<img width="1090" height="775" alt="Ręczna konfiguracja DNS" src="https://github.com/user-attachments/assets/2f7b5e4b-19c6-4448-9864-519668f9b4f8" />

*Rysunek 3: Ręczna konfiguracja DNS na maszynie klienckiej wskazująca na serwer Pi-hole.*
---

## Podsumowanie i Wnioski Inżynierskie
Stosowanie rozwiązania typu Pi-hole w odizolowanej lub domowej podsieci znacząco poprawia bezpieczeństwo oraz prywatność użytkowników:
* **Filtrowanie ruchu u źródła:** Zapytania do złośliwych lub śledzących domen są blokowane na poziomie DNS, zanim pakiety trafią do przeglądarki.
* **Integracja z Threat Intelligence:** Wykorzystanie listy CERT Polska chroni przed aktywnymi kampaniami phishingowymi i złośliwym oprogramowaniem w polskiej przestrzeni internetowej.
* **Redukcja ryzyka:** Ograniczenie ilości zbieranych danych oraz ochrona przed natrętnymi reklamami i próstymi wyłudzeniami danych.
