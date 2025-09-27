# x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)
## Let's Encrypt 2024: How It Works

- **Automaattinen varmenteen hankinta**

  Let's Encrypt käyttää ACME-protokollaa, jonka avulla verkkopalvelin voi automaattisesti pyytää ja asentaa SSL/TLS-varmenteen.

- **Domainin hallinnan todentaminen**

Palvelin todistaa omistavansa domainin joko lisäämällä tietyn tiedoston verkkosivulle (HTTP-haaste) tai lisäämällä DNS-tietueen (DNS-haaste).

- **Ilmainen ja luotettava varmenne**

Kun todentaminen onnistuu, Let's Encrypt myöntää varmenteen, joka on selainten hyväksymä.

- **Uusiminen automaattisesti**

Varmenteet ovat voimassa 90 päivää, ja ne voidaan uusia automaattisesti ennen vanhenemista.

## The Apache Software Foundation 2025: Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To: Basic Configuration Example (Ei "Cipher Suites and Enforcing Strong Security" eteenpäin. Certbot tekee meillä automaattisesti kaikki salaukseen liittyvät asetukset.

**SSL-konfiguraation minimivaatimukset:**

    LoadModule ssl_module modules/mod_ssl.so

    Listen 443
    <VirtualHost *:443>
      ServerName www.example.com
      SSLEngine on
      SSLCertificateFile "/path/to/www.example.com.cert"
      SSLCertificateKeyFile "/path/to/www.example.com.key"
    </VirtualHost>


Auki purettuna SSL:n käyttöönotto Apache-palvelimessa vaatii vähintään nämä vaatimukset:

- SSL-moduulin lataaminen
- Portin 443 (HTTPS) kuuntelu
- Virtuaalipalvelimen määrittely, jossa otetaan SSL käyttöön ja annetaan polut varmenteelle ja yksityiselle avaimelle

**Muut pääkohdat**

- Palvelin voidaan konfiguroida käyttämään vain vahvoja salausmenetelmiä määrittelemällä sopiva salausprofiili (SSLCipherSuite) ja asettamalla palvelin noudattamaan  määriteltyä järjestystä (SSLHonorCipherOrder)
      

  > SSLCipherSuite HIGH:!aNULL:!MD5


- Eri salausasetuksia voidaan soveltaa tietyille URL-poluille, jolloin esim. vain vahvat salaukset vaaditaan tietyissä hakemistossa vaikka muualla sallitaan laajempi valikoima
    

  > SSLCipherSuite RC4-SHA:AES128-SHA:HIGH:!aNULL:!MD5
  > 
  > SSLHonorCipherOrder on
  

# a) Let's. Hanki ja asenna palvelimellesi ilmainen TLS-sertifikaatti Let's Encryptilta. Osoita, että se toimii.

Otin Let's Encrypt -sertifikaatin käyttöön palvelimellani omatoimisesti edellisviikon tehtävien tekemisen jälkeen kun en hoksannut, että se on tulossa omana kohtanaan h6-tehtävissä. Täten minulla ei ole tallessa kuvakaappauksia käyttöönoton vaiheista, mutta joka tapauksessa työvaiheet olivat seuraavat:

Certbotin ja tarvittavien pakettien asennus

> $ sudo apt-get update
>
> $ sudo apt-get install -y certbot python3-certbot-apache

Varmistus, että Apache on käynnissä ja toiminnassa

> $ sudo systemctl status apache2

SSL-sertifikaatin hankinta

> $ sudo certbot --apache

Tämän jälkeen tein seuraavat asiat sitä mukaa kun ohjelma kysyi tietoja:

- Syötin sähköpostiosoitteeni
- Hyväksyin käyttöehdot
- **En** antanut lupaa jakaa sähköpostiosoitettani EFE:lle (Electronic Frontier Foundation)
- Valitsin HTTPS:lle verkkotunnukset 'samulitoropainen.com' ja 'www.samulitoropainen.com'
- Valitsin uudelleenohjauksen (Redirect) HTTP -> HTTPS
- Tämän jälkeen sain vahvistuksen sertifikaatin käyttöönotosta.

Sertifikaatin toimivuuden osoittaminen:

Ajoin palvelimellani komennon

> $ openssl s_client -connect samulitoropainen.com:443

