# a) Kirjoita ja aja "Hei maailma" kolmella kielellä.

## 1) Linux Shell script

Ensin loin Microlla tiedoston helloworld.sh

> $ micro helloworld.sh

<img width="403" height="70" alt="image" src="https://github.com/user-attachments/assets/3519578a-2369-4ad7-8c1e-460335c09380" />

Lisättyäni skriptiin sisältöä tallensin tiedoston.

<img width="322" height="156" alt="image" src="https://github.com/user-attachments/assets/b7b855b5-739d-4c0d-aacd-d09b5b520737" />

Seuraavaksi tarkistin tiedoston suoritusoikeudet ja lisäsin siihen peruskäyttäjän suoritusoikeudet.

> $ ls -l helloworld.sh
>
> $ chmod ugo+x helloworld.sh

Seuraavaksi ajoin ohjelman ja totesin skriptin toimivaksi

> $ ./helloworld.sh

<img width="403" height="90" alt="image" src="https://github.com/user-attachments/assets/cfe98b78-4140-4f55-982d-36586ccf4541" />

## 2) Python

Loin Microlla tiedoston helloworld.py

> $ micro helloworld.py

<img width="402" height="73" alt="image" src="https://github.com/user-attachments/assets/c9ab194c-c390-47dc-bd49-9db31d3359bd" />

Lisäsin tiedostoon sisältöä ja tallensin tiedoston.

<img width="331" height="104" alt="image" src="https://github.com/user-attachments/assets/e6d40230-5327-4786-b87d-2898402124e9" />

Suoritin tiedoston ja totesin sen toimivaksi ilman erillisiä oikeusmäärittelyjä.

> $ python3 helloworld.py

<img width="428" height="149" alt="image" src="https://github.com/user-attachments/assets/0955482b-e56d-4a82-a084-ce47fa7d907e" />


## 3) C++

C++:aa varten päivitin ensin asennuspaketit ja asensin ohjeen mukaisesti tiedoston build-essential-ohjelmiston.

> $ sudo apt-get update
>
> $ sudo apt-get install -y build-essential

<img width="814" height="377" alt="image" src="https://github.com/user-attachments/assets/0d595333-6f65-4c5b-b90d-adaaf2080f1d" />

Tulosteesta huomasin, että olinkin jo asentanut sen aiemmin.

Seuraavaksi loin Microlla tiedoston helloworld.cpp

> $ micro helloworld.cpp

Loin tiedostoon sisältöä ("käsin", koska en ole saanut lukuisista yrityksistä huolimatta virtuaalikoneellani shared clipboardia toimimaan):

<img width="713" height="185" alt="image" src="https://github.com/user-attachments/assets/242b700a-582d-443b-bcb6-052547b84b9b" />

Seuraavaksi käänsin lähdekoodin suoritettavaksi ohjelmaksi käyttäen GNU C++ kääntäjää

> $ g++ helloworld.cpp -o helloworld

Tämän jälkeen suoritin ohjelman ja totesin sen toimivaksi. Tässäkään ei tarvittu erillisiä oikeusmäärittelyjä.

> $ ./helloworld

<img width="582" height="73" alt="image" src="https://github.com/user-attachments/assets/50dd8ff7-061d-4460-b3f4-ae853a38ecbd" />


# b) Lähdeviitteet. Tarkista ja tarvittaessa lisää lähdeviitteet kaikkiin raportteihisi h1 alkaen. Tarkista, että olet viitannut lähteisiin: tehtäväsivuun, kurssiin, muiden opiskelijoiden raportteihin, man-sivuihin, kotisivuihin ja ylipäänsä kaikkiin käyttämiisi lähteisiin. Lähdeviite tulee olla jokaisessa raportissa tai sivussa, jossa lähdettä on käytetty. Kaikki tehtävät perustuvat tämän sivun tehtävänantoihin, joten ainakin tämä viite on syytä löytyä. (Tästä alakohdasta ei tarvitse kirjoittaa vaiheittaista raporttia)


# c) Laita Linuxiin uusi, itse tekemäsi komento niin, että kaikki käyttäjät voivat ajaa sitä.


# d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.
