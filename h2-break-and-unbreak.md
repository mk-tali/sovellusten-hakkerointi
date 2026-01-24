# h2 break and unbreak  
## Tiivistelmät    
OWASP Top 10 Broken access control  
-Yleisin heikkous  
-Käyttäjäoikeuksien hallinta toteuttaa käytäntöjä niin, että käyttäjät ei pysty toimimaan heille määriteltyjen oikeuksien ulkopuolella.  
-Epäonnistuminen johtaa yleensä tietojen vuotamiseen, muokkaamiseen tai tuhoamiseen  
-Yleisiä heikkouksia on mm: least privilege tao deny by default periaatteen rikkominen ja käyttöoikeustarkistusten ohittaminen muokaamalla URL-osoitetta.  
-Estäminen onnistuu mm: deny by default periaatetta käyttämällä ja toteuttamalla käyttöoikeuksien hallintamekanismit kerran ja hyödyntämällä niitä uudelleen koko sovelluksessa, mukaan lukien Cross-Origin Resource Sharing (CORS) käytön minimointi.  
(OWASP Top10)  

Find Hidden Web Directories - Fuzz URLs with ffuf  
-Webbipalvelimilla on yleensä piilotettuja hakemistoja, joihin ei ole linkkejä missään.  
-Näitä voi etsiä manuaalisesti, mutta fuff tekee sen automaattisesti.  
-Fuff on webbifuzzer, jonka on luonut joohoi.  
-Lataa esimerkkikohde.  
-Asenna fuff.  
-Asenna yleisten verkkopolkujen sanakirja.  
-Aja fuff.  
(Karvinen T. 2023)  

Access control vulnerabilities and privilege escalation  
-Käyttöoikeuksien hallinta määrittää, mitä toimintoja ja resursseja käyttäjä saa käyttää.  
-Oikeuksien korotus voi olla vertikaalista tai horisontaalista  
(PortSwigger)  

Raportin kirjoittaminen
-Toistettava, kaikille tulisi sama lopputulos.
-Täsmällinen, tarkasti kaikki mitä teit.
-Helppolukuinen, väliotsikot, huolellinen kieli.
-Lähdemerkinnät ja viittaukset.
-Vakiotekstit.
-Ei saa sepittää eikä plagioida.
(Karvinen T. 2006)  

## a) Break into 010-staff-only  
Environment: Debian13 Virtuaalikone, joka pyörii Windows 11 koneella. Browser Firefox.   
Ensimmäisenä asensin unzip micron, komennolla sudo apt-get -y install wget unzip micro. Tämän jälkeen latasin https://terokarvinen.com/hack-n-fix/teros-challenges.zip wget komenolla, ja purin unzip komenolla. siirryin cd komenolla challenges/010-staff-only/ hakemistoon ja ajoin python3 staff-only.py komennon. Sitten asensin python3-flask python3-flask-sqlalchemy. python3 staff-only.py komennon jälkeen sain oikean ilmoituksen  
<img width="1599" height="252" alt="image" src="https://github.com/user-attachments/assets/ed87975d-9f41-40a7-8462-860237bb8728" />  
Löysin admin salasanan, kun käytin inspector työkalua PIN koodin syöttökentässä ja poistin input type="number" kohdassa number ja syötin value"" kohtaan "'UNION SELECT password FROM pins-- "  
<img width="643" height="81" alt="image" src="https://github.com/user-attachments/assets/c0f7c135-7932-4409-9f48-a6e9f309efcc" />  
<img width="822" height="88" alt="image" src="https://github.com/user-attachments/assets/fd8e84d3-4960-4a8e-84c9-6153756d3003" />  
<img width="1544" height="281" alt="image" src="https://github.com/user-attachments/assets/8219af2a-3c16-4e1c-9c02-dc3505d386c9" />  
Sain tämän kohdan tehtyä, kun luin Portswiggerin SQL injection UNION attacks kohtaa.  

## b) Fix the 010-staff-only vulnerability from source code  
En osannut korjata haavoittuvuutta, joten katsoin apua Robin Niinemetsin tehtävästä. Sain korjattua haavoittuvuuden.  
<img width="995" height="453" alt="image" src="https://github.com/user-attachments/assets/d153499b-a7a3-4c02-bc1c-eb6cf3626d83" />  
<img width="1186" height="1132" alt="image" src="https://github.com/user-attachments/assets/8a510ed3-7b57-43f4-a1d3-44e7de966aec" />  

## c) Solve dirfuzt-1  
Latasin dirfuzt-1. Avasin sen ja se sanoo dirfutz-1 - Nothing, nil, null, nada. Asensins fuffin. Latasin Dictionary of Common Web Paths. Katkasin nettiyhteyden Virtualboxin host-only network adapterilla. Ajoin ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ  
Jostain syystä, kun yritän ajaa ffufia, se antaa vain erroria  
<img width="1501" height="731" alt="image" src="https://github.com/user-attachments/assets/08615755-e98c-4439-8ad0-947ba2246aa6" />  
Vaikka lopetin dirfuzt-0 



## Lähteet:  
Karvinen tero. 2006. Raportin kirjoittaminen. https://terokarvinen.com/2006/raportin-kirjoittaminen-4/  
Karvinen Tero. 2023. Find Hidden Web Directories - Fuzz URLs with ffuf. https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/  
OWASP Top 10. Broken access control. 2021. https://owasp.org/Top10/2021/A01_2021-Broken_Access_Control/index.html  
PortSwigger. Access control vulnerabilities and privilege escalation. https://portswigger.net/web-security/access-control  
PortSwigger. SQL injection UNION attacks. https://portswigger.net/web-security/sql-injection/union-attacks
