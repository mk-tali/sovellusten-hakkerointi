# h4 Some Disassembly Required  
## Summary  
Ghidra for Reverse Engineering (PicoCTF 2022 #42 'bbbloat')  
-Ennen Ghidraa kokeillaan yksinkertaiset ltrace ja strace  
-Asennetaan ja puretaan Ghidra  
-Avataan bbbbloat Ghidrassa  
-Etsitään strings  
-if funktiosta löytyi hexadesimaali luku, joka oli oikea vastaus, kun sen muutti normaaliksi luvuksi  

## a) Install Ghidra  
Asensin openjdk:n ja Ghidran Debian 13 koneelle komennoilla `sudo apt install openjdk-21-jdk` `wget https://github.com/NationalSecurityAgency/ghidra/releases/download/Ghidra_11.1.2_build/ghidra_11.1.2_PUBLIC_20240709.zip` ja purin sen komennolla `unzip ghidra_11.1.2_PUBLIC_20240709.zip`  

## b) rever-C  14:30
Avasin Ghidran ja loin uuden projektin, jossa avasin packd tiedoston. Katsoin ensin Window kohdasta defined strings ja löysin kohdan "What's the password?" Klikkasin siitä ja katson mitä se näytti.  
<img width="1758" height="965" alt="image" src="https://github.com/user-attachments/assets/bd54b769-d8ed-46a5-bd13-f92b18b34ecd" />  
Ei näyttänyt olevan mitään hyödyllistä. Seuraavaksi kävin funktioita läpi kunnes löysin  
<img width="599" height="496" alt="image" src="https://github.com/user-attachments/assets/2f82cb3a-b180-482d-8d9b-c729461c7a44" />  
Tämä näytti siltä, että voisi olla pääohjelma. Aloin tutkimaan tätä funktiota tarkemmin. Sen sain ainakin selvitettyä, että var on käyttäjän syöte, joten nimesin sen "user_input". käyttäjän syötettä verrataan FUN_001053a7(0x1063a7). Jos vertailu on totta, ohjelma palauttaa 0. Muussa tapauksessa ohjelma palauttaa FUN_001053a7(0x1063ed).  

## c) If backwards 3h  
Avasin Ghidralla passtr tiedoston. Etsin kohdan, jossa on main funktio.  
<img width="992" height="446" alt="image" src="https://github.com/user-attachments/assets/f1dcf937-e71f-4b76-aeea-678d6991174a" />  

## d) Nora CrackMe Compile to binaries  
Luin README.md tiedoston ja kloonasin git repon debian koneelleni `git clone https://github.com/NoraCodes/crackmes.git`. Siirryin crackmes hakemistoon `cd crackmes`. Sitten ajoin komennon `make`.  

## e) Nora crackme01  
Aloitin ajamalla ohjelman komennolla `./crackme01.64` ja katsoin, mitä ohjelma tekee.  
<img width="457" height="65" alt="image" src="https://github.com/user-attachments/assets/ad685352-b092-471a-b188-1f8925e173c3" />  
Koska ohjelma pyytää yhtä argumenttia, kokeilin seuraavaa.  
<img width="488" height="66" alt="image" src="https://github.com/user-attachments/assets/6ac98935-e133-4882-bb36-8d568bc168f4" />  
Näistä sain käsityksen, miten ohjelma toimii, mutta ei auttanut minua ratkaisemaan tehtävää. Seuraavaksi kokeilin komentoa `strings crackme01.64` sieltä löysin seuraavan.  
<img width="285" height="79" alt="image" src="https://github.com/user-attachments/assets/d7acfa59-1b6e-4e8f-a6d8-49d2a892193a" />  
Kokeilin syöttää "password1" aikaisemman "test" tilalle ja sain ratkottua tehtävän.  
<img width="559" height="66" alt="image" src="https://github.com/user-attachments/assets/38e7c7f5-8081-4903-8e5e-3eee8b7b4af7" />  

## e) Nora crackme01e  
Kokeilin nyt suoraan komentoa `strings crackme01e.64` ja löysin kohdan  
<img width="310" height="83" alt="image" src="https://github.com/user-attachments/assets/0795b9ad-c09b-4dbf-a5c2-fc994f4b0987" />  
Yritin komentoa `./crackme01e.64 slm!paas.k`, mutta nyt sain virheilmoituksen  
<img width="552" height="41" alt="image" src="https://github.com/user-attachments/assets/2518fe60-24ad-450f-9f7e-38845f580627" />  
Kokeilin laittaa salasanan heittomerkkeihin ja se toimi.  
<img width="578" height="41" alt="image" src="https://github.com/user-attachments/assets/db9670ce-aa63-49b5-82f4-98b6cefa6d7d" />  

## f) Nora crackme02  
Loin uuden projektin Ghidrassa ja avasin siellä tiedoston crackme02.64. Tässä on main funktio ennen muutoksia. Tutkin sitä, ja mietin mitä mikäkin kohta tekee.  
<img width="460" height="537" alt="image" src="https://github.com/user-attachments/assets/b68fc470-ce71-4abf-af3c-65b3571d76d9" />  





## Lähteet:
John Hammond. 2022. GHIDRA for Reverse Engineering (PicoCTF 2022 #42 'bbbloat'). https://www.youtube.com/watch?v=oTD_ki86c9I  
Leonora Tindall (NoraCodes). Crackmes. https://github.com/NoraCodes/crackmes 



