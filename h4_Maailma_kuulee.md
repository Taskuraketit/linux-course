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

Käyttäjälle julkisen kansion public_html luonti omaan kotihakemistoon + varmistus, että julkinen kansio näkyi halutussa kansiossa. 

SSH-yhteyden avaus ja micron asennus

> $ sudo systemctl start ssh
> $ sudo apt-get install micro

Kotihakemistoon porautuminen ja tekstitiedoston index.html luonti microlla

> $ cd public_html
> $ micro index.html

Lyhyen nettisivun rungon teko tiedostoon W3Schoolsin ohjeilla, tallennus ja tallennuksen vahvistus terminaalissa salasanalla.
Nettisivujen ulkoasun tarkastelu erillisen Windows-koneen Chrome-selaimella.

### f) Palvelimen ohjelmien päivitys

Palvelimelle kirjautuminen (pää)käyttäjänä.
Päivitykset komennoilla:

> $ sudo apt-get update

> $ sudo apt-get upgrade

> $ sudo apt-get dist-upgrade

## Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS

**Lyhyet ohjeet uuden virtuaalipalvelimen ja verkkotunnuksen käyttöönottoon**

- Käytä aina vahvoja salasanoja – ei poikkeuksia.
- Virtuaalipalvelimet ja verkkotunnukset ovat kilpailtuja palveluita. Artikkelissa käytetty esimerkkinä DigitalOceania ja NameCheapia, koska ne sisältyvät GitHub Education Student Packiin.
- Opiskelijana voi saada GitHubin opiskelijapaketin ilmaiseksi. Se sisältää mm. virtuaalipalvelimen ja .me-verkkotunnuksen rajoitetuksi ajaksi.
- GitHubiin rekisteröidytään yliopiston sähköpostilla + sähköpostin vahvistus

**Virtuaalipalvelimen luominen DigitalOceanissa**

- Luo uusi tili ja lisää maksutiedot tai kampanjakoodi.
- Luo uusi Ubuntu 16.04 LTS -palvelin. (*HUOM! Toteutuksella ICI003AS2A-3014 valittiin Debian, koska kurssilla opeteltu käyttämään sitä*)
- Valitse datakeskus lähellä asiakkaitasi (esim. Euroopassa).
- Voit ladata SSH-julkisen avaimen, jos osaat – muuten saat automaattisesti luodun salasanan.
- Tarkista palvelimen IP-osoite.

# a) Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. (Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla ilmaiseksi vagrant:ia paikallisesti. Suosittelen kuitenkin harjoittelemaan oikeilla, tuotantoon kelpaavilla julkisilla palveluilla).

**Kurssiluennolla vertailtiin muutamaa eri palveluntarjoajaa, joista valitsin opettajan suosituksesta suomalaisen UpCloudin.**

**Loin tunnukset ja kirjauduin UpCloudin sivuille**

<img width="772" height="795" alt="image" src="https://github.com/user-attachments/assets/aef7a13c-c8e3-4cb6-bc3f-9ff60beffb10" />

**Valitsin, että haluan vuokrata serverin**

<img width="407" height="607" alt="image" src="https://github.com/user-attachments/assets/c121b52d-c79c-4876-b44f-3d03a0c61306" />

**Sijainniksi valitsin Helsingin**

<img width="826" height="760" alt="image" src="https://github.com/user-attachments/assets/4704f59f-4c51-42b4-883d-7775b8f2547e" />

**Otin halvimman mahdollisen vaihtoehdon (1 core / 1 GB muistia / 10 GM levytilaa / hinta 3,00 euroa kuukaudessa)**

<img width="857" height="698" alt="image" src="https://github.com/user-attachments/assets/c38c0690-46d9-4c56-b44a-65a7273926e0" />

**Käyttöjärjestelmäksi valitsin Debian GNU/Linux 13 (Trixie)**

<img width="804" height="681" alt="image" src="https://github.com/user-attachments/assets/b8a3774d-72c0-426c-bcb9-dd7e4f724122" />

**Nämä vaihtoehdot Network-osion alla olivat oletuksena päällä. Valitsin kaikki, koska niistä ei tullut lisämaksua.**

<img width="826" height="513" alt="image" src="https://github.com/user-attachments/assets/58b02a7c-e791-43b3-951b-4354f4c59528" />

