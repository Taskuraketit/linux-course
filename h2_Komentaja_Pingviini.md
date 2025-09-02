# h2 Komentaja Pingviini 
## x) Lue ja tiivistä (Muutama ranskalainen viiva riittää. Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella. Lisää jokin oma kysymys, idea tai huomio). Karvinen 2020: Command line basics revisited (nämä komennot ja hakemistot kannattaa myös opiskella ulkoa ja harjoitella automaatiotasolle)

### Yhteenveto
Linuxin tärkeimmät komennot on syytä opetella ulkoa, jotta operointi Linuxin komentokehotteessa käy sujuvasti. Kopiointi-, siirto- ja poistokomennot ovat loppujen lopuksi loogisia ja yksinkertaisia kunhan niitä tottuu käyttämään.
Erityisesti poistolauseiden kanssa ons syytä olla varovainen, koska poisto tapahtuu yleensä **ilman varoituksia tai varmisteluja**. Tämän tehtävän tekemisestä minulle jäi fiilis, että haluan tehdä lisää Linux-aiheisia muistiinpanoja tärkeistä komennoista ja toiminnoista.

### Tiivistelmä

Linuxista löytyy useita eri komentoja, joista tärkeimmät on syytä opetella ulkoa niin, että ne Linuxin komentokehotteella operoidessa tulevat automaattisesti. Alla yleisiä komentoja ja huomioita:

**Hakemistoissa liikkuminen**
- promptin alussa on aina dollarimerkki $, jota ei tarvitse kirjoittaa erikseen
- *$ pwd* -> näyttää missä hakemistossa liikutaan parhaillaan
- *$ ls* -> listaa hakemiston tiedostot ja alahakemistot
- *$ cd kansio/* -> siirtyy cd:n jälkeiseen kansioon
- *$ cd ..* -> siirrytään hakemistopuussa yhtä ylempään hakemistoon
- *$ less filu.txt* -> avaa tekstiteidoston selaustilassa. Välilyönnistä siirtyy seuraavalle sivulle, b:stä palaa edelliselle sivulle, kenoviivalla "/" pystyy etsimään ja q-kirjaimesta poistutaan tiedostosta.
- Minkä tahansa komennon tulosteen voi lukea sivu kerrallaan ohjaamalla sen less-ohjelmaan putkella (|), esim.  */etc/|less*

