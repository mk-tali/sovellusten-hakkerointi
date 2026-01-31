# h3 No Strings Attached  
## a) Strings n. 15min    
Aloitin lataamalla ezbin-challenges.zip ``wget https://terokarvinen.com/loota/yctjx7/ezbin-challenges.zip`` komennolla. Tämän jälkeen purin kansion ``unzip ezbin-challenges.zip`` Sitten ajoin komennon ``./passtr`` ja kokeilin, mitä tapahtuu jos siihen laittaa vain jotain tekstiä.  
<img width="754" height="154" alt="image" src="https://github.com/user-attachments/assets/3bf4cc46-f35f-468e-a7a1-aeab5421a1aa" />  
Tämän jälkeen kokeilin komentoa ``strings passtr`` ja löysin tämän kohdan.  
<img width="1141" height="184" alt="image" src="https://github.com/user-attachments/assets/63ca3527-1ff6-4f6f-b6b7-dfcecba6276f" />  
Ajoin uudestaan `./passtr` komennon ja kokeilin salasanaksi "sala-hakkeri-321".  
<img width="1123" height="127" alt="image" src="https://github.com/user-attachments/assets/6c1d80ac-cfc5-46db-add2-45a34786bad0" />  

## b) New version of passtr.c 1,5h  
Aloitin tutkimalla miten obfuscoida C koodia. Löysin digital.ai sivulta ohjeet ja linkin githubiin, josta voi asennettua obfuscatorin. (https://digital.ai/catalyst-blog/how-to-obfuscate-c-code/) (https://github.com/obfuscator-llvm/obfuscator?_ga=2.71821587.1866848522.1769697216-782570487.1769697216)  
Asensin obfuscatorin `git clone -b llvm-4.0 https://github.com/obfuscator-llvm/obfuscator.git`. Jatkoin asennusta ohjeiden mukaan  
<img width="607" height="129" alt="image" src="https://github.com/user-attachments/assets/3374b880-d86e-4401-9c0d-e822c768be37" />  
cmake komennon kanssa tuli ongelma, joten kysyin apua ChatGPT:ltä ja se sanoi, että minun ei tarvitse tehdä mitään tästä. Loin uuden tiedoston komennolla `nano passtr_obf.c`. Tänne tiedostoon kirjoitin seuraavan koodin.  
<img width="1470" height="994" alt="image" src="https://github.com/user-attachments/assets/9a34f986-a084-4ae1-b2b7-3b1582a3d98f" />  
Sitten ajoin komennon `gcc -O2 passtr_obf.c -o passtr_obf`  
<img width="1111" height="150" alt="image" src="https://github.com/user-attachments/assets/78ed4310-c5b3-40a0-b97f-cd8192e012f8" />  
Salasana ainakin toimii vielä.
<img width="1124" height="639" alt="image" src="https://github.com/user-attachments/assets/7d1881c7-f517-4772-aacf-4438863592ac" />  
`strings passtr_obf` komennolla salasana ei enää näy. 

## c) Packd  n. 30min
Aloitin ajamalla packd komenolla `./packd`. Ohjelma kysyi salasanaa ja kokeilin syöttämällä jotakin tekstiä.  
<img width="704" height="161" alt="image" src="https://github.com/user-attachments/assets/029137a4-a7da-4047-8291-4cb428976aba" />  
Seuraavaksi kokeilin komentoa `strings packd`, ajattelin jos löytäisin samalla tavalla vastauksen tai jonkun vihjeen, niin kuin a) kohdassa. Löysin seuraavan kohdan.  
<img width="475" height="215" alt="image" src="https://github.com/user-attachments/assets/2afe4fbd-2ef0-4295-a933-4e7f854d241c" />  
Ajoin uudestaan `./packd` komennon ja kokeilin salasanaksi kuvassa näkyvää "Piilos-An", mutta se ei toiminut. Aikaisemmalla strings komennolla löysin myös seuraavan kohdan, mistä ajattelin olevan jotain hyötyä.  
<img width="1251" height="94" alt="image" src="https://github.com/user-attachments/assets/4a6f1b57-42bc-442e-968d-a16538959aca" />  
Etsin internetistä tietoa UPX executable packeristä. Ajattelin, että koska tiedosto on pakattu, se ei näytä kaikkea tietoa. Löysin sivun https://upx.github.io/ Asensin UPX:n komennolla `sudo apt install upx-ucl`. Tämän jälkeen ajoin komennot `upx -t packd` `upx -d packd` Nyt kun ajoin uudestaan `strings packd` salasana ja flag näkyi kokonaan.  
<img width="1136" height="152" alt="image" src="https://github.com/user-attachments/assets/364e8af0-722d-4ca2-a4f9-c0b322a2cb8a" />  
<img width="1115" height="127" alt="image" src="https://github.com/user-attachments/assets/bf5af88e-cf07-466d-b85f-b0d0056a1cc1" />

## Lähteet  
Markus F.X.J. Oberhumer, László Molnár & John F. Reiser. 2024. UPX. https://upx.github.io/