...ja sain tulokseksi pitkän listauksen tuloksista. Tässä alkuosa: 


<img width="791" height="423" alt="image" src="https://github.com/user-attachments/assets/8fe89611-e3d9-42c9-aaec-267fdb8b1007" />


Kun tulosta skrollataan hieman eteenpäin, löytyy seuraava kohta, jonka tulos on toivotunlainen:


<img width="580" height="47" alt="image" src="https://github.com/user-attachments/assets/3f66dffa-80ca-4779-84fa-3ec0c380185c" />


Lisäksi sertifikaatin myöntäjänä (issuer) näkyy 'Let's Encrypt' ja palvelimena (subject) domainini 'samulitoropainen.com'.


<img width="366" height="39" alt="image" src="https://github.com/user-attachments/assets/a7b491e5-2fbe-4ae5-92a1-2442d2b1eb9f" />


Tekstin loppupuolelta löytyy tämä kohta, joka myös on toivotunlainen:


<img width="278" height="31" alt="image" src="https://github.com/user-attachments/assets/46089386-9674-4c68-9ddb-1dd8bf50ab5d" />


Viimeinen vaihe on se, että avatessani selaimessa oman nettisivuni (joka on yhdistetty palvelimeeni), selaimen osoiterivillä näkyy lukon kuva:


<img width="1031" height="231" alt="image" src="https://github.com/user-attachments/assets/a36dfabd-88ce-4b10-a22f-f8365d74fc62" />


# b) A-rating. Testaa oma sivusi TLS jollain yleisellä laadunvarmistustyökalulla, esim. SSLLabs (Käytä vain tavanomaisia tarkistustyökaluja, ei tunkeutumistestausta eikä siihen liittyviä työkaluja)

Menin osoitteeseen https://www.ssllabs.com/ssltest/ ja syötin sivun Hostname-kenttään oman domainnimeni 'samulitoropainen.com'. Laitoin täpän ruutuun kohdassa "Do not show the results on the boards", koska en ole varma voiko domainnimeni näkymisellä tuollaisessa paikassa olla haitallisia vaikutuksia. Painoin "Submit" ja jäin seuraamaan analyysin edistymistä.


<img width="1115" height="377" alt="image" src="https://github.com/user-attachments/assets/b769fd66-1b6e-47f8-b1b6-83f15b918904" />


**Analyysi käynnissä:**


<img width="1104" height="244" alt="image" src="https://github.com/user-attachments/assets/c32845c8-1c55-4a10-8270-cb0fcb435d1b" />


**Yhteenveto**


<img width="1104" height="612" alt="image" src="https://github.com/user-attachments/assets/a4f0688f-b3f8-4ebe-b233-44f2dfd5950d" />


**Sertifikaatin tiedot**


<img width="994" height="681" alt="image" src="https://github.com/user-attachments/assets/2678f37d-32f7-4b22-b005-4ffa4cdf5bfb" />


<img width="996" height="470" alt="image" src="https://github.com/user-attachments/assets/de925810-d680-4377-b66c-8800ab8cd977" />


**...ja kenties koko tehtävän pihvi tulee tässä:**


<img width="997" height="296" alt="image" src="https://github.com/user-attachments/assets/eda9fbb2-0994-47dc-ad7e-47022972fbc7" />


# c) Vapaaehtoinen: Tee weppilomake, jossa on käyttäjätunnus ja salasana. Käytä salaamatonta http-yhteyttä. Sieppaa liikennettä (esim. Wireshark, ngrep). Mitä havaitset? Mitä vaikutuksia tällä on tietoturvaan?


Loin hakemistoon /var/www/html uuden tiedoston login.html


<img width="535" height="295" alt="image" src="https://github.com/user-attachments/assets/76e8d35b-89ad-4e94-8cf1-23de0d6f2042" />


Tein tiedostoon html:llä yksinkertaisen kirjautumislomakkeen ja tallensin muutokset:


<img width="601" height="362" alt="image" src="https://github.com/user-attachments/assets/f6f9e21b-7749-490d-9298-dde3abce0d8d" />


Käynnistin uudelleen Apachen


> $ sudo systemctl restart apache2


<img width="655" height="46" alt="image" src="https://github.com/user-attachments/assets/fd22f4f4-3dc3-447c-b94a-c9b7dc05849d" />