**Tiedostojen manipulointi**
- *$ nano filu.txt* -> komento käynnistää tekstitiedoston nano-tekstieditorissa. Jos kyseistä tiedostoa ei löydy, se luodaan.
- *$ mkdir uusikansio* -> luo uuden kansion nimeltä 'uusikansio'
- *$ mv VANHANIMI UUSINIMI* -> jos UUSINIMI on olemassaoleva hakemisto, VANHANIMI siirretään sen sisälle. Jos UUSINIMI ei ole olemassa, VANHANIMI nimetään UUSINIMI:ksi.
- *$ mv FILU KANSIO/* -> siirtää filu-tiedoston kansioon 'KANSIO'
- *$ cp -r ALKUP KOPIO* -> rekursiivinen kopiointi eli jos ALKUP on hakemisto, koko hakemisto kopioidaan alihakemistoineen
- *$ rmdir TYHJA* -> poistaa tyhjän kansion TYHJA
- *$ rm ROSKA* -> poistaa ROSKA-tiedoston
- *$ rm -r ROSKAKANSIO/* -> poistaa kansion ROSKAKANSIO sisältöineen

**SSH Etäyhteys**
- *$ ssh sopuli@example.com* -> avaa SSH-yhteyden sopuli-käyttäjänimelle example.com-serverille
- komennolla *'w'* näet etäkoneen muut käyttäjät
- *remotecomputer$ exit* -> exit-komennolla palataan omalle koneelle
- *$ scp -r FOLDER sopuli@example.com:public_html/* -> komennolla kopioidaan kansio turvallisesti etäkoneelle
  
**Apukomennot**
- *$ man ls* -> näyttää komennon manuaalin
- muita apukomentoja ovat *'$ ls --help'* ja *'$ wget -h'*

**Historia ja ennakoiva syöttö**
- Painamalla tabulaattoria kahdesti näkee mitä voi kirjoittaa seuraavaksi
> $ ls /etc/re[tab][tab]
> 
> reportbug.conf  resolvconf/     resolv.conf

- Tabulaattori myös täydentää komennon silloin kun se on *yksiselitteinen*
> $ ls /etc/resolv.[tab]
> 
> $ ls /etc/resolv.conf 

- tabulaattorin käyttö on suotavaa kirjoitusvirheiden välttämiseksi
- ylänuoli näyttää edellisen komennon, liikkumalla vasemmalla ja oikealla nuolella pystyy muokkaamaan komentoriviä
- ajettujen komentojen historian näkee komennolla *'$ history'*

**Tärkeimmät hakemistot**
Tästä tarkempi selostus alla kohdassa c)

**Hallinnointikomentoja**
- *$ sudo apt-get update* -> päivittää asennettavien ohjelmien listan
- *$ sudo apt-cache search <ohjelman nimi>* -> etsii ohjelmia hakusanalla
- *$ sudo apt-get -y install <ohjelman nimi>* -> asentaa ohjelman vastaten "y" (=kyllä) kysymyksiin
- *$ $ dpkg --listfiles <ohjelman nimi>* -> Graafisessa käyttöliittymässä monet ohjelmat näkyvät siellä. Komentoriviohjelmat eivät yleensä näy siellä, joten käyttäjän täytyy tietää oikea komento ohjelman käynnistämiseen.

  
## a) Micro. Asenna micro-editori.
**Pakettiluettelon päivitys**

<img width="1144" height="288" alt="image" src="https://github.com/user-attachments/assets/6aa8f992-2169-4e5c-826d-512298db7532" />

**Micron asennus**

Tästä valitettavasti puuttuu kuvakaappaus, mutta käytin komentoa *'$ sudo apt-get install -y micro'*



**Micron testaus**

<img width="594" height="471" alt="image" src="https://github.com/user-attachments/assets/a7c052ad-475f-410f-b0d4-c19a63d027d3" />



<img width="1146" height="708" alt="image" src="https://github.com/user-attachments/assets/ef1a2e06-7263-4b4b-8342-069e20a3d8eb" />



## b) Apt. Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla?

**Kolmen ohjelman asennus**

Koska Linux-ohjelmien tuntemukseni on heikkoa, kysyin ChatGPT:ltä vinkkejä mitä komentorivityökaluja kannattaa asentaa. ChatGPT:n ehdotuksista poimin seuraavat jotka kuulostivat houkuttelevimmilta:
- **glances**: Laajempi järjestelmämonitori yhdellä näkymällä
- **htop**: Reaaliaikainen prosessien ja resurssien näyttö, helppo navigointi
- **fzf**: Interaktiivinen tiedostojen ja komentohistorian haku

Käytetty komento alla. Yksi tai useampi ohjelma ehdotti ylimääräisiä paketteja asennettavaksi. 

<img width="937" height="566" alt="image" src="https://github.com/user-attachments/assets/2829f9f4-3a71-4969-bacf-b447c4cf332f" />


<img width="1283" height="315" alt="image" src="https://github.com/user-attachments/assets/44e7fd4a-4c70-47b3-87bd-961a3ee27039" />

Pitkän asennusrupeaman jälkeen päästiin loppuun:

<img width="1279" height="738" alt="image" src="https://github.com/user-attachments/assets/5df184ce-124c-478f-b0f2-ce880df48e71" />


**Glances**

<img width="1281" height="772" alt="image" src="https://github.com/user-attachments/assets/3d9b9774-ec99-4506-9a82-d3fb00f718ee" />


**Htop**

<img width="1281" height="772" alt="image" src="https://github.com/user-attachments/assets/366b42cb-ba0b-405d-b76f-4a1f1486cb7c" />


**fzf**

<img width="1285" height="773" alt="image" src="https://github.com/user-attachments/assets/bceab762-21cc-41ce-bb87-999be70cf4b9" />


## c) FHS. Esittele kansiot, jotka on listattu "Command Line Basics Revisited" kappaleessa "Important directories". 
Näytä kuvaava esimerkki kunkin tärkeän kansion sisältämästä tiedostosta tai kansiosta. Jos kyseessä on tiedosto, näytä siitä kuvaava esimerkkirivi. 
Työskentele komentokehotteessa ja näytä komennot, joilla etsit esimerkit.

**/ - Juurihakemisto (Root Directory)**
- Tämä on juurihakemisto, koko tiedostojärjestelmän ylin taso.
- Kaikki tiedostot ja hakemistot löytyvät jostain polusta tämän alapuolelta.
- Ei ole Windowsin tyyppisiä asemakirjaimia (C:, D:). 

<img width="824" height="182" alt="image" src="https://github.com/user-attachments/assets/2b5f59ec-84cd-4e6e-8781-194770052355" />

**/home/ - Kotihakemisto (Home Directory)**

- Sisältää kaikkien käyttäjien kotihakemistot.
- Käyttäjät säilyttävät täällä omia tiedostojaan ja asetuksiaan.
- Esim. /home/samuli/ on käyttäjän "samuli" kotihakemisto :)
<img width="839" height="542" alt="image" src="https://github.com/user-attachments/assets/9cbcdc38-25dd-44fb-aa47-2fb84dcff954" />

**/home/samuli - oma kotihakemistoni**

- Kotihakemistoon pääsee komennolla 'cd ~' -> katsoin tämän jälkeen tree-komennolla kotihakemistoni sisällön

