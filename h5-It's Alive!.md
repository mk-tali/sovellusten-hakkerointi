# h5 It's Alive!  

## Ympäristö  
-Debian 13 virtuaalikone, joka pyörii Windows 11 VirtualBoxissa  

## a) Lab0  
Latasin tiedoston ja purin sen. Ajoin komennon `gdb ./buggy_program` ja ensiksi annoin komennon `list`  
<img width="878" height="231" alt="image" src="https://github.com/user-attachments/assets/3a06dfc2-a151-45c0-86d0-158b7870a79a" />  
Asetin ensimmäisen breakpointin main kohtaan. Menin seuraavaan kohtaan `buggy_functions` komennolla `step` ja laitoin siihen seuraavan breakpointin. Koodissa olevat kommentit auttoivat nopeasti ymmärtämään mikä koodissa on vikana. Sen pystyi todistamaan seuraavasti.  
<img width="878" height="388" alt="image" src="https://github.com/user-attachments/assets/9e3c271a-fe2b-4ac7-a0d0-1617e25c6359" />  
<img width="198" height="114" alt="image" src="https://github.com/user-attachments/assets/4f964969-1709-4f70-bdd0-f8ab611df1a0" />  
Tässä arr[5] tulostaa 0.

## b) Lab1  
Aloitin lataamalla tiedostot tehtävän ohjeista ja purkamalla ne terminaalissa `unzip` komennolla. Siirryin lab1 hakemistoon ja ajoin siellä komennon `gcc gdb_example1.c -g -Wall -Werror -o gdb_example1`. Tämän jälkeen avasin tiedoston gnu debuggerilla `gdb ./gdb_example1`.  
<img width="1036" height="823" alt="image" src="https://github.com/user-attachments/assets/9441686b-3c0f-4309-a390-65a2eb39b2f4" />  
Tutkin ohjelmaa ja huomasin, että se crashaa `print_scrambled(bad_message)` kohdassa. Uskon, että tämä johtuu NULL pointterista `char * bad_message = NULL;`.

## c) Lab2  
Aloitin tehtävän lukemalla README.md tiedoston. Tämän jälkeen ajoin molemmat passtr, sekä passtr2o tiedostot. Molemmat tulostivat täysin saman.  
<img width="530" height="177" alt="image" src="https://github.com/user-attachments/assets/c92ecbee-e0e7-4fb7-a7e4-fc9c670a41f3" />  
Avasin passtr tiedoston gnu debuggerilla. Kun annoin kaksi kertaa komennon list, sain salasanan ja flagin näkyviin.  
<img width="1074" height="390" alt="image" src="https://github.com/user-attachments/assets/709c73a4-b2c8-4b66-8375-f0ad4fa2a865" />  
Tämän jälkeen avasin passtr2o tiedoston gnu debuggerilla. Tällä kertaa list komento ei toiminut, vaan ohjelma tulosti `No symbol table is loaded.  Use the "file" command.` Annoin komennon `info files` ja sain tulokseksi  
<img width="769" height="593" alt="image" src="https://github.com/user-attachments/assets/eff812e7-1ee0-4815-a9f9-b669e9b4028f" />  
Annoin komennon `run` ja ohjelma kysyi salasanaa, mutta ilman oikeaa salasanaa ohjelma palauttaa saman kuin aiemmin, "Sorry, no bonus." Asetin breakpointit kohtoon puts ja printf. Ajoin ohjelman ja annoin väärän salasanan. Ohjelma hyppäsi breakpoint 2:een. Kirjoitin `x/s $rdi` ja ohjelma palautti "Sorry, no bonus.\n". Annoin komennon backtrace, jotta näen missä kohtaa salasanan tarkistus tapahtuu.  
<img width="732" height="57" alt="image" src="https://github.com/user-attachments/assets/65ea5d88-818a-4a3b-805b-fa3ebd6992ee" />  
Menin frame 1:een ja annoin komennon `x/60i $rip-120`.  
<img width="903" height="1098" alt="image" src="https://github.com/user-attachments/assets/a3871dc2-459b-45f9-9319-0dd2b67a489e" />  
Tässä kohtaa menin ihan sekaisin.





