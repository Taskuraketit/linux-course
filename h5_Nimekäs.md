# Lue itse: tämän kerran lukuläksy on etsiä itse laadukkaat lähteet kaikkiin vieraisiin käsitteisiin ja työkaluihin. Vastaukset tulevat osaksi analyysiä ja tulkintaa, erillisiä tiivistelmiä ei tällä kertaa tehdä.

# a) Nimi. Laita julkinen nimi osoittamaan omaan koneeseesi. (Siis vastaava kuin terokarvinen.com. Nimen saattaa saada myös ilmaiseksi Github Education -paketilla. Suosittelen hankkimaan oikean nimen, mutta jos välttämättä haluat, voit myös simuloida nimen toimintaa paikallisesti hosts-tiedoston avulla.)

Tätä tehtävää varten päätin hankkia oman domainnimen NameCheapilta. Aluksi menin osoitteeseen www.namecheap.com ja loin itselleni tunnukset palveluun. Tämän jälkeen hain hakutyökalulla minkälaisia domainnimiä olisi tarjolla. Ensisijaisesti haluamani domain toropainen.com on varattu joten päätin ottaa opettajan suositteleman etunimisukunii.com-osoitteen.


<img width="1322" height="707" alt="image" src="https://github.com/user-attachments/assets/e7b0d84f-bdfc-43ca-895c-13cc660d38d1" />


Vertailun vuoksi: eri päätteillä hintaerot ovat todella suuria, tässä muutaia esimerkkejä:


<img width="1325" height="665" alt="image" src="https://github.com/user-attachments/assets/771c8985-9655-427c-95f6-1efc7769732b" />


Etenin seuraavilla valinnoilla ilman mitään ylimääräisiä härpäkkeitä: 


<img width="1293" height="856" alt="image" src="https://github.com/user-attachments/assets/a17f9d88-9268-404d-8a98-79758ad7950a" />


Seuraavalla sivulla syötin yhteystietoni:


<img width="1252" height="570" alt="image" src="https://github.com/user-attachments/assets/eb0a8d1a-9d06-4ed8-9f15-8c243ec460ef" />


Seuraavalla sivulla valitsin, että olen itse sivuston hallinnollinen, tekninen ja laskutukseen liittyvä yhteyshenkilö.


<img width="1275" height="373" alt="image" src="https://github.com/user-attachments/assets/5bdf5496-0be3-43b0-b169-e2caee95ed73" />


Sivun alalaidassa valitsin seuraavasti: 


<img width="1266" height="661" alt="image" src="https://github.com/user-attachments/assets/c673f2b8-4d6b-485f-a7d5-350e7080ba80" />


Seuraavalle sivulle syötin maksukortin tiedot ja valitsin, että domainnimeä **ei uusita** automaattisesti. Valintani perustuu siihen, että halusin ostaa domainnimen lähinnä oppimismielessä enkä todellisuudessa tiedä mitä tulen Linux-palvelimella tai domainnimellä tekemään.


<img width="1261" height="512" alt="image" src="https://github.com/user-attachments/assets/6686a389-69b9-4649-a72b-e2a52a1fd69d" />


Kas näin, maksu suoritettu!


<img width="1356" height="666" alt="image" src="https://github.com/user-attachments/assets/95aaf58d-e5f3-424d-a2ed-182aaea77bf5" />


Seuraavaksi menin Domain list -sivulle ja valitsin "Advanced DNS". Poistin oletusrivit ja lisäsin kaksi uutta A-tietuetta (A Record) ja laitoin molemmmat osoittamaan virtuaalipalvelimeeni. TTL:ksi valitsin 5 minuuttia. Lopuksi tallensin muutokset.


<img width="1414" height="767" alt="image" src="https://github.com/user-attachments/assets/b9736dac-98e7-48e2-8411-744d5f27812e" />


Tämän tehtyäni kirjauduin terminaalin kautta virtuaalipalvelimelleni ja yllätyksekseni ikkunaan tuli ilmoitus fingerprintistä. Valitsin "yes" ja syötin salasanani


<img width="953" height="308" alt="image" src="https://github.com/user-attachments/assets/ee469b54-84e9-4091-9359-9560df2c7750" />


Seuraavaksi kokeilin pingata domainnimeäni

> ping samulitoropainen.com


<img width="799" height="387" alt="image" src="https://github.com/user-attachments/assets/ec917b33-a797-403a-acb1-e05fec572036" />


