---
title: 'Konfiguracja zapory sieciowej Network Firewall'
excerpt: 'Dowiedz się, jak skonfigurować reguły firewalla w OVH'
slug: network-firewall
section: 'Sieć & IP'
---

> [!primary]
> Tłumaczenie zostało wygenerowane automatycznie przez system naszego partnera SYSTRAN. W niektórych przypadkach mogą wystąpić nieprecyzyjne sformułowania, na przykład w tłumaczeniu nazw przycisków lub szczegółów technicznych. W przypadku jakichkolwiek wątpliwości zalecamy zapoznanie się z angielską/francuską wersją przewodnika. Jeśli chcesz przyczynić się do ulepszenia tłumaczenia, kliknij przycisk „Zaproponuj zmianę” na tej stronie.
>

**Ostatnia aktualizacja z dnia 23-12-2021**

## Wprowadzenie

Aby chronić swoją globalną infrastrukturę oraz serwery klientów, OVHcloud udostępniło zaporę ogniową, z możliwością wprowadzenia własnej konfiguracji, w pełni zintegrowaną z rozwiązaniem **Anty-DDoS (VAC)**: Network Firewall . Jest to rozwiązanie filtrujące ataki z sieci publicznej na usługi naszych klientów.

**Ten przewodnik wyjaśnia, jak skonfigurować zaporę Network Firewall w Panelu klienta.**


> [!primary]
>
> Więcej informacji o rozwiązaniu DDoS, znajdziesz na stronie: <https://www.ovh.pl/anti-ddos/>.
> 

![Szczegóły dotyczące systemu VAC](images/vac-inside.png){.thumbnail}


## Wymagania początkowe

- Korzystanie z usługi OVHcloud ze zintegrowaną zaporą ogniową, Network Firewall: ([serwer dedykowany](https://www.ovh.pl/serwery_dedykowane/){.external}, [serwer VPS](https://www.ovh.pl/vps/){.external}, [instancje Public Cloud](https://www.ovh.pl/public-cloud/instances/){.external}, [Private Cloud](https://www.ovh.pl/private-cloud/){.external}, [IP Failover](https://www.ovh.pl/serwery_dedykowane/ip_failover.xml){.external}, etc.)
- Dostęp do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external}


## W praktyce

### Aktywacja zapory Network Firewall 

> [!primary]
>
> Network Firewall chroni adresy IP powiązane z serwerem.  Należy zatem skonfigurować reguły dla każdego adresu IP oddzielnie. Wprowadzenie wspólnej konfiguracji dla całego serwera nie jest możliwe.
> 

Zaloguj się do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl), kliknij menu `Bare Metal Cloud`{.action}, a następnie sekcję `IP`{.action} w dolnej części kolumny po lewej stronie. Kliknij `...`{.action}, aby aktywować zaporę na wybranym adresie IPv4.

![Aktywacja Network Firewall ](images/firewall_creation.png){.thumbnail}

Następnie wymagane jest potwierdzenie.

![Zatwierdzenie](images/creationvalid.png){.thumbnail}

Następnie kliknij przycisk `Aktywuj firewall`{.action} (1), po czym wybierz `Skonfiguruj firewall`{.action} (2) i rozpocznij konfigurację.

![Uruchomienie konfiguracji](images/activationconfig.png){.thumbnail}

Do dyspozycji masz **20 reguł dla każdego adresu IP**.

> [!warning]
>
> Firewall uruchamia się automatycznie przy każdym ataku DDoS i nie można go wyłączyć przed zakończeniem ataku.  Dlatego ważne jest, aby reguły firewalla były aktualne. 
> Domyślnie, żadne reguły nie są skonfigurowane, więc można ustanowić dowolne połączenia z serwerem. 
> Kiedy korzystasz z firewalla, pamiętaj o regularnym sprawdzaniu reguł (jeśli je ustawiłeś), nawet jeśli jest on w danej chwili dezaktywowany.
> 

> [!primary]
>
> - Fragmentacja UDP jest domyślnie zablokowana (DROP).  Jeśli używasz sieci VPN, to podczas aktywacji firewalla, pamiętaj, aby poprawnie skonfigurować maksymalną jednostkę transmisji (MTU). Na przykład na OpenVPN możesz zaznaczyć `MTU test`{.action}.
> - Reguły skonfigurowane w Network Firewallu nie są brane pod uwagę wewnątrz sieci OVHcloud.  Wprowadzone reguły nie mają wpływu na połączenia w wewnętrznej sieci OVHcloud.
>


