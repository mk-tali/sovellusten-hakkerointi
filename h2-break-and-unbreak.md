Remember systematic working methods and report as you go. Also reflect: Where could this vulnerability be common? How could this mistake be avoided? What did I learn from this?  

# h2 break and unbreak  
## Tiivistelmä  
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

## Lähteet:  
Karvinen tero. 2006. Raportin kirjoittaminen. https://terokarvinen.com/2006/raportin-kirjoittaminen-4/  
Karvinen Tero. 2023. Find Hidden Web Directories - Fuzz URLs with ffuf. https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/  
OWASP Top 10. Broken access control. 2021. https://owasp.org/Top10/2021/A01_2021-Broken_Access_Control/index.html  
PortSwigger. Access control vulnerabilities and privilege escalation. https://portswigger.net/web-security/access-control
