# x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella). 
## Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4) (opiskelijan esimerkkiraportti), kohdat

### a) Pilvipalvelimen vuokraus ja asennus

- Kuvauksessaan palvelimen vuokrauksesta ja asennuksesta Susanna kertoo hankkineensa palvelimen DigitalOceanilta ja domainnimen Namecheapilta
- Palvelimen vuokra DigitalOceanilta eteni raportin mukaan loogisesti valitsemalla halutut speksit (mm. Sijainti -> Amsterdam, joka oli vaihtoehdoista lähimpänä Helsinkiä) ja syöttämällä omat maksutiedot
- Alkutoimien jälkeen virtuaalipalvelin oli valmis ja Susanna sai palvelimensa IP-osoitteen tietoon

-  Domainnimen varaus on käynyt näemmä helposti tarkistamalla palvelusta nimen saatavuus ja valitsemalla itselle sopiva domainnimi
-  Opiskelijana hän sai domainnimen ilmaiseksi (!)
-  Muutaman mutkan kautta Susanna sai lopulta uuden domainnimensä osoittamaan uuden palvelimensa IP-osoitteeseen

### d) Palvelin suojaan palomuurilla

**Palomuurin asennuksen toimenpiteet palvelimen komentorivillä:**

ssh-yhteyden muodostus

> $ ssh root@<ip-osoite>

Ohjelmien päivitys

> $ sudo apt-get update

Palomuurin asennus

> $ sudo apt-get install ufw

Reiän tekeminen palomuuriin

> $ sudo ufw allow 22/tcp

Palomuurin laitto päälle

> $ sudo ufw enable


### e) Kotisivut palvelimelle

Käyttäjän lisäys virtuaalipalvelimelle

> $ sudo adduser <käyttäjä>

Pääkäyttäjän tekeminen käyttäjästä

> $ sudo adduser <käyttäjä> sudo

Virtuaalipalveimen testaus (toisessa terminaalissa)

> $ ssh <käyttäjä>@<ip-osoite>
> $ sudo apt-get update

Juuren lukitseminen

> $ sudo usermod –lock root

Domainnimen pingaaminen testimielessä

> $ ping <domainnimi>

Toisen terminaalin avaaminen uudestaan + SSH-yhteyden muodostaminen pääkäyttäjänä. 
Tietoturvapäivitysten asentaminen

> $ sudo apt-get update
> $ sudo apt-get upgrade
> $ sudo apt-get dist-upgrade

Apache-webbi-palvelimen asennus

> $ sudo apt-get install apache2

Palvelimen tilan tarkastelu

> $ sudo systemctl status apache2

Toisen reiän tekeminen palomuuriin:

> $ sudo ufw allow 80/tcp

...ja tämän jälkeen domainnimen testaus omalla palvelimella selaimessa.

Apachen testisivun korvaaminen komennolla

> $ echo Hello world! |sudo tee /var/www/html/index.html

Userdir-moduulin käyttöönotto ja webbipalvelimen uudelleenkäynnistys

> $ sudo a2enmod userdir
> $ sudo service apache2 restart

### f) Palvelimen ohjelmien päivitys

## Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS

# a) Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. (Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla ilmaiseksi vagrant:ia paikallisesti. Suosittelen kuitenkin harjoittelemaan oikeilla, tuotantoon kelpaavilla julkisilla palveluilla).

# b) Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys.

# c) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. Kokeile myös eri koneelta, esim kännykältä. (Jos haluat tehdä oikeat weppisivut, tarvitset Name Based Virtual Hostin)

# d) Vapaaehtoinen: Laita omalle julkiselle palvelimellesi uusi Name Based Virtual Host. Kun sammutat muut weppisivut, niin se ainut näkyy nimestä riippumatta etusivulla. Name Based Virtual Host avulla pääset muokkaamaan kotisivuja normaalilla käyttäjällä, ilman sudoa.