Avasin selaimessa sivun 'http://80.69.172.107/login.html' ja syötin sivulle hatusta vedetyt kirjautumistunnukset. Mielenkiintoinen havainto oli, että selainkin varoitti yhteyden salaamattomuudesta. Painoin "Kirjaudu"-painiketta.


<img width="671" height="397" alt="image" src="https://github.com/user-attachments/assets/a59a41c2-aea2-4aa0-8e6a-6935b1cdd72c" />


Syötin terminaalissa komennon, jolla yritin tarkastella http-liikennettä, mutta sain ilmoituksen ettei ngrep-työkalua ole asennettu joten asensin sen.


> $ sudo ngrep -d any -q -W byline "POST" port 80

<img width="784" height="38" alt="image" src="https://github.com/user-attachments/assets/3f6e914a-cc6a-489c-924e-d093d85368dd" />


> $ sudo apt-get update
>
> $ sudo apt-get install -y ngrep


<img width="924" height="683" alt="image" src="https://github.com/user-attachments/assets/837b6833-d441-4978-a60e-2ce12234aa06" />


Syötin aiemman komennon uudelleen

> $ sudo ngrep -d any -q -W byline "POST" port 80


Tulokset eivät kuitenkaan olleet ihan sitä mitä piti:


<img width="797" height="101" alt="image" src="https://github.com/user-attachments/assets/d3f89dd2-a16c-477e-87e6-29f8fab314ab" />


Tarkistutin Copilotilla koodin ja se huomautti, että h2-otsikon alta puuttuu '/login' joten lisäsin sen koodiin. Lisäksi löysin apuja toisesta lähteestä ja muokkasin lomakkeen sisältöä seuraavanlaiseksi:


<img width="620" height="400" alt="image" src="https://github.com/user-attachments/assets/dbe9dc2c-de4f-428b-a624-a2e96a41068f" />


Käynnistin taas apachen uudestaan ja testasin kirjautumista.


> $ sudo systemctl restart apache2


Tällä kertaa "kirjautuminen" meni eteenpäin:


<img width="785" height="297" alt="image" src="https://github.com/user-attachments/assets/31da44a3-0e77-498c-aaf2-214c7a8a640d" />


Tarkistus terminaalissa:


> $ sudo ngrep -d any -q -W byline "POST" port 80

Kokeilin lomakkeen täyttöä uudelleen ja huomasin, että em. komento ilmeisesti tuottaa tuloksia reaaliajassa:


<img width="859" height="296" alt="image" src="https://github.com/user-attachments/assets/78b00abf-3a2c-4832-b4d8-6babe4fbc016" />


Tässä ei kuitenkaan näy kirjautumistietoja, joiden ilmeisesti pitäisi näkyä.


Valitettavasti tässä kohtaa en ehtinyt tehdä enempää vianmääritystä tämän suhteen joten jatkan (ehkä) tehtävää myöhemmin. Joka tapauksessa voidaan todeta seuraavaa:

- POST-pyynnön sisällä tietojen *pitäisi* näkyä selväkielisenä, mikä aiheuttaa ilmeisen tieoturvaongelman
- Selväkielisyys mahdollistaa vakoilun ja tunnusten sieppaamisen
- Selaimet eivät automaattisesti estä HTTP-yhteyttä, mutta sen käyttö on teknisesti mahdollista (onneksi ainakin virtuaalikoneella Firefox varoitti lomakkeella salaamattomuudesta)
- Tietoturvaongelmat voivat aiheuttaa riskin tietomurrolle sekä asiakkaiden luottamuksen menettämiselle, minkä vuoksi tuotantoympäristössä tulisi aina käyttää salattua yhteyttä (HTTPS)

# Lähteet:

- **Karvinen, T.** Linux-palvelimet. h6 Salataampa. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu: 27.9.2025.
- **Let's Encrypt**. How it works. Luettavissa: https://letsencrypt.org/how-it-works/. Luettu: 27.9.2025.
- **Req Bin**. HTTP POST Request Method. Luettavissa: https://reqbin.com/Article/HttpPost/. Luettu: 27.9.2025.
- **SSL Labs**. SSL Test. Luettavissa: https://www.ssllabs.com/ssltest/. Luettu: 27.9.2025.

Lisäksi käytetty ongelmanratkaisun tukena ChatGPT:tä ja Copilotia.







