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

## d) Nora CrackMe  



