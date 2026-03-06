# h7 Uhagre2  
## Ympäristö  
-Debian 13 virtuaalikone 4GB RAM, joka pyörii VirtualBoxissa Windows 11 pöytäkoneella. 16GB RAM, AMD Ryzen 7 2700X, Nvidia GTX 1080.  

## Tiivistelmät  
Schneier 2015: Applied Cryptography, 20ed: Chapter 1: Foundations:  

1.1 Terminology ("Historical Terms" to the end)  
-Viesti on plaintextiä ja sen salausta kutsutsaan encryption.  
-Kryptografia myös hoitaa todentamisen, eheyden ja kiistämättömyyden.  
-On olemassa kaksi yleistä avaimiin perustuvaa algoritmiä, symmetrinen ja public-key.  
-Kryptoanalyysi on salauksen purkamista ilman avainta.  
-Historiallisesti koodi viittaa kryptojärjestelmään, joka käsittelee kielellisiä yksilöitä.  
(Schneier 2015)  

1.4 Simple XOR  
-XOR on exclusive-or operaatio
-Tämän murtaminen käy tietokoneellaa muutamassa sekunnissa.  
(Schneier 2015)  

1.7 Large Numbers  
-Tässä kirjassa käytettyjen suurien numeroiden merkitys on helppo unohtaa, joten tässä on annettu taulukko ja esimerkki selitykset niille. Esim todennäköisyys kuolla salamaniskuun on 1 suhde 9miljardiin (2^33).  
(Schneier 2015)  

Python basics for hackers.  
-Palaute on tärkeää.  
-Kannattaa työskennellä pienissä osissa.  
-REPL - Read-Eval-Print, kirjoita komento, aja, katso tulos.  
-iPython antaa lisää ominaisuuksia Python REPL:iin.  
-REPL:iä suurempi ympäristö on F5 compile.  
-Pyhton on hyvä laskin.  
-Salaus käyttää paljon XOR.  
(Karvinen 2024)  

## a) 1. Convert hex to base64  
Muutin hex stringin base64 komennolla `echo "hex" | xxd -r -p | base64` ja sain oikean tuloksen.  
<img width="1438" height="66" alt="image" src="https://github.com/user-attachments/assets/84343791-a5ad-4dd9-b21d-f07602806f9e" />  

## b) 2. Fixed XOR  
Kirjoitin seuraavanlaisen koodin pätkän.  
<img width="463" height="302" alt="image" src="https://github.com/user-attachments/assets/31c8bcfe-6875-49b9-8eb8-0dc1448c1819" />  
Alussa importtasin funktiot. Määritin hex1 ja -2 annetuilla stringeillä. Muutetaan hex -> bytes. Luodaan result buffer. Looppi enumeratella.  
Ajoin koodin ja sain oikean tuloksen.  
<img width="414" height="63" alt="image" src="https://github.com/user-attachments/assets/8d207d49-fe5e-4597-a631-c2f6a7d6dee2" />  

## c) 3. Single-byte XOR cipher  
Kirjoitin seuraavanlaisen koodin.  
<img width="886" height="660" alt="image" src="https://github.com/user-attachments/assets/9a38019b-a3f0-4d2d-be7c-2dc9fcb1d6af" />  
Ohjelma decodaa hexin, kokeilee kaikkia 256 single-byte hex, pisteyttää tulokset sen perusteella, kuinka paljon ne vastaavat englannin kieltä, järjestää ne parhaimman ensiksi ja tulostaa viisi eniten pistettä saanutta vaihtoehtoa.

## Lähteet  
Karvinen. 2024. Python Basics for Hackers. https://terokarvinen.com/python-for-hackers/ 
Schneier 2015: Applied Cryptography, 20ed: Chapter 1: Foundations. https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001 

