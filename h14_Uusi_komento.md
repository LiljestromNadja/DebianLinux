

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

    
    


    




    


    


---

### b) b) Tee Linuxiin uusi komento Pythonilla. Komennon tulee toimia kaikilla käyttäjillä, työhakemistosta riippumatta.  

---
### c) Tee Linuxiin komento, joka tekee jotain monelle tiedostolle  

---
---

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

 












