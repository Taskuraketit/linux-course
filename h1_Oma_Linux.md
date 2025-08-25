# h1 Oma Linux

## x) Lue ja tiivistä (Muutama ranskalainen viiva kustakin artikkelista riittää. Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)
Raportin kirjoittaminen -> linkki: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Raportin kirjoittamisessa tulee huomioida useita seikkoja, mutta pelkällä kaupunkilaisjärjelläkin pääsee jo pitkälle. Oleellisimpia elementtejä raportissa ovat...
1) Täsmällisyys: raportista tulee käydä selkeästi ilmi mitä on tehty ja missä järjestyksessä ja minkälaisin lopputuloksin. 
  Havainnollisuutta voi lisätä liittämällä raporttiin kuvakaappauksia esimerkiksi prompteista, virheilmoituksista jne.
2) Toistettavuus: jos toinen henkilö toistaa raportilla kuvaillut asiat samalla tavalla ja samanlaisessa ympäristössä, lopputuloksenkin _pitäisi_ olla sama.
   Ympäristö voi vaikuttaa oleellisesti lopputulokseen.
3) Helppolukuisuus: raportin luettavuutta voi helpottaa mm. selkeillä kappalejaoilla, väliotsikoilla ja oikeakielisyydellä. Pitkän raportin tapauksessa on hyvä
   lisätä tekstin alkuun selkeä tiivistelmä raportin sisällöstä.

Lisäksi on hyvä muistaa muutamia yleissääntöjä: muista asianmukaiset lähdeviittaukset, käytä tarvittaessa vakiotekstejä (dokumentin kopiointi lisenssin mukaisesti, mitä nettisivua raportin, tehtävän tms. pohjana on käytetty jne.) ja vältä plagiointia sekä sepittämistä.

## a) Asenna Linux virtuaalikoneeseen. (Tee raporttia varten uusi virtuaalikone, vaikka olisit asentanut sen aiemmin)

Tässä tehtävässä käytin asennuksen apuna muistiinpanojani viime keskiviikon Linux-palvelimet-kurssin aloitusluennosta Johanna Heinosen osiosta sekä Johannan GitHubiin tekemää sivua (linkki: https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-20082025.md). Lisäksi asennusta varten kysyin joitain asioita myös ChatGPT:ltä.

### VirtualBoxin asennus

1. Menin sivulle https://www.virtualbox.org/wiki/Downloads ja valitsin sivun vasemmasta reunasta VirtualBox 7.2.0 platform packages -otsakkeen alta "Windows Hosts".
2. Debian ISO imagen latausta varten latasin tarvittavan ISO-tiedoston (debian-live-13.0.0-amd64-xfce.iso) sivulta https://cdimage.debian.org/debian-cd/13.0.0-live/amd64/iso-hybrid/. Asennuksen kliksuttelin kohta kohdalta läpi aloitusluennolla annettujen ohjeiden mukaisesti (OS Versioniin Debian 64-bit, RAMia vähintään 2048 MB, CPU:uita vähintään 2, kovalevytilaa vähintään 20 GB...)
   
Tässä kuvia asennuksen etenemisestä:
<img width="1014" height="501" alt="image" src="https://github.com/user-attachments/assets/3bb40c51-cc0e-476d-b6a2-6dc97b91627c" />
<img width="1026" height="516" alt="image" src="https://github.com/user-attachments/assets/41ef97e1-42ee-45e6-bd8b-962970b65e8a" />
<img width="1017" height="508" alt="image" src="https://github.com/user-attachments/assets/eb95fb27-0153-4428-bff2-f23516b0e21d" />

Tässä valmiin virtuaalikoneen yhteenveto:
<img width="953" height="1015" alt="image" src="https://github.com/user-attachments/assets/7d9c53e7-f0ff-41e7-b438-8b3f053ef97f" />

### Linuxin / Debianin asennus

Valitettavasti en huomannut ottaa tästä osiosta kuvakaappauksia tai tehdä muistiinpanoja, joskin se olisi ollut tärkeää sekä dokumentoinnin että mahdollisen vianmäärityksen kannalta. Yritän kuitenkin kuvailla mahdollisimman selkeästi eri työvaiheet.

1. Käynnistin virtuaalikoneen VirtualBoxissa tuplaklikkaamalla koneen kuvaketta vasemmasta palkista.
2. Tässä näkymässä painoin enteriä avatakseni Debianin:
<img width="619" height="546" alt="image" src="https://github.com/user-attachments/assets/587b5adb-d135-4624-9077-499a63ed5624" />

Kuvan lähde: https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-20082025.md

3. Debian aukesi ja kokeilin klikkailla eri valikoita, avasin komentokehotteen ja avasin nettiselaimen.
4. Komentokehote ei ymmärtänyt ääkkösiä ja monet erikoismerkitkin antoivat eri merkkejä kuin olisi pitänyt. Yritin ensin muuttaa näppäimistön asetukset suomeksi valitsemalla Applications > Settings > Keyboard > Layout-välilehti, poistamalla "English" ja lisäämällä "Finnish" keyboard layoutin. Tämä toki muutti näppiksen suomeksi, mutta asetus ei pysynyt virtuaalikoneen buutin myötä vaan palasi lähtötilanteeseen. Seuraavaksi kokeilin näppäimistöasetusten muuttamista ChatGPT:n ohjeen mukaan:

Vaihe 1: Suorita komento
Avaa terminaali ja kirjoita:

sudo dpkg-reconfigure keyboard-configuration

Paina Enter.
Sinulta pyydetään salasanaa, kirjoita se ja paina Enter.

Vaihe 2: Valitse näppäimistömalli

Näyttöön tulee lista malleista.
Liiku nuolinäppäimillä (↑ ja ↓) kohtaan:
Generic 105-key (Intl) PC
Paina Enter.

Vaihe 3: Valitse näppäimistön asettelu

Seuraavaksi tulee lista kielistä/layouteista.
Liiku nuolinäppäimillä kohtaan:
Finnish
Paina Enter.

Vaihe 4: Other options

Seuraavat kysymykset ovat yleensä oletusarvoja (esim. “Use Control+Alt+Backspace to terminate the X server?”).
Jos haluat jättää oletuksiksi, paina Enter jokaisessa.

Vaihe 5: Tallenna asetukset

Ohjelma tallentaa asetukset automaattisesti, kun olet käynyt läpi kaikki valinnat.
Ei siis tarvita erillistä “Save”-painiketta – Enter viimeisessä valikossa riittää.

Vaihe 6: Aktivoi uusi näppäimistöasetus

Suorita komento:

sudo setupcon

Tämä päivittää näppäimistöasetuksen heti ilman uudelleenkäynnistystä.

(ChatGPT:n ohje päättyy tähän)










