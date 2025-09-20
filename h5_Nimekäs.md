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


> sudo micro /etc/fail2ban/jail.local


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


> sudo fail2ban-client status apache


Asetin aiemmalle hyökkääjä-IP:lle estot


> $ sudo fail2ban-client set apache banip 45.88.186.32



Tarkistin aktiiviset prosessit:


> ps aux



Tarkistin mahdolliset uudet käyttäjät



> cat /etc/passwd



Tarkistin verkkoyhteydet



> netstat -tulnp



Tarkistin onko index.html- tai muita tiedostoja muokattu



> ls -l /var/www/html



Asensin ja ajoin rkhunter-ohjelman Rootkit-ohjelmien varalta:



> sudo apt-get install rkhunter chkrootkit

> sudo rkhunter --check

> sudo chkrootkit


Rkhunterin tulokset olivat muuten puhtaat, mutta ohjelma varoitti seuraavasta:


<img width="550" height="52" alt="image" src="https://github.com/user-attachments/assets/c0d4a68f-3b93-4be1-9844-f296e98744ed" />



Copilotin tulkinta: 


<img width="634" height="266" alt="image" src="https://github.com/user-attachments/assets/b278898e-c64d-42f3-8478-6c059aeaaa60" />



Tarkistin /dev-hakemiston:


> ls -l /dev | grep -v '^c\|^b'



Tarkistin piilotetut tiedostot:


> sudo find / -name ".*" -type f 2>/dev/null



Mitään epäilyttävää ei löytynyt joten tulkitsin tämän **false positive -tilanteeksi**.



Tässä kohtaa menin uudelleen katsomaan samulitoropainen.com-sivua ja yllätyksekseni se oli päivittyyt oikeanlaiseksi eli TTL oli ilmeisesti jostain syystä pidempi kuin NameCheap.com-sivulle asettamani 5 minuuttia.



<img width="1281" height="885" alt="image" src="https://github.com/user-attachments/assets/842b211f-ca7b-4e4d-8e24-d632a7397b73" />



Ja näin sivu skaalautuu mobiililaitteella (iPhone 12):


<img width="1170" height="2532" alt="image" src="https://github.com/user-attachments/assets/b8efd28f-7dd5-42c8-88a2-0d7f396df361" />



# b) Based. Laita Name Based Virtual Host näkymään uudessa nimessäsi. Kotisvuja pitää pystyä muokkaamaan ilman pääkäyttäjän oikeuksia.


# c) Kotisivu. Tee vähintään kolmen erillisen alasivun (esim. index.html, blog.html, projects.html) kotisivu ja kopioi se näkymään palvelimellesi. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.


# d) Alidomain. Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com). Tässä tehtävässä riittää, että alidomainit avaavat saman sivun kuin päädomain. (Vapaaehtoinen bonus: Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Vapaaehtoinen bonus: tee alidomainiin oma erillinen name based virtual host.)


# e) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset, keskity nimipalvelimelta tulleisiin kenttiin (dig näyttää paljon muutakin tietoa). Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:

## Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.

## Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).

## Jonkin suuren ja kaikkien tunteman palvelun tiedot.


# f) Vapaaehtoinen bonus: Aakkossalaattia sähköpostiin. Etsi palvelu, jonka DNS-tiedoissa on SPF ja DMARC. Selitä näiden kenttien osat ja vaikutukset yksityiskohtaisesti. Voit halutessasi käyttää tulkinnan apuna jotain ohjelmaa tai palvelua, kunhan selität ja tulkitset lopputuloksen myös itse.
