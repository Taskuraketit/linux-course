# x) Lue ja tiivistä (Muutama ranskalainen viiva kustakin artikkelista riittää. Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella. The Apache Software Foundation 2023: Apache HTTP Server Version 2.4 Documentation: Name-based Virtual Host Support. Karvinen 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address
- Perinteiseen IP-osoitteisiin pohjautuvaan virtual hostingiin (virtuaalipalvelun) verrattuna nimipohjainen virtuaalipalvelu on yksinkertaisempaa konfiguroida sekä ylläpitää, ja nykyään IP-pohjaista virtual hostingia käytetään lähinnä silloin kun se on teknisistä syistä välttämätöntä.
- Nimipohjaisessa virtual hosteissa taas useat sivustot voivat jakaa saman IP-osoitteen, sillä palvelin tunnistaa sivuston selaimen lähettämän verkkotunnuksen avulla.
  
**Nimipohjaisen virtuaalipalvelun toiminta lyhyesti:**
1. Kun pyyntö saapuu, palvelin etsii sopivimman <VirtualHost>-määrittelyn IP-osoitteen ja portin perusteella.
2. Jos useampi virtual host täsmää, Apache vertaa pyynnön verkkonimeä ServerName- ja ServerAlias-arvoihin.
3. Jos ServerName on jätetty pois, Apache käyttää järjestelmän isäntänimestä johdettua oletusnimeä, mikä voi aiheuttaa odottamattomia tuloksia ja on siksi vältettävää.
4. Jos sopivaa nimeä ei löydy, käytetään ensimmäisenä listattua virtual hostia kyseiselle IP-osoitteen ja portin yhdistelmälle.
   
**Nimipohjaisen virtuaalipalvelun käyttöönotto lyhyesti:**
1. Webserverin (Apache2) asennus ja oletussivun asetus.
2. Uuden nimipohjaisen virtual hostin lisäys.
3. Web-sivun luonti **normaalina käyttäjänä** eli **ei sudolla**.
4. Sivun testaus curl-komennolla.


# a) Testaa, että weppipalvelimesi vastaa localhost-osoitteesta. Asenna Apache-weppipalvelin, jos se ei ole jo asennettuna.

**Apahen asennus**

<img width="1279" height="796" alt="image" src="https://github.com/user-attachments/assets/6d676cf0-fd9c-4aa1-9fbf-79bbe1232c28" />

<img width="1278" height="794" alt="image" src="https://github.com/user-attachments/assets/5e9049dd-cea4-42bd-b7b0-9b358962a4c9" />

**Statuksen tarkistus**

<img width="1286" height="384" alt="image" src="https://github.com/user-attachments/assets/32b2a01f-a759-46ee-ab85-204271829ea1" />

**Testataan käynnistyykö Apache automaattisesti virtuaalikoneen buutin yhteydessä**

<img width="1284" height="74" alt="image" src="https://github.com/user-attachments/assets/07e09840-5bb7-4e61-a802-8d65c15215d2" />
Teksti "Enabled" kertoo, että Apache käynnistyy automaattisesti.


**Kun kirjoitan osoiteriville "localhost", aukeaa seuraavanlainen sivu:**

<img width="1281" height="886" alt="image" src="https://github.com/user-attachments/assets/5c48041a-4505-4ad0-bd39-c41d9b7518a4" />
-> web-palvelin vastaa localhost-osoitteesta.


# b) Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).

**Lokin rivit saa esiin komennolla 'sudo tail -f /var/log/apache2/access.log'**

<img width="1280" height="385" alt="image" src="https://github.com/user-attachments/assets/8d699d0d-bc9d-4a4e-9d50-b42bbbbc8c3c" />

Tarkastellaan viimeisintä riviä '127.0.0.1 - - [08/Sep/2025:22:10:40 +0300] "GET / HTTP/1.1" 304 248 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"'

