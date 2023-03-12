

# h14_Uusi_komento

**Tehtävänanto:**

a) Tee Linuxiin uusi komento Bashilla. Komennon tulee toimia kaikilla käyttäjillä, työhakemistosta riippumatta. Tee jotain muuta kuin "hei maailma".  
b) Tee Linuxiin uusi komento Pythonilla. Komennon tulee toimia kaikilla käyttäjillä, työhakemistosta riippumatta.  
c) Tee Linuxiin komento, joka tekee jotain monelle tiedostolle  

**Vinkit:**

- Kannattaa harjoitella arviotavaa labraa varten  
  - Voit esimerkiksi tehdä kaikki kurssin harjoitukset läpi tyhjälle tietokoneelle (ilman että raportoit niitä uudelleen).  
  - Vanhoja arvioitavia labroja löytyy netistä. Toki eri kursseilla olen saattanut opettaa eri ohjelmilla tai kielillä, joten kannattaa katsoa tehtäviä soveltuvin osin  
  - Perusasiat: aina hyvät salasanat, testaa kaikki, oikeudet oikein...  

[Lähde: Linux-palvelimet 2023 alkukevät](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)   

---
## Tehtävät  

### a) Tee Linuxiin uusi komento Bashilla. Komennon tulee toimia kaikilla käyttäjillä, työhakemistosta riippumatta. Tee jotain muuta kuin "hei maailma".  

Luodaan kansio tälle tehtävälle ja mennään kyseiseen kansioon:  

    nadja@debian:~$ mkdir tryscripts
    nadja@debian:~$ cd tryscripts/ 
    
Luodaan tiedosto **tervehdi**:  

    nadja@debian:~/tryscripts$ micro tervehdi

    ->
    echo "Tervehdys!" 
    
Kokeillaan:  

    nadja@debian:~/tryscripts$ bash tervehdi  
    
