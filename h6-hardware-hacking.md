# Hardware Hacking

## Ympäristö  
-Debian 13 virtuaalikone 4GB RAM, joka pyörii VirtualBoxissa Windows 11 pöytäkoneella. 16GB RAM, AMD Ryzen 7 2700X, Nvidia GTX 1080.  

## 1) Decrypt firmware image  
Aloitin tehtävän lataamalla tp-link-decrypt git repon `git clone https://github.com/robbins/tp-link-decrypt`. Seuraavaksi latasin TapoV3 firmware binäärin `aws s3 cp s3://download.tplinkcloud.com/firmware/Tapo_C200v3_en_1.4.2_Build_250313_Rel.40499n_up_boot-signed_1747894968535.bin Tapo_C200v3_en_1.4.2.bin --no-sign-request`. Jatkoin tp-link-decrypt git repossa olevien ohjeiden mukaan. Ajoin tp-link-decrypt hakemistossa seuraavat komennot `./preinstall.sh` `./extract_keys.sh` ja `make`. `./extract_keys.sh` komento tulosti "permission denied.  
<img width="967" height="545" alt="image" src="https://github.com/user-attachments/assets/aafaf660-00c4-42f6-8b75-ebbe26df2a6e" />  
Eikä antanut RSA avaimia.  
<img width="559" height="41" alt="image" src="https://github.com/user-attachments/assets/f6d0b127-acc2-4aa4-9f97-a52df8d1cead" />  
Minun piti asentaa seuraavat ohjelmat, jotta sain `./extract_keys.sh` toimimaan. `sudo apt install -y python3-pip p7zip-full unzip squashfs-tools` `sudo pip3 install --upgrade pip` `sudo pip3 install jefferson ubi_reader`  
Tässä tuli myös ongelma.  
<img width="1066" height="904" alt="image" src="https://github.com/user-attachments/assets/a6593177-5826-4274-a1b5-460d295030b1" />  
Asensin venv:in ja asensin noi sen sisällä. Se toimi ja sain vihdoin ajettua `./extract_keys.sh` ja decryptattua tiedoston.  
<img width="982" height="324" alt="image" src="https://github.com/user-attachments/assets/572727dd-5784-423b-8ef8-7a6f783b34ab" />

Makefileä piti muokata laittamalla -std=gnu89 CFLAGS kohtaan.  
<img width="670" height="631" alt="image" src="https://github.com/user-attachments/assets/d6ea0abf-5234-4252-a81d-01a2c3ee455d" />  

## 2) Analyse the image file  
Aloin analysoimaan tiedostoa ajamlla komennon `binwalk Tapo_C200v3_en_1.4.2.bin.dec`  
<img width="1836" height="252" alt="image" src="https://github.com/user-attachments/assets/db522fdd-9c66-4d1c-acdd-ec6a4b4bf328" />  
<img width="1804" height="82" alt="image" src="https://github.com/user-attachments/assets/389f2995-5bbb-455b-8de9-c47175934f6c" />  

## 3) extract rootfs from the dump file  
Ajoin komennon `binwalk dump-tapo-c200v3-1.4.2.bin` ja extractasin `binwalk -e dump-tapo-c200v3-1.4.2.bin`. Siirryin extracted kansioon ja sieltä squashfs-root kansioon. 

## 4) extract rootfs from the image file  
Extractasin tiedoston komennolla `binwalk -e Tapo_C200v3_en_1.4.2.bin.dec`. Siirryin tämän yhteydessä luotuun hakemistoon `cd _Tapo_C200v3_en_1.4.2.bin.dec-0.extracted` ja siellä `cd squashfs-root`.  

## 5) search available applications  
Katsoin molemmissa dump ja image fileissa mitä ne sisältävät.  
Dump file.  
<img width="1300" height="1067" alt="image" src="https://github.com/user-attachments/assets/3e6dead9-84ea-4e12-995a-03ac9e6d4b49" />  
<img width="1333" height="364" alt="image" src="https://github.com/user-attachments/assets/678bad3b-0040-4151-93de-c4af5d3903a4" />   
Image file.
<img width="1445" height="573" alt="image" src="https://github.com/user-attachments/assets/a459a9fb-c1a2-4766-855c-d1708c220a4d" />  

## 6) analyse and try to open root password  

Ajoin `ls` ja `file` komentoja ja käytin apuna ChatGPT 5.2 analysoimaan tulostuksia, löytääkseni jotain mistä olisi hyötyä. Näillä en löytänyt mitään, joten ChatGPT ehdotti komentoja `grep -Ri password .` `grep -Ri root .` `grep -Ri login .` `grep -Ri auth .` Nyt löysin seuraavan kohdan, joka näytti mielenkiintoiselta.  
<img width="523" height="59" alt="image" src="https://github.com/user-attachments/assets/4119870f-dba0-40e1-bb49-270addc49e95" />  
<img width="444" height="23" alt="image" src="https://github.com/user-attachments/assets/16b98148-e6d0-4091-bd05-825db16a914a" />  
Tämän jälkeen ajoin komennon `strings bin/main | grep -Ei "pass|admin|root|login"`, josta löytyi hyvin paljon tietoa kirjautumiseen liittyen.  
<img width="1391" height="553" alt="image" src="https://github.com/user-attachments/assets/4484c30d-dac9-4487-9fa3-f5c52be4757f" />  
Tästä en enää ollut varma miten jatkaa ja saada root salasana.

## Lähteet  
robbins/tp-link-decrypt. https://github.com/robbins/tp-link-decrypt  
QKaiser. 2025. Rooting the TP-Link Tapo C200 Rev.5. https://quentinkaiser.be/security/2025/07/25/rooting-tapo-c200/
