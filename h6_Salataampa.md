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

SSL-konfiguraation minimivaatimukset:

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

Muut pääkohdat

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






# c) Vapaaehtoinen: Tee weppilomake, jossa on käyttäjätunnus ja salasana. Käytä salaamatonta http-yhteyttä. Sieppaa liikennettä (esim. Wireshark, ngrep). Mitä havaitset? Mitä vaikutuksia tällä on tietoturvaan?
