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




# b) Based. Laita Name Based Virtual Host näkymään uudessa nimessäsi. Kotisvuja pitää pystyä muokkaamaan ilman pääkäyttäjän oikeuksia.


# c) Kotisivu. Tee vähintään kolmen erillisen alasivun (esim. index.html, blog.html, projects.html) kotisivu ja kopioi se näkymään palvelimellesi. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.


# d) Alidomain. Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com). Tässä tehtävässä riittää, että alidomainit avaavat saman sivun kuin päädomain. (Vapaaehtoinen bonus: Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Vapaaehtoinen bonus: tee alidomainiin oma erillinen name based virtual host.)


# e) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset, keskity nimipalvelimelta tulleisiin kenttiin (dig näyttää paljon muutakin tietoa). Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:

## Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.

## Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).

## Jonkin suuren ja kaikkien tunteman palvelun tiedot.


# f) Vapaaehtoinen bonus: Aakkossalaattia sähköpostiin. Etsi palvelu, jonka DNS-tiedoissa on SPF ja DMARC. Selitä näiden kenttien osat ja vaikutukset yksityiskohtaisesti. Voit halutessasi käyttää tulkinnan apuna jotain ohjelmaa tai palvelua, kunhan selität ja tulkitset lopputuloksen myös itse.