...ja huomasin, että se pingaa takaisin (jes!), mutta ilmoittaa osoitteeksi murukoira.com, jonka olin aiemmassa vaiheessa laittanut config-fileen. Pysäytin ping-komennon painamalla ctrl + C.


Menin muokkaamaan /etc/apache2/sites-available-kansiossa olevaa conf-tiedostoa. Aloitin ottamalla siitä varmuuskopion (jossa onnistuin muutaman typottamisen jälkeen)

> sudo cp murukoira.com.conf murukoira.com.conf.orig


Nimesin tiedoston uudelleen

> sudo mv murukoira.com.conf samulitoropainen.com.conf


<img width="1018" height="246" alt="image" src="https://github.com/user-attachments/assets/8c4ac64e-7a1d-40c6-9e72-7f8d5c164b16" />


Muokkasin config-tiedostoon kohdat ServerName, ServerAlias sekä lokitiedostojen nimet.


<img width="1286" height="805" alt="image" src="https://github.com/user-attachments/assets/550237d9-7be8-4dac-b5c5-a792a45284b7" />


Tämän jälkeen pingaamalla terminaalissa 'samulitoropainen.com' tuli edelleen näkyviin aiemmin laittamani osoite murukoira.com. Tilanne ei muuttunut käynnistämällä webbipalvelin uudelleen.

> ping samulitoropainen.com

> sudo systemctl reload apache2

> ping samulitoropainen.com


<img width="812" height="506" alt="image" src="https://github.com/user-attachments/assets/a8d72556-dba6-4e68-8256-d2fcf4847a8b" />


Microsoft Copilotin avulla onnistuin paikantamaan, että tieto tulee **/etc/hosts-tiedostosta** joten avasin sen

> micro /etc/hosts


<img width="729" height="143" alt="image" src="https://github.com/user-attachments/assets/674ea5d2-f466-47d2-94b3-c4f3c4ff5106" />



...ja muokkasin tiedostoon oikeat tiedot (eli murukoira.comin tilalle samulitoropainen.com).


<img width="739" height="165" alt="image" src="https://github.com/user-attachments/assets/f223b907-8107-4c94-938c-86add8f07591" />


Tämän jälkeen pingaamisessakin alkoi näkyä oikea osoite :)


<img width="864" height="233" alt="image" src="https://github.com/user-attachments/assets/b8845a72-3c22-42e1-9d06-df1ad807e3ab" />


Seuraavaksi halusin muokata nettisivua hieman tarkoituksenmukaisemmaksi. Navigoin /var/www/html-kansioon ja otin varmuuskopion aiemmasta tiedostosta ja muokkasin index.html-tiedostoa.


<img width="748" height="265" alt="image" src="https://github.com/user-attachments/assets/71d08666-9a9c-45c0-8f6d-813e115ffa10" />


<img width="1251" height="696" alt="image" src="https://github.com/user-attachments/assets/59a0a946-5bc8-4c0b-9165-24203e02b7e3" />


Lopputulos:


<img width="1295" height="491" alt="image" src="https://github.com/user-attachments/assets/ceead934-ce8b-4b5c-a59d-b1f6ad206902" />



Hetken selvittelyn jälkeen hoksasin, että conf-tiedostossani on väärä kansiopolku. Luomani index.html sijaitsee sijainnissa /var/www/html, joten päivitin tämän tiedostoon.


Lähtötilanne:


<img width="786" height="385" alt="image" src="https://github.com/user-attachments/assets/2ea6f150-9d26-4226-a696-a5783404faca" />


Muokkauksen jälkeen:


<img width="779" height="394" alt="image" src="https://github.com/user-attachments/assets/8972af94-a302-4c2d-8ad5-48c2ae57a00b" />


Tämän jälkeen käynnistin Apachen uudelleen

> sudo systemctl reload apache2


<img width="787" height="111" alt="image" src="https://github.com/user-attachments/assets/f7892c2e-25b7-4825-80fc-d738ebe78bc0" />



Kaiken tämän jälkeen osoite samulitoropainen.com vie edelleen vanhalle sivulle.


<img width="988" height="429" alt="image" src="https://github.com/user-attachments/assets/1f4964a7-08f0-4535-8e54-c17dc30e46d6" />



Kokeillaanpa kommentoida hosts-tiedostosta rivit pois josko se sotkisi nimipalvelua... eli risuaidat rivien alkuun:


<img width="785" height="181" alt="image" src="https://github.com/user-attachments/assets/91b3e36b-0017-49d3-b181-c78cc4b0e461" />