**Tämän jätin tyhjäksi**

<img width="827" height="351" alt="image" src="https://github.com/user-attachments/assets/4d27b987-183f-45b9-bbda-2d18a05dfa5c" />

**Loin SSH-avaimen ja lisäsin SSH-avaimen tänne**

<img width="836" height="386" alt="image" src="https://github.com/user-attachments/assets/e5cad837-7977-4208-b31e-ef6f0b99fb8c" />

**Palvelin pystyssä - nimettynä luonnollisesti koirani mukaan :)**

<img width="848" height="687" alt="image" src="https://github.com/user-attachments/assets/fae9458c-3988-4963-af47-bbd90b402328" />

# b) Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys.

**SSH-yhteyden muodostaminen palvelimelle**

<img width="948" height="751" alt="image" src="https://github.com/user-attachments/assets/71516740-1c12-48b3-a528-9965f8c8a6c0" />

**Asennuspakettien päivitys**

<img width="1154" height="791" alt="image" src="https://github.com/user-attachments/assets/c020def7-0c11-4702-a423-56a2a2da4e8d" />

**Config-tiedoston muokkaus**

<img width="1224" height="729" alt="image" src="https://github.com/user-attachments/assets/93d67fc2-dda8-4113-8413-a5e40ffce877" />

**Oletuksena oli "no" -> vaihdoin "yes"**

<img width="863" height="793" alt="image" src="https://github.com/user-attachments/assets/7194a115-1975-4cef-8c42-e35932ce1511" />

**SSH-palvelun uudelleenkäynnistys**

<img width="706" height="97" alt="image" src="https://github.com/user-attachments/assets/e67b8266-b903-47ad-9e2e-f1328c1b7e9f" />

<img width="943" height="320" alt="image" src="https://github.com/user-attachments/assets/c2a9245c-9315-49a1-a6bb-d6fd8648b588" />

**Avasin terminaalin uudelleen ja testasin kirjautumista samuli-tunnuksella. Samalla testasin groups-komentoa, joka kertoi minun olevan sudo-käyttäjä.**

<img width="828" height="547" alt="image" src="https://github.com/user-attachments/assets/4d1891b6-0c93-498f-b1d9-7b3e82e1759d" />

**Ohjelmien päivitys ja rootin lukitseminen:**

<img width="624" height="134" alt="image" src="https://github.com/user-attachments/assets/27046fa2-ca82-4d7f-8c65-6d33f190b8b5" />

**Tarkistin, että root on lukittu ulos:**

<img width="396" height="84" alt="image" src="https://github.com/user-attachments/assets/5f45390f-5dc9-466a-b8c1-b4c473f00841" />

**Muokkasin sshd_config-tiedostoon kohdan PermitRootLogin asetuksen "yes" -> "no" + tallennus**

<img width="830" height="552" alt="image" src="https://github.com/user-attachments/assets/4fb4b208-0890-42f4-957f-870f4b66dea3" />

**Tulimuurin asennus. Valitsin "y" ja asennus ruksutti läpi.**

<img width="837" height="346" alt="image" src="https://github.com/user-attachments/assets/23af4197-e34f-4a98-9a07-ad46a2dae188" />

<img width="835" height="549" alt="image" src="https://github.com/user-attachments/assets/5cbd6740-ce29-43c9-9b4b-4a021dde8cdb" />

**Automaattisten tietoturvapäivitysten asentaminen**

<img width="834" height="552" alt="image" src="https://github.com/user-attachments/assets/482bc258-1174-4c8b-b79d-3ba1614582fd" />

**Automaattisen täydennyksen lisäys bash-komentoriville**

<img width="823" height="347" alt="image" src="https://github.com/user-attachments/assets/d3093757-c37e-4383-a610-c8a7cb3a2414" />


# c) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. Kokeile myös eri koneelta, esim kännykältä. (Jos haluat tehdä oikeat weppisivut, tarvitset Name Based Virtual Hostin)

# d) Vapaaehtoinen: Laita omalle julkiselle palvelimellesi uusi Name Based Virtual Host. Kun sammutat muut weppisivut, niin se ainut näkyy nimestä riippumatta etusivulla. Name Based Virtual Host avulla pääset muokkaamaan kotisivuja normaalilla käyttäjällä, ilman sudoa.
