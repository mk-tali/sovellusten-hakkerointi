# h5 It's Alive!  

## Ympäristö  
-Debian 13 virtuaalikone, joka pyörii Windows 11 VirtualBoxissa  

## a) Lab1  
Aloitin lataamalla tiedostot tehtävän ohjeista ja purkamalla ne terminaalissa `unzip` komennolla. Siirryin lab1 hakemistoon ja ajoin siellä komennon `gcc gdb_example1.c -g -Wall -Werror -o gdb_example1`. Tämän jälkeen avasin tiedoston gnu debuggerilla `gdb ./gdb_example1`.  
<img width="1036" height="823" alt="image" src="https://github.com/user-attachments/assets/9441686b-3c0f-4309-a390-65a2eb39b2f4" />  
Tutkin ohjelmaa ja huomasin, että se crashaa `print_scrambled(bad_message)` kohdassa. Uskon, että tämä johtuu NULL pointterista `char * bad_message = NULL;`. 

