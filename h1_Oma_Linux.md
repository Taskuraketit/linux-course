# h1 Oma Linux

## x) Lue ja tiivistä (Muutama ranskalainen viiva kustakin artikkelista riittää. Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)
Raportin kirjoittaminen -> linkki: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Raportin kirjoittamisessa tulee huomioida useita seikkoja, mutta pelkällä kaupunkilaisjärjelläkin pääsee jo pitkälle. Oleellisimpia elementtejä raportissa ovat...
1) Täsmällisyys: raportista tulee käydä selkeästi ilmi mitä on tehty ja missä järjestyksessä ja minkälaisin lopputuloksin. 
  Havainnollisuutta voi lisätä liittämällä raporttiin kuvakaappauksia esimerkiksi prompteista, virheilmoituksista jne.
2) Toistettavuus: jos toinen henkilö toistaa raportilla kuvaillut asiat samalla tavalla ja samanlaisessa ympäristössä, lopputuloksenkin _pitäisi_ olla sama.
   Ympäristö (koti, Haaga-Helian kampus, Pohjois-Haagan kirjasto...) voi vaikuttaa oleellisesti lopputulokseen.
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