Curlilla testatessa alkaa jo näyttää oikealta:

> curl http://samulitoropainen.com


<img width="1295" height="699" alt="image" src="https://github.com/user-attachments/assets/71676b65-24cf-4fa8-ae73-b87e2f214b63" />


Tässä kohtaa vilkaisin lokitiedostoja ja löysinkin jotain yllättävää - joku (kenties botti) on pommittanut serveriäni ja saanut useita virheilmoituksia. Siispä Copilotin ohjeen mukaan estin kyseisen IP-osoitteen komennolla

> sudo iptables -A INPUT -s 45.88.186.32 -j DROP

<img width="1280" height="667" alt="image" src="https://github.com/user-attachments/assets/fb812d34-4f5d-488b-bc61-56570deb5340" />


Seuraavaksi tarkistin whatismyipaddress.com-palvelussa kyseisen IP-osoitteen sijainnin ja se paikallistui Saksaan:


<img width="1513" height="834" alt="image" src="https://github.com/user-attachments/assets/a2f5f783-5cef-4b05-91e2-35dedab4d441" />


Tämän jälkeen jatkoin selvitystä Copilotin avustuksella seuraavasti:


Tarkistin fail2banin (ohjelman, joka suojaa palvelinta bruteforce- ja bot-hyökkäyksiltä)


> $ sudo systemctl status fail2ban


Tarkistin aktiiviset jailit eli säännöt


> $ sudo fail2ban-client status


Loin fail2ban-konfiguraatiotiedoston


> $ sudo micro /etc/fail2ban/jail.local


Syötin konfiguraatiotiedostoon seuraavat tiedot:



*[apache]*
*enabled = true*
*port    = http,https*
*filter  = apache-auth*
*logpath = /var/log/apache2/access.log*
*maxretry = 5*
*bantime = 3600*

Tallensin tiedoston ja suljin sen.


Tarkistin, että jail on aktiivinen 


> $ sudo fail2ban-client status apache


Asetin aiemmalle hyökkääjä-IP:lle estot


> $ sudo fail2ban-client set apache banip 45.88.186.32



Tarkistin aktiiviset prosessit:


> $ ps aux



Tarkistin mahdolliset uudet käyttäjät



> $ cat /etc/passwd



Tarkistin verkkoyhteydet



> $ netstat -tulnp



Tarkistin onko index.html- tai muita tiedostoja muokattu



> $ ls -l /var/www/html



Asensin ja ajoin rkhunter-ohjelman Rootkit-ohjelmien varalta:



> $ sudo apt-get install rkhunter chkrootkit
> $ sudo rkhunter --check
> $ sudo chkrootkit


Rkhunterin tulokset olivat muuten puhtaat, mutta ohjelma varoitti seuraavasta:


<img width="550" height="52" alt="image" src="https://github.com/user-attachments/assets/c0d4a68f-3b93-4be1-9844-f296e98744ed" />



Copilotin tulkinta: 


<img width="634" height="266" alt="image" src="https://github.com/user-attachments/assets/b278898e-c64d-42f3-8478-6c059aeaaa60" />



Tarkistin /dev-hakemiston:


> $ ls -l /dev | grep -v '^c\|^b'



Tarkistin piilotetut tiedostot:


> $ sudo find / -name ".*" -type f 2>/dev/null



Mitään epäilyttävää ei löytynyt joten tulkitsin tämän **false positive -tilanteeksi**.



Tässä kohtaa menin uudelleen katsomaan samulitoropainen.com-sivua ja yllätyksekseni se oli päivittyyt oikeanlaiseksi eli TTL oli ilmeisesti jostain syystä pidempi kuin NameCheap.com-sivulle asettamani 5 minuuttia.



<img width="1281" height="885" alt="image" src="https://github.com/user-attachments/assets/842b211f-ca7b-4e4d-8e24-d632a7397b73" />



Ja näin sivu skaalautuu mobiililaitteella (iPhone 12):


<img width="398" height="861" alt="image" src="https://github.com/user-attachments/assets/83852252-6e34-4583-9b95-62547a1defbb" />




# b) Based. Laita Name Based Virtual Host näkymään uudessa nimessäsi. Kotisvuja pitää pystyä muokkaamaan ilman pääkäyttäjän oikeuksia.


Tämä tuli  tehtyä jouhevasti a-kohdan yhteydessä.


