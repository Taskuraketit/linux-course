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

Lähdeviitteet tarkistettu ja puutteet korjattu.

# c) Laita Linuxiin uusi, itse tekemäsi komento niin, että kaikki käyttäjät voivat ajaa sitä.

Loin ensin tiedoston 'laskuri.sh' sijaintiin /usr/local/bin/

> $ sudo micro /usr/local/bin/laskuri.sh

<img width="582" height="76" alt="image" src="https://github.com/user-attachments/assets/19ee064a-43ff-4a63-8425-5a6dd59bd378" />

Tiedoston sisältö (tallennus luonnin jälkeen):

<img width="307" height="178" alt="image" src="https://github.com/user-attachments/assets/c732c597-7a81-4ff6-86f8-8c6aee4c97b3" />

Suoritusoikeuksien lisääminen kaikille käyttäjille (a = all)

> $ sudo chmod a+x /usr/local/bin/laskuri.sh

<img width="627" height="149" alt="image" src="https://github.com/user-attachments/assets/36594c88-d70c-4053-8636-4ebb101772d1" />

Tiedoston suorittaminen:

> $ laskuri.sh

<img width="702" height="230" alt="image" src="https://github.com/user-attachments/assets/9d0f82c5-03f0-4267-9229-6a623f0bca22" />

...ja sehän toimi kuin junan vessa :)

# d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.

**Tätä tehtävää varten valitsin soveltuvin osin tehtäväksi vanhan laboratorioharjoituksen 'Arvioitava laboratorioharjoitus – Linux palvelimet ict4tn021-7 tiistai – alkukevät 2018 – 5 op'. Tein tehtäväkokonaisuuden Linux-virtuaalikoneellani (en palvelimella).**

  \## Työntekijät
  
  *Työntekijöitämme ovat Joe Doe, Jorma Mähkylä, Pekka Hurme, Ronaldo Smith,Håkan Petersson ja Einari Mikkonen. Laita einarin käyttäjätunnukseksi "einari". Tee kullekin käyttäjälle esimerkkikotisivu.*

Yksinkertaistuksen vuoksi loin vain Einarin ja tarkistin, että hänelle muodostui oma kotihakemisto.

> $ sudo adduser einari
>
> ls -ld /home/einari
>
> grep einari /etc/passwd

<img width="658" height="379" alt="image" src="https://github.com/user-attachments/assets/7847d9a0-be93-4c22-a7af-52f31d866d5d" />

Seuraavaksi loin Einarille esimerkkisivut. Aloitin tämän userdir-moduulin aktivoinnilla

> $ sudo a2enmod userdir
>
> $ sudo systemctl restart apache2

<img width="802" height="222" alt="image" src="https://github.com/user-attachments/assets/9bf32b65-4e87-49b0-9bc2-f5d9dc6454d1" />

Loin Einarille public_html-kansion

> $ sudo -u einari mkdir /home/einari/public_html

Seuraavaksi loin varsinaisen nettisivun Einarille

<img width="1244" height="63" alt="image" src="https://github.com/user-attachments/assets/957b652e-26aa-442c-9e91-97a0e6baae89" />

Seuraavaksi muokkasin kansion oikeuksia

> $ sudo chmod -R 755 /home/einari/public_html

<img width="659" height="39" alt="image" src="https://github.com/user-attachments/assets/c764a735-7965-49c5-afd2-5dfd106656d5" />


Tässä 
- -R tekee muutoksen rekursiivisesti eli kaikille alihakemistoille ja tiedostoille kyseisessä hakemistossa
- 755 antaa omistajalle (einari) oikeudet: luku (r), kirjoitus (w), suoritus (x) ja ryhmälle sekä muille käyttäjille: luku (r), suoritus (x)


Tarkistin vielä tiedoston sisällön ja siistin tekstin rivitystä, minkä jälkeen käynnistin apache2:n uudelleen.

> $ micro index.html
>
> $ sudo systemctl restart apache2

<img width="382" height="199" alt="image" src="https://github.com/user-attachments/assets/083cc031-104a-4198-ba92-aaddd698d37b" />

<img width="756" height="136" alt="image" src="https://github.com/user-attachments/assets/1e16cc91-aabf-49e0-8113-be68063bf508" />

Tämän jälkeen nettisivu näkyi oikein localhostilla:

<img width="562" height="188" alt="image" src="https://github.com/user-attachments/assets/30de3a6d-3b47-46f9-97d2-f05285b3cc3c" />

 
  *\## LAMP*
  
  *Asenna LAMP - Linux, Apache, MySQL, PHP. Tee einarin kotihakemistoon esimerkkisovellus, joka näyttää tietueita tietokannasta.*

  Tätä ei käyty kurssilla läpi joten jätin tämän kohdan väliin.
  
  \## invis.example.com
  
  Laita Einarin esimerkkisovellus näkymään osoitteesta http://invis.example.com. Voit simuloida nimipalvelun toimintaa hosts-tiedoston avulla.

  Tätä ei käyty kurssilla läpi joten jätin tämän kohdan väliin.
  
  \## mitakello
  
  *Tee uusi komento 'mitakello', joka tulostaa kellonajan. Komennon tulee toimia kaikilla käyttäjillä, kaikista hakemistoista pelkällä nimellä kutsuttuna.*

Skriptin luonti:

  > $ sudo micro /usr/local/bin/mitakello

Skriptin sisältö:

<img width="313" height="121" alt="image" src="https://github.com/user-attachments/assets/23db5b27-197a-4823-adcc-9c46f1d279f5" />

Suoritusoikeuksien säätö:

> $ sudo chmod a+x /usr/local/bin/mitakello

Skriptin testaus:

> $ mitakello

<img width="617" height="82" alt="image" src="https://github.com/user-attachments/assets/f01d6475-86d8-4b0d-852b-8c75ad893c2a" />




  \## Metapaketti
  
  Tee meille metapaketti, joka asentaa ohjelmat: git, httpie, curl, mitmproxy.
  
  Kuulemma "karvinen equivs" hakusanalla saattaisi löytyä ohjeita. Liitä metapaketin lähdekoodi palautettavan lab.txt:n loppuun. 
  
  \## unikarhu.example.com
  
  Laita staattinen html5-esimerkkisivu näkyviin osoitteeseen http://unikarhu.example.com. Voit simuloida nimipalvelun toimintaa hosts-tiedoston avulla.
  
  \## bonuskuorma
  
  Mittaa koneesi kuormitusta työkalulla, joka kerää kuormitustietoja yli ajan
  
  (ei pelkästään yhdellä hetkellä). Kuormita konetta haluamallasi tavalla, ja etsi kuormitustieto työkalusi keräämästä historiasta.
  
  \## Metapaketin uusi nimi
  
  Muuta metapaketin nimeksi xoy-tools. Asenna se.



# Lähteet

**Heinonen, J. s.a.** Linux Shell Scripting Basics. Luettavissa: https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-01102025.md. Luettu: 1.10.2025.

**Karvinen, T. s.a.** Linux Palvelimet 2025 alkusyksy. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu: 1.10.2025.

**Karvinen, T. 13.3.2018.** Arvioitava laboratorioharjoitus – Linux palvelimet ict4tn021-7 tiistai – alkukevät 2018 – 5 op. Luettavissa: https://terokarvinen.com/2018/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-7-tiistai-alkukevat-2018-5-op/. Luettu: 5.10.2025.