### Konfiguracja zapory Network Firewall 

Dodawanie reguły odbywa się przez kliknięcie po prawej stronie `Dodaj regułę`{.action}.

![Dodawanie reguły](images/ajoutregle1.png){.thumbnail}

Dla każdej reguły możesz wybrać:

- priorytet (od 0 do 19, gdzie 0 jest pierwszą zastosowaną regułą);
- akcja (`Zezwalaj`{.action} lub `Odrzucaj`{.action});
- protokół
- IP (opcjonalnie);
- port źródłowy (tylko dla TCP);
- port docelowy (tylko dla TCP);
- opcje TCP (tylko dla TCP).

![Szczegóły dotyczące dodania reguły](images/ajoutregle4.png){.thumbnail}


> [!primary]
>
> - Priorytet 0: zaleca się autoryzację protokołu TCP dla wszystkich IP z opcją `Established`{.action}. Opcja `Established`{.action} umożliwia sprawdzenie, czy pakiet jest częścią poprzednio otwartej sesji (już zainicjowanej).  Jeśli na to nie zezwolisz, serwer nie otrzyma zwrotów protokołu TCP z żądań SYN/ACK.
> 
> - Priorytet 19: odrzucenie całego protokołu IPv4, jeśli nie zostanie spełniona żadna reguła przed 19-tą (ostatnią możliwą).
> 

### Przykład konfiguracji

Aby pozostawić otwarte tylko porty SSH (22), HTTP (80), HTTPS (443), UDP (na porcie 10000), zezwalając na ICMP, należy przestrzegać następujących zasad:

![Przykład konfiguracji.](images/exemple.png){.thumbnail}

Reguły są uporządkowane chronologicznie, od 0 (pierwsza odczytana reguła) do 19 (ostatnia odczytana reguła) i w tym porządku są uruchamiane dla pakietów.  Reguły przestają być sprawdzane, w chwili gdy jedna z nich dotyczy odebranego pakietu.

Na przykład pakiet przeznaczony dla portu 80/TCP zostanie przechwycony przez regułę 2, wtedy kolejne reguły nie są już aplikowane.  Pakiet przeznaczony dla portu 25/TCP zostanie przechwycony tylko przy ostatniej regule (19), która zablokuje go, ponieważ OVHcloud nie zezwala na żadną komunikację na porcie 25 w poprzednich regułach.

> [!warning]
>
> W chwili gdy włącza się ochrona Anty-DDoS, Twoje reguły zdefiniowane w usłudze Network Firewall zostaną uaktywnione, nawet jeśli je wyłączyłeś. W przypadku dezaktywacji firewalla, pamiętaj o usunięciu reguł.
> 

### Konfiguracja zapory Armor (Firewall Game)

> [!primary]
> Domyślnie firewall Armor jest wstępnie skonfigurowany z niektórymi zasadami, które OVHcloud ustalił podczas uruchamiania najpopularniejszych gier. Jednak w przypadku klientów posiadających serwer dedykowany Game możemy pójść o krok dalej i skonfigurować reguły dla portów.
>

Aby skonfigurować reguły portów w trybie Armor, należy najpierw zalogować się do Panelu klienta OVHcloud.<br>
Następnie przejdź do menu `Bare Metal Cloud`{.action} i kliknij sekcję `IP`{.action} na pasku bocznym po lewej stronie. Kliknij `...`{.action} obok adresu IP serwera gier, a następnie `Konfiguracja firewall game`{.action}.

![Game_wall](images/GAMEwall2021.png){.thumbnail}

Na następnym ekranie kliknij przycisk `Dodaj regułę`{.action}, aby dodać regułę do Armor.

![Konfiguruj_Armor](images/ConfigureArmor2021.png){.thumbnail}

Włącz porty zgodnie z Twoimi potrzebami na kolejnym ekranie i kliknij przycisk `Zatwierdź`{.action}, gdy zakończysz dodawanie reguł. Firewall Armor został już skonfigurowany.

## Sprawdź również

Przyłącz się do społeczności naszych użytkowników na stronie <https://community.ovh.com/en/>.