# c) Kotisivu. Tee vähintään kolmen erillisen alasivun (esim. index.html, blog.html, projects.html) kotisivu ja kopioi se näkymään palvelimellesi. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.


Aloitin luomalla uudet html-tiedostot samaan kansioon (/var/wwww/html) kuin missä index.html-tiedosto sijaitsee. Oikaisin hieman ja kopioin index.html:n, nimesin sen uudelleen ja muokkasin sisältöä.


> $ sudo cp index.html blog.html


> $ sudo micro blog.html


<img width="1264" height="746" alt="image" src="https://github.com/user-attachments/assets/cb53f41e-7014-46f6-9622-499b854fbf28" />



Otin varmuuden vuoksi varmuuskopion nykyisestä index.html-tiedostosta ja muokkasin työstettävään tiedostoon vastaavan navigaatiopalkin (joka toivottavasti toimii kuten pitäisi...)


> $ sudo cp index.html index.html.backup

> $ sudo micro index.html

<img width="678" height="137" alt="image" src="https://github.com/user-attachments/assets/2c3bc4c7-ff54-4136-852c-8b2c1102765f" />


<img width="1279" height="768" alt="image" src="https://github.com/user-attachments/assets/f094307c-64ee-4505-a394-64c1dcaa3ac1" />


Oikaistakseni hieman poistin aiemmin luomani projects.html-tiedoston, otin kopion blog.html:stä, nimesin sen uudelleen projects.html:ksi ja muokkasin sisältöä.


> $ sudo rm projets.html

> $ sudo cp blog.html projects.html

<img width="763" height="315" alt="image" src="https://github.com/user-attachments/assets/be6f86aa-0dd6-4566-9f03-e3196f0b11a5" />


<img width="1276" height="740" alt="image" src="https://github.com/user-attachments/assets/426e3e9a-478f-4832-b704-cae316af79ea" />


Tässä kohtaa sivuni toimivat teknisesti kuten pitää, mutta värikontrastin vuoksi muokkasin tiedostoja siten, että navigaatiopalkki näkyy samalla tavalla kuten pääsivulla:


Lähtötilanne:

<img width="1276" height="740" alt="image" src="https://github.com/user-attachments/assets/96de2bb1-832d-42b6-b385-e602c503c97a" />


<img width="1288" height="480" alt="image" src="https://github.com/user-attachments/assets/5f142f5c-5f26-4a20-8b4a-d74778a591ef" />


Ratkaisu: </header>-osion siirto varsinaisen header-osion alle ennen navigaattoria


<img width="1009" height="432" alt="image" src="https://github.com/user-attachments/assets/9ab2701a-9c84-459e-8f04-1475d51443f1" />


Nyt navigaattori näkyy oikein jokaisella kolmella sivulla :) Käytännössä jos olisin tekemässä vakavissani nettisivuja, tekisin header-osioon erilliset painikkeet yhteensopivalla värimaailmalla, mutta tässä tapauksessa tyydyn siihen, että sivut toimivat teknisesti siten mmiten kuuluukin.


<img width="1281" height="466" alt="image" src="https://github.com/user-attachments/assets/36114cca-bac8-48a4-a432-836686720351" />




# d) Alidomain. Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com). Tässä tehtävässä riittää, että alidomainit avaavat saman sivun kuin päädomain. (Vapaaehtoinen bonus: Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Vapaaehtoinen bonus: tee alidomainiin oma erillinen name based virtual host.)


Lisäsin Namecheap.comissa A Recordin, jolle laitoin Hostiksi 'vadelma', IP-osoitteeksi palvelimen IP-osoitteen ja TTL:ksi 5 minuuttia. Lisäsin myös CNAME Recordin, jolle laitoin Hostiksi 'mansikka' ja Value-kohtaan domainnimen 'samulitoropainen.com' ja TTL:ksi 5 minuuttia.


<img width="1130" height="326" alt="image" src="https://github.com/user-attachments/assets/9d331bac-bc08-43a4-9030-4a27cf4d1af3" />


Molemmat alidomainit alkoivat heti toimia (ks. selaimen osoiterivi):



<img width="1282" height="473" alt="image" src="https://github.com/user-attachments/assets/eb691e92-8efa-4d20-8d8f-6022ed762786" />


 
<img width="1285" height="477" alt="image" src="https://github.com/user-attachments/assets/05fc2404-a20e-49ac-9b86-05f551871b05" />
 


