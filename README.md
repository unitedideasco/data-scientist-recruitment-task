# Data Science Summer Internship Recruitment Task

## Podstawowe pojęcia

* Arbitraż - kupowanie w jednym miejscu taniej, a w drugim sprzedawanie, równocześnie:
    * https://pl.wikipedia.org/wiki/Arbitra%C5%BC_(ekonomia)
    * http://money.howstuffworks.com/personal-finance/financial-planning/arbitrage.htm
    * https://www.youtube.com/watch?v=AuCH7fHZsZ4
* Bid - jest to cena po której otwierane są zlecenia sprzedaży i zamykane zlecenia kupna. Ask - jest to cena po której otwierane są transakcje kupna i zamykane transakcje sprzedaży. Spread - jest to różnica pomiędzy ceną kupna (Ask), a ceną sprzedaży (Bid).
* Long - gdy coś kupujemy, oczekując że kurs wzrośnie
* Short - gdy coś sprzedajemy, spodziewając się spadku
* Short Selling - krótka sprzedaż - sprzedawanie czegoś czego nie mamy - rodzaj transakcji giełdowej która umożliwia nam zarabianie na spadku. W praktyce polega to na tym że pożyczamy i obstawiamy spadek. Tutaj wyjaśnienie jak to działa: http://www.investopedia.com/terms/s/shortselling.asp

Ważne info: Rozróżnienie to ma ogromne znaczenie dla rozliczania transakcji. Należy pamiętać, że kupując dany instrument (otwierając pozycję długą) transakcja zostanie zawarta po cenie Ask (wyższej). Zawarcie transakcji sprzedaży odbywa się zawsze po cenie Bid. Zamknięcie pozycji długiej następuje po kursie Bid, krótkiej zaś po cenie Ask.

## Algorytm arbitrażu

TL;DR: Arbitraż polega na kupowaniu taniej sprzedawaniu drożej

1. Załóżmy że mamy taki stan początkowy:
    * $1000.00 do dyspozycji
    * 0 kg jabłek
2. W celu uproszczenia tematu, zakładamy że możemy robić krótką sprzedaż jabłek :-)
3. W pewnym momencie obserwowania kursów zauważamy że:
  1. Na Targowisku 1: Jabłka mają kurs sprzedaży (ask) $1.39297 i kupna (bid) $1.39279 (podane kursy za kilogram jabłek)
  2. Na Targowisku 2: Jabłka mają kurs sprzedaży (ask) $1.38297 i kupna (bid) $1.38279 (podane kursy za kilogram jabłek)
  3. Wygląda na to, że możemy kupić na Targowisku 2 taniej, a na Targowisku 1 sprzedać drożej, dla ułatwienia zakładamy w tym momencie że jest pewna  różnica kursu przy której w ogóle będziemy otwierać transakcję, nazwijmy ją X - mniejszy "rozjazd" niż X nas nie interesuje, i nie będziemy w ogóle tego uważali za oportunity po które warto się schylać
  4. W takim razie, otwieramy dwie transakcje jednocześnie:
    1. Otwieramy na kwotę $500.00 transakcję kupna (long) na Targowisku 2
    2. Otwieramy za kwotę $500.00 transakcję sprzedaży (short) na Targowisku 1
    3. W tym momencie teoretycznie zarobiliśmy, ale po otwarciu obu transakcji:
      1. Mamy (wirtualne) jabłka na Targowisku 2 - tyle ile udało się kupić za $500
      2. Mamy (wirtualne) dolary na Targowisku 1 - tutaj zrobiliśmy krótką sprzedaż, zatem musimy "sprzedać" tyle kilogramów jabłek ile kupiliśmy na Targowisku 2 za dolary
  5. W tym momencie jesteśmy w trakcie arbitrażu, ale potrzebujemy wrócić do stanu początkowego, to znaczy mieć znowu dolary a nie kontrakty na dolary i kontrakty short na jabłka
  6. Czekamy zatem na kolejne oportunity aż kursy się znowu rozjadą o jakiś sensowny przedział (bo mniejszy nas w ogóle nie będzie interesował), nazwijmy go Y
  7. Zamykamy wtedy transakcje na obu targowiskach, dzięki czemu jesteśmy spowrotem z dolarami w ręku i bez jabłek
  8. Załóżmy że na tej transakcji zarobiliśmy $100.00 dolarów (takie były różnice), w takim razie mamy $1100.00 na koncie
  9. Możemy czekać na następne oportunities

## Twoje zadanie

Do tego zadania są załączone pliki CSV. Zawierają one kursy jabłek z 7 targowisk. Bazując na dostarczonych danych z różnych źródeł, zaproponuj najbardziej efektywną strategię arbitrażu. Zakładamy że zaczynasz z kwotą $1000 w pierwszym dniu wspomnianym w plikach (27 kwietnia). Twój cel to mieć jak największą kwotę na koniec (28 maja) okresu danych.

Metoda rozwiązania tego zadania jest dowolna, można używać absolutnie wszystkiego.

Następnie:

* Rezultat zadania wrzuć na dostępne publicznie repozytioum na GitHub (kod zrodlowy) + plik README.md z opisem jak to zostało zrobione / jak uruchomić test
* Umów naszą następną rozmowę za [tego formularza](https://calendly.com/chojnowski/recruitment-task-first-review) - tam jest też pole do wpisania linka do Twojego repozytorium - będziemy rozmawiać o wykonanym zadaniu, dlaczego zostały zastosowane takie a nie inne rozwiązania

## Protips

1. Zakresy dat w plikach nie zawsze sie pokrywaja, niektore targowiska nie dzialaja w sposob ciagly
2. Można optymalizować conajmniej te parametry:
    1. Ilosc uzywanego kapitalu do kupowania/sprzedawania
    2. Minimalna roznica dla otwarcia transakcji
    3. Minimalna roznica dla zamkniecia transakcji
    4. Maksymalny czas kiedy mamy otwarta transakcje - kiedy nie pojawi sie oportunity dla zamkniecia, i tak zamykamy pozycje aby mozna bylo otwierac kolejne transakcje
    5. Alokacja kapitalu miedzy targowiskami - niektore ich pary generują większe okazje między sobą, niektóre mniejsze
3. I oczywiście inne według Twojej kreatywności :-)
4. Pamiętaj o tym że $1000.00 (lub inna kwota kapitału którą masz) musi zostać podzielona między targi - nie możesz z $1000.00 iść jednocześnie na dwa targowiska i zrobić tymi samymi pieniędzmi kupna i sprzedaży, przy dwóch targach musisz to podzielić na $500.00

Powodzenia!
