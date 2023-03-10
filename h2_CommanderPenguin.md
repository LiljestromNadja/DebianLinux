# Komentorivi
Using the command line

## h2 Komentaja Pingviini 
Näiden harjoitusten avulla on tarkoitus saada näppituntumaa Linuxin komentoriviin.  Tämä tehtävä osa Haaga-Helia ammattikorkeakoulun [Linux-palvelimet -kurssia](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

### Harjoitukset
<!--[Micro-editorin asentaminen](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#micro-editorin-asentaminen)  
[Listaa koneesi rauta](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#listaa-koneesi-rauta)  
[Kolmen komentoriviohjelman asentaminen:](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#kolmen-komentoriviohjelman-asentaminen)  
-[Cowsay](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#cowsay)  
-[Nano](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#nano)  
-[Asciijump](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#asciijump)  
[Important directories](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#important-directories)  
[The Friendly M](https://github.com/LiljestromNadja/DebianLinux/edit/main/h2_CommanderPenguin.md#the-friendly-m) -->  



Micro -editorin asentaminen  
Listaa koneesi rauta  
Kolmen komentoriviohjelman asentaminen:  
-Cowsay  
-Nano  
-Asciijump  
-Useamman ohjelman asentaminen samalla komennolla  
Important directories  
Grep

<br></br>

### Micro-editorin asentaminen
Tehtävä: Asenna komentoriviltä Micro-editori.  

     sudo apt-get install micro
      
      
![Näyttökuva (90)](https://user-images.githubusercontent.com/118609353/213944752-3e46584c-04f2-4b06-b868-ce1be98c5c9b.png)  

     micro newfile.md
     
![Näyttökuva (118)](https://user-images.githubusercontent.com/118609353/214039817-fde5fec9-1957-4294-936b-e576d7d7e4ed.png) 
     
     ^Q poistumiseen

<br></br>

### Listaa koneesi rauta
Tehtävä: Rauta. Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). Asenna lshw tarvittaessa. Selitä ja analysoi listaus.  

      apt-get install lshw
      
![Näyttökuva (87)](https://user-images.githubusercontent.com/118609353/213945161-757920ba-d815-49f6-bf86-e476f0c150ba.png)  

Annetaan käsky hieman painokkaammin:  

      sudo apt-get install lshw

![Näyttökuva (88)](https://user-images.githubusercontent.com/118609353/213945254-2812e97e-357f-4c79-86b1-7cf53426ad6c.png)  

      sudo lshw -short sanitize
      
![Näyttökuva (89)](https://user-images.githubusercontent.com/118609353/213945332-0102753c-0b23-4363-a14e-4d5c75523103.png)  

...ja muistetaan että jokaisella merkillä on merkitys:  
     
     sudo lshw -short -sanitize  
     
![Näyttökuva (117)](https://user-images.githubusercontent.com/118609353/214037645-97b15800-2bd6-4d38-a046-ca98cda1784c.png)


<br></br>

### Kolmen komentoriviohjelman asentaminen
Tehtävä: Apt. Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla? 

##### Cowsay, tervehtivä lehmä

      sudo apt-get update
      sudo apt-get -y install cowsay


![Näyttökuva (100)](https://user-images.githubusercontent.com/118609353/213946654-6e8bb33a-2f0e-4388-95ee-46badef03fca.png)

      cowsay moi linux
      
![Näyttökuva (101)](https://user-images.githubusercontent.com/118609353/213946724-305357f9-0764-4416-a876-00013d687e02.png)  

<br></br>

##### Nano-tekstieditori

      sudo apt-get -y install nano
      
![Näyttökuva (102)](https://user-images.githubusercontent.com/118609353/213946880-e7830406-5bc7-4856-9a2c-8523255f41cd.png)

      nano newfile 
      
![Näyttökuva (103)](https://user-images.githubusercontent.com/118609353/213947372-58fa9cfb-49e2-4354-a879-0aebf1133c08.png)  

     ^X poistumiseen

<br></br>

##### Asciijump-mäkihyppypeli

      sudo apt-get update
      sudo apt-get install asciijump
      
![Näyttökuva (106)](https://user-images.githubusercontent.com/118609353/213948514-bd1bce2a-8496-4528-bd56-75c11e0ea9ca.png)

      asciijump
      
![Näyttökuva (105)](https://user-images.githubusercontent.com/118609353/213948533-10a9d5be-e014-4e22-9b72-e6299333245b.png)

<br></br>

##### Useamman ohjelman asentaminen samalla komennolla  

Poistetaan ensin äskettäin asennettuja ohjelmia, annetaan komennot ja erotellaan ohjelmat välilyönnillä:  

     sudo apt-get -y autoremove --purge asciijump nano micro  
     

![Näyttökuva (123)](https://user-images.githubusercontent.com/118609353/214051983-92a5f270-a4c5-4244-b199-f2e8507ce116.png)

Tämän jälkeen asennus uudelleen:  

     sudo apt-get -y install micro nano asciijump  

![Näyttökuva (122)](https://user-images.githubusercontent.com/118609353/214052462-9ae4566f-4b29-4123-940a-c5c0289ac15b.png)

<br></br>

### Important Directories 
Tehtävä: FHS. Esittele kansiot, jotka on listattu "Command Line Basics Revisited" kappaleessa "Important directories". Näytä kuvaava esimerkki kunkin tärkeän kansion sisältämästä tiedostosta tai kansiosta. Jos kyseessä on tiedosto, näytä siitä kuvaava esimerkkirivi. Työskentele komentokehotteessa ja näytä komennot, joilla etsit esimerkit.  

/ Root Directory  
![Näyttökuva (109)](https://user-images.githubusercontent.com/118609353/213950902-c3658e08-f11e-4fa9-9099-542150811d69.png)  
/home/  
![Näyttökuva (110)](https://user-images.githubusercontent.com/118609353/213951050-fa9416e7-3c37-4deb-932b-cf358e06c75f.png)

/home/nadja/  
![Näyttökuva (111)](https://user-images.githubusercontent.com/118609353/213951165-5cf0a7e2-044f-4924-837b-0b81a3eb3aef.png)

/etc/  
![Näyttökuva (112)](https://user-images.githubusercontent.com/118609353/213951439-dd134a08-09c7-4a7e-9fa1-edb8732f15ce.png)

/media/  
![Näyttökuva (113)](https://user-images.githubusercontent.com/118609353/213951578-dd073081-764a-484d-987e-e453a87ecdc2.png)

/var/log/  
![Näyttökuva (115)](https://user-images.githubusercontent.com/118609353/213951818-1aef2b27-495c-4e23-b793-8434dd207498.png)





<br></br>
### Grep  
Tehtävä: The Friendly M. Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta.  

Komento, jolla saa grepin manuaalin:  

     man grep
     
![Näyttökuva (124)](https://user-images.githubusercontent.com/118609353/214125521-462d9cf7-0dc4-45da-9a47-3fd4a40ec618.png)  

Idea on siis:  

     grep [OPTION]... PATTERNS [FILE]
     

![Näyttökuva (125)](https://user-images.githubusercontent.com/118609353/214126628-2e88f5f2-af3b-4a98-9b0f-4661203eb9b6.png)


Kokeilin seuraavasti:    

     grep -H 'and so is' newfile.md anothernewfile.md  
    
![Näyttökuva (126)](https://user-images.githubusercontent.com/118609353/214127677-477cb9ee-5ee1-4b55-a370-55c2720a051e.png)  

     grep -i 'and so is' newfile.md anothernewfile.md  
     
![Näyttökuva (127)](https://user-images.githubusercontent.com/118609353/214128941-d4131384-8d0a-436c-87a5-704faddb770c.png)
![Näyttökuva (129)](https://user-images.githubusercontent.com/118609353/214129614-f90f7b06-b972-41e6-b8ba-644a6312bc9f.png)  

Poistin tiedostosta anothernewfile.md pienellä kirjoitetun "and so is" -tekstin ja kokeilin uudelleen:  

     grep -H 'and so is' newfile.md anothernewfile.md 
     
![Näyttökuva (130)](https://user-images.githubusercontent.com/118609353/214130480-7f0f19bc-cebe-4149-89af-aeb5c8329698.png)



     

      






#### Lähteet:  
Karvinen, Tero: [Linux Palvelimet 2023 alkukevät](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).  
Karvinen, Tero: [Command Line Basics Revisited](https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited), 2020.  
Karvinen, Tero: [Command Line Basics](https://terokarvinen.com/2009/command-line-basics-4/), 2009.  
Karvinen, Tero: [Commands for Admin](https://terokarvinen.com/2008/commands-for-admin-4/), 2008.  
Installati.one: [How To Install cowsay on Debian](https://installati.one/debian/10/cowsay/).  
Installati.one: [Debian10](https://installati.one/debian/10/).