- **127.0.0.1**: Tämä on asiakkaan IP-osoite. 127.0.0.1 tarkoittaa localhost → pyyntö tuli samalta koneelta, jossa palvelin pyörii.
- **- -** Ensimmäinen - olisi identd-käyttäjänimi (vanha käytäntö, lähes aina tyhjä). Toinen - olisi HTTP-autentikoinnin käyttäjätunnus, jos sellainen olisi käytössä. Tässä ei ollut.
- **[08/Sep/2025:22:10:40 +0300]**: Päivämäärä ja kellonaika: 8. syyskuuta 2025 klo 22:10:40. +0300 = aikavyöhyke-ero GMT:stä → Suomen kesäaika (UTC+3).
- **"GET / HTTP/1.1"**: Tämä on itse HTTP-pyyntö, GET = HTTP-metodi (halutaan hakea resurssi). / = palvelimen juuripolku → käytännössä etusivu. HTTP/1.1 = käytetty protokollaversio.
- **304**: HTTP-palvelimen statuskoodi. 304 Not Modified tarkoittaa, että selain pyysi resurssia, mutta palvelin ilmoitti, että välimuistissa oleva kopio on edelleen ajantasainen → mitään sisältöä ei tarvitse lähettää uudelleen. Tämä on syy, miksi rivissä näkyy 304 eikä 200.
- **248**: Tämä on vastauksen koko tavuina. Vaikka sisältöä ei lähetetty (koska 304), otsakkeet vievät silti hieman tilaa → siksi täällä näkyy 248 tavua.
- **"-"**: Tämä on Referrer-kenttä, eli mistä käyttäjä tuli. "-" tarkoittaa, että pyyntöä ei tehty minkään muun sivun kautta (esim. osoite kirjoitettu suoraan selaimeen tai klikattu kirjanmerkkiä).
- **"Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"**: Tämä on User-Agent, eli tiedot selaimesta. X11; Linux x86_64 → käytössä on 64-bittinen Linux. Firefox/128.0 → selain on Mozilla Firefox, versio 128. 
Gecko/20100101 → Gecko-renderöintimoottori.

# c) Etusivu uusiksi. Tee uusi name based virtual host. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).

**Käytetään viime luennolla luotua kotihakemistoa ja index.html-tiedostoa**

<img width="542" height="647" alt="image" src="https://github.com/user-attachments/assets/c65a056a-a3d4-4339-b1e5-9815f8f482d3" />

**Lisätään yksinkertainen etusivu**

<img width="728" height="305" alt="image" src="https://github.com/user-attachments/assets/25b026da-3b53-48bf-9c53-e104496b0e79" />

**Luodaan uusi Virtual Host -asetustiedosto**

<img width="866" height="87" alt="image" src="https://github.com/user-attachments/assets/ade4160d-d412-4a53-b32f-ea7dd78728e8" />

<img width="816" height="358" alt="image" src="https://github.com/user-attachments/assets/4384a6d9-022d-4533-bc8a-387637fc9ad4" />

**Poistetaan vanha oletussivu käytöstä**

<img width="914" height="209" alt="image" src="https://github.com/user-attachments/assets/9694c7a7-9d21-4fce-89ee-fa4f52fa9d2d" />

**Otetaan uusi oletussivu käyttöön ja käynnistetään Apache uudestaan**

<img width="914" height="337" alt="image" src="https://github.com/user-attachments/assets/37cb2081-e79b-443a-93f7-277138f42289" />

**Jotain meni pieleen, koska oletussivuna näkyy luennolla luomani sivu...**

<img width="562" height="160" alt="image" src="https://github.com/user-attachments/assets/2cd8e8b7-8b68-40bc-9733-9318576b590b" />

**Tarkistetaan hattu.example.com.conf-tiedoston sisältö**

<img width="774" height="303" alt="image" src="https://github.com/user-attachments/assets/4afab254-5d06-4244-a437-bd628c201b26" />

**Poistetaan vanha tiedosto käytöstä ja otetaan uusi käyttöön**

<img width="940" height="308" alt="image" src="https://github.com/user-attachments/assets/d0b89de6-dc76-46ac-84db-ebec1384f865" />

**...edelleen sama lopputulos..**

<img width="612" height="168" alt="image" src="https://github.com/user-attachments/assets/7cf1ef1a-4382-4164-ad4a-c4c3fe738f24" />

**Kävin ohjetta uudelleen läpi ja huomasin, että oletussivun sisältävä tiedosto löytyy täältä:**

<img width="537" height="202" alt="image" src="https://github.com/user-attachments/assets/3da3af5d-f86c-4b79-a191-ad5e5e42314b" />

**Kopioidaan aiemmin luomani tiedosto uuteen sijaintiin**

<img width="680" height="177" alt="image" src="https://github.com/user-attachments/assets/602ef331-92d5-4488-9618-b316c534a3ae" />

**Samojen komentojen syöttö uudelleen...**

<img width="739" height="144" alt="image" src="https://github.com/user-attachments/assets/c459af23-4891-436f-bad0-a8277ed30288" />

**Tarkistetaan hosts-tiedoston sisältö**

<img width="613" height="63" alt="image" src="https://github.com/user-attachments/assets/e00e69f4-7bf1-4b90-88f2-a231a523c241" />

**Päivitetään sisältö (tekstitiedostossa oli luennolla syötetyt tiedot site1.com-sivusta)**

<img width="775" height="129" alt="image" src="https://github.com/user-attachments/assets/633fe832-9640-446a-9d4d-45b2878c4c02" />

**Apachen uudelleenkäynnistys**

<img width="578" height="63" alt="image" src="https://github.com/user-attachments/assets/7ecc7f0b-e572-42a8-8467-ae1789d9f951" />

**Nyt päästiin jo siihen asti, että sivu näkyy oikein kun syöttää osoitteen 127.0.0.1 osoiteriville, mutta pelkällä localhost-osoitteella ei löydy..**

