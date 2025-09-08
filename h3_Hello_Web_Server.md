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



# b) Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).



# c) Etusivu uusiksi. Tee uusi name based virtual host. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).



# e) Tee validi HTML5 sivu.




# f) Anna esimerkit 'curl -I' ja 'curl' -komennoista. Selitä 'curl -I' muutamasta näyttämästä otsakkeesta (response header), mitä ne tarkoittavat.



# m) Vapaaehtoinen, suosittelen tekemään: Hanki GitHub Education -paketti.



# o) Vapaaehtoinen, vaikea: Laita sama tietokone vastaamaan kahdellla eri sivulla kahdesta eri nimestä. Eli kaksi weppisiteä samalla koneelle, esim. foo.example.com ja bar.example.com. Voit simuloida nimipalvelun toimintaa hosts-tiedoston avulla.