# e) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset, keskity nimipalvelimelta tulleisiin kenttiin (dig näyttää paljon muutakin tietoa). Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:

## Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.

Syötin komentiriville komennot 'host samulitoropainen.com' ja 'dig samulitoropainen.com', mutta sain ilmoituksen "command not dound". Siispä asensin dnsutils-paketin, joka sisältää sekä dig- että host-komennot (tämän vinkin sain Copilotilta).

> $ sudo apt-get update
>
> $ sudo apt-get install -y dnsutils

<img width="1290" height="802" alt="image" src="https://github.com/user-attachments/assets/329b2f5c-5dff-4265-8e59-b06482f867b1" />


Syötin uudelleen komennot

> $ host samulitoropainen.com
>
> $ dig samulitoropainen.com

...ja sain seuraavat tulokset:


<img width="1285" height="639" alt="image" src="https://github.com/user-attachments/assets/a55e8d41-b1e4-4c35-92ff-4bd15e085d97" />


## Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).


Syötin komentoriville komennot

> $ host terokarvinen.com
>
> $ dig terokarvinen.com


...ja sain seuraavat tulokset:


<img width="718" height="562" alt="image" src="https://github.com/user-attachments/assets/7b273177-153b-481b-b4be-241f4d184276" />


## Jonkin suuren ja kaikkien tunteman palvelun tiedot.


Syötin komentoriville komennot

> $ host microsoft.com
>
> $ dig microsoft.om


...ja sain seuraavat tulokset:


<img width="1286" height="657" alt="image" src="https://github.com/user-attachments/assets/5991b6ef-6e0f-4f9a-bdcc-547d34d4c0dd" />



**Tulosten vertailua**

- Kaikkien kolmen domainin kyselyt onnistuivat (status-kohdassa luki 'NOERROR')
- flags-kohdassa kaikilla kolmella sivulla oli tuloksena 'qr rd ra', jotka tarkoittavat
 - qr = query response (kyselyn vastaus)
 - rd = recursion desired (kysely pyysi rekursiota)
 - ra = recursion available (palvelin tarjosi rekursion)
- 'udp: 65494' kertoo, että palvelin tukee 65494 tavun kokoisia UDP-paketteja DNS-vastauksissa
- QUESTION SECTION -osio kertoo mitä kysyttiin
 - ensimmäisenä domainnimi
 - 'IN' = internet-luokka
 - 'A' = A-tietue eli IPv4-osoite
- ANSWER SECTION -osio kertoo vastauksen
 - ensimmäisenä domainnimi
 - numeroarvo kertoo TTL:n (Time To Live) = aika skunteina kauanko tieto on välimuistissa
 - 'IN' = internet-luokka
 - 'A' = IPv4-osoite
 - xxx.xxx.xxx.xxx = domainin IP-osoite
- query time = kyselyyn kulunut aika millisekunteina
- 'SERVER: 127.0.0.53#53(127.0.0.53) (UDP)' -> DNS-kysely tehtiin paikalliselle resolverille
- 'WHEN' = kyselyn ajankohta
- MSG SIZE rcvd = vastauksen koko tavuina

# f) Vapaaehtoinen bonus: Aakkossalaattia sähköpostiin. Etsi palvelu, jonka DNS-tiedoissa on SPF ja DMARC. Selitä näiden kenttien osat ja vaikutukset yksityiskohtaisesti. Voit halutessasi käyttää tulkinnan apuna jotain ohjelmaa tai palvelua, kunhan selität ja tulkitset lopputuloksen myös itse.
 

# Lähteet:

- **Karvinen, T.** Linux Palvelimet 2025 alkusyksy. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu: 18.9.2025.
- **Namecheap.** Luettavissa: https://www.namecheap.com/. Luettu: 18.9.2025.
- **ServerFault.** What are all the flags in a dig response? Luettavissa: https://serverfault.com/questions/729025/what-are-all-the-flags-in-a-dig-response. Luettu: 20.9.2025.
- **WhatIsMyIPADdress.** Luettavissa: https://whatismyipaddress.com/. Luettu: 18.9.2025.
- **W3Schools.com.** HTML Tutorial. Luettavissa: https://www.w3schools.com/html/. Luettu: 20.9.2025.
- **Zivanov, S.** PhoenixNAP.dig Command in Linux with Examples. Luettavissa: https://phoenixnap.com/kb/linux-dig-command-examples. Luettu: 20.9.2025.

  Lisäksi käytetty Microsoft Copilotia ongelmanratkaisun tukena.