<img width="824" height="516" alt="image" src="https://github.com/user-attachments/assets/98aefeaf-de0d-4f49-863c-f880afaa6f69" />

**/etc/ - Järjestelmätiedostot**

- Sisältää järjestelmän kokoonpanotiedostot (configuration files).
- Tiedostot ovat yleensä luettavia tekstitiedostoja, joita voi muokata tekstieditorilla.

<img width="836" height="540" alt="image" src="https://github.com/user-attachments/assets/691e154b-f8cf-4a9d-ae38-6a87aae4189e" />


**/media/ - Irrotettavat mediat**

- Käytetään irrotettaville medioille, kuten CD-levyille, USB-tikuille tai ulkoisille kiintolevyille.

<img width="833" height="161" alt="image" src="https://github.com/user-attachments/assets/36866bdd-dec6-4349-ac94-0f28898fe668" />

**/var/log/ - Järjestelmän lokitiedostot**

- Sisältää järjestelmän lokitiedostot (log files).
- Lokitiedostoista näkee esimerkiksi järjestelmän tapahtumat, virheet ja käyttäjän kirjautumiset.

<img width="836" height="547" alt="image" src="https://github.com/user-attachments/assets/e9e835cb-80c8-46ee-8012-daa25383a347" />


## d) The Friendly M. Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta.

**grep-komennon peruskäyttö**

Komento *'grep "hakusana" tiedosto.txt'* etsii tiedostosta rivit, joissa esiintyy kyseinen hakusana

<img width="837" height="546" alt="image" src="https://github.com/user-attachments/assets/8a0ef6ba-d6af-4aad-ae16-c8269c8ed455" />

**rivinumerot**

Komento *'grep -n "hakusana" tiedosto.txt'* näyttää rivinumerot, joilla hakusana esiintyy

<img width="712" height="87" alt="image" src="https://github.com/user-attachments/assets/80dbfd7b-dfab-4536-ad48-6858ea544322" />

**hakusanan pois sulkeminen hakutuloksista**

Komento *'grep -v "hakusana" tiedosto.txt" näyttää rivit, joilla hakusanaa **ei esiinny**.

<img width="681" height="101" alt="image" src="https://github.com/user-attachments/assets/08f94dab-76f7-44e2-8aa9-d00a5654010a" />


## e) Pipe. Näytä esimerkki putkista (pipes, "|").

Putkittaminen eli |-symbolin käytöllä toisen ohjelman standardituloste ohjataan toisen ohjelman standardisyötteeseen. Putken käyttö grep- ja less-komentojen kanssa on erittäin tärkeää Linuxin komentokehotteen sujuvan käytön kannalta.

**Tiedostojen määrän laskeminen**

Komento *'$ ls /etc | wc -l'* listaa /et-kansion sisälllön ja laskee montako tiedostoa sieltä löytyy.

Komento ja tulos:

<img width="827" height="150" alt="image" src="https://github.com/user-attachments/assets/f9ca348e-f477-4051-a229-db7bbc071fea" />

**Asennettujen pakettien määrän laskeminen**

Komento *'$ dpkg -l | wc -l'* laskee asennettujen pakettien määrän.

Komento ja tulos:

<img width="397" height="73" alt="image" src="https://github.com/user-attachments/assets/960a259f-786f-4c62-b278-b04808a32906" />


## f) Rauta. Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). Asenna lshw tarvittaessa. Selitä ja analysoi listaus.

Ensiyrittämällä komento ei toiminut joten ohjelma piti asentaa:
<img width="832" height="525" alt="image" src="https://github.com/user-attachments/assets/22679640-a9db-4d86-b2c6-d2f36412f8a2" />

<img width="1281" height="766" alt="image" src="https://github.com/user-attachments/assets/1268fef0-feec-4ae5-8db7-40f9ae3da874" />

Virtuaalikone käyttää niitä resursseja, jotka sille on Virtualboxissa annettu.



# Lähteet:
- Karvinen, T. 2020. Command line basics revisited. Luettavissa: https://terokarvinen.com/2020/command-line-basics-revisited/. Luettu: 1.9.2025.
- Linux.fi. Grep. Luettavissa: https://www.linux.fi/wiki/Grep. Luettu: 1.9.2025.
- Linux.fi. Putki. Luettavissa: https://www.linux.fi/wiki/Putki. Luettu: 1.9.2025.
- Quora. How do Install 2 programs simultaneously in Linux? Luettavissa: https://www.quora.com/How-do-I-install-2-programs-simultaneously-in-Linux. Luettu: 1.9.2025.




Seuraavat tehtävät jätän myöhemmäksi... :)
## g) Vapaaehtoinen: Valitse muutama rivi lokeista. Tulkitse ja analysoi.
## h) Vapaaehtoinen: Asenna jokin plugin micro-editorille ja kokeile sitä. Vaikkapa palettero, cheat tai runit.