<img width="715" height="242" alt="image" src="https://github.com/user-attachments/assets/7da8ba4f-9137-42cb-b58f-d041c2beb750" />


<img width="552" height="158" alt="image" src="https://github.com/user-attachments/assets/03714fee-d8a8-485a-9e97-9e537f138206" />

**Tässä vaiheessa keksin kokeilla tyhjentää virutaalikoneen selaimen sivuhistorian, evästeet ym... ja se alkoi kuin alkoikin toimia halutulla tavalla :D**

<img width="700" height="242" alt="image" src="https://github.com/user-attachments/assets/5ccac6c5-d0df-4e7b-8b9a-8eb0b1442579" />

<img width="670" height="232" alt="image" src="https://github.com/user-attachments/assets/6806612a-59c2-4943-bf70-2060bd39c0e7" />

Ja näin päästiin vaikeuksien kautta voittoon - *per aspera ad astra*


# e) Tee validi HTML5 sivu.

**Lähdetään liikkeelle varmuuskopion ottamisesta. Muokataan edellisessä tehtävässä luotua hattusivua.**

<img width="691" height="296" alt="image" src="https://github.com/user-attachments/assets/f288f300-2ea6-4d7b-b937-b64065a52399" />


<img width="840" height="328" alt="image" src="https://github.com/user-attachments/assets/29b97732-69b3-4754-8113-a9ee06f72fd2" />


**Poistetaan vanha oletussivu**

<img width="654" height="38" alt="image" src="https://github.com/user-attachments/assets/584b5113-3ad8-49c6-86e2-6d50da421d64" />

Sivu oli jo disabbloitu.

**Uuden virtual hostin käyttöönotto**

<img width="698" height="41" alt="image" src="https://github.com/user-attachments/assets/e41ece6e-3119-454c-bb84-5bc4902ec110" />

Sivu oli jo enabloitu.

**Web-palvelimen avaus uudelleen**

<img width="631" height="45" alt="image" src="https://github.com/user-attachments/assets/1725618e-9f4b-4fd2-8012-cca4faaa2a88" />

Koska selain näytti localhostissa aiemmin luodun oletussivun, tarvittiin vähän kikkailua...

**Tiedoston kopiointi ja Apachen uudelleenkäynnistys**

<img width="836" height="787" alt="image" src="https://github.com/user-attachments/assets/e372a506-a201-4e34-9b17-f28b54d492d7" />

**Poistettuani jälleen selaimesta sivuhistorian ja evästeet uusi oletussivu alkoi toimia. Jee!**

<img width="572" height="252" alt="image" src="https://github.com/user-attachments/assets/55185161-8b15-4243-8c35-0dbf45754eee" />


<img width="556" height="246" alt="image" src="https://github.com/user-attachments/assets/2fecc297-e7e7-4124-bc8b-07d0ba916e8d" />


# f) Anna esimerkit 'curl -I' ja 'curl' -komennoista. Selitä 'curl -I' muutamasta näyttämästä otsakkeesta (response header), mitä ne tarkoittavat.

curl ja curl -I käytetään verkkopyyntöjen testaamiseen ja tiedon hakemiseen palvelimelta.
- curl → hakee koko sivun sisällön (HTML, JSON tms.), jolloin näkee sivun todellisen datan.
- curl -I → hakee vain HTTP-otsakkeet (response headers), jolloin näkee palvelimen tilan, vastauskoodin, sisällön tyypin ja muut metatiedot ilman varsinaista sisältöä.

Näillä komennoilla voi nopeasti tarkistaa, toimiiko palvelin, mikä statuskoodi tulee ja millaisia otsakkeita se lähettää, ilman selainta.

<img width="802" height="567" alt="image" src="https://github.com/user-attachments/assets/267f55c6-6d82-48fb-9ea2-eed152bb74c7" />


# m) Vapaaehtoinen, suosittelen tekemään: Hanki GitHub Education -paketti.


# o) Vapaaehtoinen, vaikea: Laita sama tietokone vastaamaan kahdellla eri sivulla kahdesta eri nimestä. Eli kaksi weppisiteä samalla koneelle, esim. foo.example.com ja bar.example.com. Voit simuloida nimipalvelun toimintaa hosts-tiedoston avulla.


# Lähteet

- **Karvinen, T.** s.a. Linux Palvelimet alkusyksy 2025. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu: 8.9.2025.
- **The Apache Software Foundation 2023**. Apache HTTP Server Version 2.4 Documentation: Name-based Virtual Host Support. Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html. Luettu: 8.9.2025.
- **Karvinen, T.** 2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. Luettavissa: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/. Luettu: 8.9.2025.

Lisäksi käytetty ChatGPT:tä ongelmanselvityksen tukena sekä selittämään eri komentojen sisältöjä.
