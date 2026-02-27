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


## Lähteet  
robbins/tp-link-decrypt. https://github.com/robbins/tp-link-decrypt