![Näyttökuva 2023-03-10 183156](https://user-images.githubusercontent.com/118609353/224371010-955c25ea-2ad9-4873-ae6d-dd1cdaa7bd70.png)  

Tiedoston **tervehdi** tiedostopolku:  

    nadja@debian:~/tryscripts$ realpath tervehdi 
    
    ->
    /home/nadja/tryscripts/tervehdi  
    
  
Kokeillaan ajaa ilman että kirjoitetaan 'bash' eteen (kolmella tavalla):  

    nadja@debian:~/tryscripts$ /home/nadja/tryscripts/tervehdi
    
    ->
    bash: /home/nadja/tryscripts/tervehdi: Permission denied
    
    nadja@debian:~/tryscripts$ ./tervehdi
    
    ->
    bash: ./tervehdi: Permission denied
    
    nadja@debian:~/tryscripts$ tervehdi
    
    ->
    bash: tervehdi: command not found
    
    
![Näyttökuva 2023-03-10 184413](https://user-images.githubusercontent.com/118609353/224373486-c44f822c-0165-406f-85cd-33f6d82b7eb4.png)

Katsotaan, millaiset tiedoston luku-, kirjoitus- ja suoritusoikeudet (read,write,execute) ovat tällä hetkellä:  

  
    nadja@debian:~/tryscripts$ ls -l tervehdi 
    
    ->
    -rw-r--r-- 1 nadja nadja 19 Mar 10 18:29 tervehdi  
    
    
![Näyttökuva 2023-03-10 185242](https://user-images.githubusercontent.com/118609353/224375430-544fd2c5-3e4d-40eb-a320-3dbc6c47539f.png)

    
    -       = file  
    user:   rw-
    group:  r--
    other:  r--  
    
    
Muokataan oikeuksia niin, että kaikille lisätään oikeus suorittaa (x=execute):  
<!--HUOM! Others-joukkioon kuuluville ei tule antaa write-oikeuksia-->  

    nadja@debian:~/tryscripts$ chmod ugo+x tervehdi 
    
    u=user
    g=group
    o=others
    +=add
    
Tarkistetaan, että oikeudet menivät niin kuin oli tarkoituskin:  

    nadja@debian:~/tryscripts$ ls -l tervehdi 
    -rwxr-xr-x 1 nadja nadja 19 Mar 10 18:29 tervehdi  
    
    -       = file  
    user:   rwx
    group:  r-x
    other:  r-x  
    
    
Testataan:  

    nadja@debian:~/tryscripts$ /home/nadja/tryscripts/tervehdi
    
    ->
    Tervehdys!
    
    nadja@debian:~/tryscripts$ ./tervehdi 
    
    ->
    Tervehdys!
    
    nadja@debian:~/tryscripts$ tervehdi
    
    ->
    bash: tervehdi: command not found
    

    
![Näyttökuva 2023-03-10 191147](https://user-images.githubusercontent.com/118609353/224379551-ee1c3689-c16a-4aed-8d27-a299811632d4.png)

Määritellään millä ohjelmaa ajetaan:  
<!-- 
#!/bin/bash
#kertoo millä komentotulkilla tulkitaan -->  

    nadja@debian:~/tryscripts$ micro tervehdi 
    
    ->
    #!/usr/bin/bash
    
    echo "Tervehdys!"   
    
Tehdään tiedostosta **tervehdi** kopio hakemistoon **/usr/local/bin/**, (jossa tarkistaessani ei näkynyt vielä yhtään tiedostoa):  


<!-- Kohdekansion sisältö on hyvä tarkistaa samannimisten tiedostojen varalta, sillä cp kirjoittaa hakemistossa jo olevan samannimisen tiedoston päälle. 
Tässä vaiheessa ./tervehdi ja tervehdi ovat eri ohjelmat, tervehdi on kopio ./tervehdi:stä. Kannattaa huomata ohjelmaa muokatessa. -->

    nadja@debian:~/tryscripts$ sudo cp tervehdi /usr/local/bin/
 
![Näyttökuva 2023-03-10 192605](https://user-images.githubusercontent.com/118609353/224382546-18010b21-d650-4d6e-b435-e2186237a873.png)  

Testataan:  

    nadja@debian:~/tryscripts$ tervehdi 
    nadja@debian:/usr/local/bin$ tervehdi 
    
    ->
    Tervehdys!
  
![Näyttökuva 2023-03-10 193501](https://user-images.githubusercontent.com/118609353/224384357-bfa6776b-c99f-448c-86fd-a6465b1fe77c.png)


Lisätään tiedostoon **tervehdi** (alkuperäinen tiedosto) myös päiväys, niin kopio ja alkuperäinen on helpompi erottaa toisistaan:  

    nadja@debian:~/tryscripts$ micro tervehdi 
    
    ->
    #!/usr/bin/bash

    echo "Tervehdys!" 
    echo "Tänään on: "
    date --iso
   
   
Ja kokeillaan:  

    nadja@debian:~/tryscripts$ ./tervehdi
    
    ->
    Tervehdys!
    Tänään on: 
    2023-03-10
    
    nadja@debian:~/tryscripts$ tervehdi 
    
    ->
    Tervehdys!
    

![Näyttökuva 2023-03-10 194651](https://user-images.githubusercontent.com/118609353/224387271-ae0e89b5-bcc1-4b04-b318-6e3ef24bebbf.png)


Luodaan uusi käyttäjä ja kokeillaan, toimiiko komennon ajaminen myös toisella käyttäjällä:  

    nadja@debian:~$ sudo adduser testierkki
    nadja@debian:~$ su testierkki
    
    testierkki@debian:/home/nadja$ tervehdi 
    
    ->
    Tervehdys!
    
    

![Näyttökuva 2023-03-10 201717](https://user-images.githubusercontent.com/118609353/224393095-deb6963c-d7f2-4db7-bd03-642f1919e99e.png)  


Päivitetään vielä hakemistossa /usr/local/bin/ oleva **tervehdi** -tiedosto niin että siinäkin näkyy päiväys:  

    nadja@debian:~/tryscripts$ sudo cp tervehdi /usr/local/bin/
    
Ja kokeillaan testierkki -tunnuksella:  

    testierkki@debian:~$ tervehdi 
    
    ->
    Tervehdys!
    Tänään on: 
    2023-03-10
    

![Näyttökuva 2023-03-10 202745](https://user-images.githubusercontent.com/118609353/224394972-9e342e65-dc62-424c-8748-8a340323088d.png)

<!--
    nadja@debian:~/tryscripts$ micro ihanapaiva
    nadja@debian:~/tryscripts$ micro ihanapaiva
    -> 
    echo "Tervehdys!"
    nadja@debian:~/tryscripts$ bash ihanapaiva
    nadja@debian:~/tryscripts$ ls -l ihanapaiva
    nadja@debian:~/tryscripts$ chmod ugo+x ihanapaiva
    nadja@debian:~/tryscripts$ ls -l ihanapaiva
    nadja@debian:~/tryscripts$ ./ihanapaiva
    nadja@debian:~/tryscripts$ micro ihanapaiva
    -> 
    #!/usr/bin/bash/ 
    echo "Tervehdys"
    nadja@debian:~/tryscripts$ ./ihanapaiva  
    nadja@debian:~/tryscripts$ sudo cp ihanapaiva /usr/local/bin/
    testierkki@debian:~$ ihanapaiva
-->


---

### b) b) Tee Linuxiin uusi komento Pythonilla. Komennon tulee toimia kaikilla käyttäjillä, työhakemistosta riippumatta.  


Luodaan  tiedosto **moropy** kansioon **tryscripts**:  

    nadja@debian:~/tryscripts$ micro moropy

    ->
    print("Koodaamisen iloa!")
    
Kokeillaan:  

    nadja@debian:~/tryscripts$ python3 moropy  
    
    ->
    Koodaamisen iloa!


![Näyttökuva 2023-03-10 205555](https://user-images.githubusercontent.com/118609353/224402569-239a367e-5c53-4e08-9f12-7ee21637246a.png)

Päivitetään oikeudet ja testataan:  

    nadja@debian:~/tryscripts$ ls -l moropy 
    
    ->
    -rw-r--r-- 1 nadja nadja 27 Mar 10 20:52 moropy
    
    nadja@debian:~/tryscripts$ chmod ugo+x moropy 
    
    nadja@debian:~/tryscripts$ ls -l moropy 
    
    ->
    -rwxr-xr-x 1 nadja nadja 27 Mar 10 20:52 moropy
    
    nadja@debian:~/tryscripts$ ./moropy 
    
    ->
    ./moropy: line 1: syntax error near unexpected token `"Koodaamisen iloa!"'
    ./moropy: line 1: `print("Koodaamisen iloa!")'

    
    
![Näyttökuva 2023-03-10 205904](https://user-images.githubusercontent.com/118609353/224403168-4ef49e76-9618-4ec0-abf2-9a7d699daee2.png)
  
Tarkistetaan missä python on:  

    nadja@debian:~/tryscripts$ which python3
    
    ->
    /usr/bin/python3
    
Lisätään polku, missä python on tiedostoon **moropy**:  
    
    nadja@debian:~/tryscripts$ micro moropy 
    
    ->
    #!/usr/bin/python3

    print("Koodaamisen iloa!")  
    
    
Ja testataan:  

    nadja@debian:~/tryscripts$ ./moropy 
    
    ->
    Koodaamisen iloa!  
    
    
Kopioidaan **moropy** hakemistoon /usr/local/bin/:  

    nadja@debian:~/tryscripts$ sudo cp moropy /usr/local/bin/

Ja testataan:  

    testierkki@debian:~$ moropy 
    
    ->
    Koodaamisen iloa!




![Näyttökuva 2023-03-10 210734](https://user-images.githubusercontent.com/118609353/224404591-4028c8bd-3541-44cc-b0aa-5be6af6144ec.png)

Muokataan vielä alkuperäistä **moropy** -tiedostoa:  

    nadja@debian:~/tryscripts$ micro moropy 

    ->
    #!/usr/bin/python3

    print("")
    username = input("Kukas siellä: ")
    print("Koodaamisen iloa,  " + username + "!")
    
    
Testataan:  

    nadja@debian:~/tryscripts$ ./moropy 

    Kukas siellä: nadja
    Koodaamisen iloa,  nadja!
    
Ja kopioidaan tiedosto **moropy** hakemistoon /usr/local/bin/:  

    nadja@debian:~/tryscripts$ sudo cp moropy /usr/local/bin/
    
    
Testataan käyttäjällä testierkki:  

    testierkki@debian:~$ moropy 

    ->
    Kukas siellä: Erkki
    Koodaamisen iloa,  Erkki!


![Näyttökuva 2023-03-10 211611](https://user-images.githubusercontent.com/118609353/224406109-32379baf-5558-4d3d-8d68-ea02cdaae6e0.png)
    





    
  

---
### c) Tee Linuxiin komento, joka tekee jotain monelle tiedostolle  



#### hae

Tehdään komento, joka kysyy etsittävän tiedostonimen ja tulostaa etsityn tiedoston rivien sisällön. 

Luodaan tiedosto **hae:**  

    nadja@debian:~/tryscripts$ micro hae
    
    ->     
    #!/usr/bin/bash
    read -p "Enter file name : " filename
    while read line
    do 
    echo $line
    done < $filename  
    
    
Testataan hakemalla tiedostoa **moropy**:  

    nadja@debian:~/tryscripts$ bash hae
    
    ->
    Enter file name : moropy
    
    ->
    #!/usr/bin/python3

    print("")


    username = input("Kukas siellä: ")
    print("Koodaamisen iloa, " + username + "!")  
    
![Näyttökuva 2023-03-13 001921](https://user-images.githubusercontent.com/118609353/224577191-e905a8ac-032c-435a-9ce9-cc847cecd332.png)

    
Oikeudet:  

    nadja@debian:~/tryscripts$ ls -l hae
    
    ->
    -rw-r--r-- 1 nadja nadja 102 Mar 13 00:03 hae

    nadja@debian:~/tryscripts$ chmod ugo+x hae
    
    nadja@debian:~/tryscripts$ ls -l hae
    
    ->
    -rwxr-xr-x 1 nadja nadja 102 Mar 13 00:03 hae  
    
    
Testataan hakemalla tiedostoa **tervehdi**:  

    nadja@debian:~/tryscripts$ ./hae
    
    ->
    Enter file name : tervehdi
    
    ->
    #!/usr/bin/bash

    echo "Tervehdys!"
    echo "Tänään on: "
    date --iso
    
    
![Näyttökuva 2023-03-13 002045](https://user-images.githubusercontent.com/118609353/224577288-773fdbcb-705f-4742-8505-143aeb44bdb5.png)

    
    
Kopioidaan tiedosto **hae** hakemistoon **/usr/local/bin/**:  

    nadja@debian:~/tryscripts$ sudo cp hae /usr/local/bin/
    
    
Testataan käyttäjällä **testierkki**  


    testierkki@debian:/home/nadja/tryscripts/testitiedostot$ hae

    ->
    Enter file name : tiedosto1
    
    ->
    tämä on tiedosto numero 1
    tämän tiedoston on kirjoittanut nadja


    tekstiä
    tekstiä
    tekstiä




![Näyttökuva 2023-03-13 001552](https://user-images.githubusercontent.com/118609353/224577011-ba10aab4-237d-4eda-a513-bf797d225e0d.png)


    

---
### Komentojen kertaus

Luodaan tiedosto:  

    micro tiedostonnimi
    -> 
    echo "Tervehdys!"
    
Testataan:  

    bash tiedostonnimi

Oikeudet: 

    ls -l tiedostonnimi
    chmod ugo+x tiedostonnimi
    
Tarkistetaan oikeudet:  

    ls -l tiedostonnimi
    
Testataan, että toimii:  

    ./tiedostonnimi
    
Kerrotaan käytettävä komentotulkki:  

    micro tiedostonnimi
    -> 
    #!/usr/bin/bash/ 
    echo "Tervehdys"
    
Testataan:  
    ./tiedostonnimi  
    
Kopioidaan tiedosto:

    sudo cp tiedostonnimi /usr/local/bin/
    
Testataan:  

    tiedostonnimi
    
    
<!-- 
~/. local is an attempt to provide a standard place to store executables and data for applications ported from Linux. -->

---
---

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

 












