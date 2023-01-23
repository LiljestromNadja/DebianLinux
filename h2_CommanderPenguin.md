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
Important directories  

<br></br>

### Micro-editorin asentaminen
Tehtävä: Asenna komentoriviltä Micro-editori.  

     sudo apt-get install micro
      
      
![Näyttökuva (90)](https://user-images.githubusercontent.com/118609353/213944752-3e46584c-04f2-4b06-b868-ce1be98c5c9b.png)  
<br></br>

### Listaa koneesi rauta
Tehtävä: Rauta. Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). Asenna lshw tarvittaessa. Selitä ja analysoi listaus.  

      apt-get install lshw
      
![Näyttökuva (87)](https://user-images.githubusercontent.com/118609353/213945161-757920ba-d815-49f6-bf86-e476f0c150ba.png)

      sudo apt-get install lshw

![Näyttökuva (88)](https://user-images.githubusercontent.com/118609353/213945254-2812e97e-357f-4c79-86b1-7cf53426ad6c.png)

      sudo lshw -short sanitize
      
![Näyttökuva (89)](https://user-images.githubusercontent.com/118609353/213945332-0102753c-0b23-4363-a14e-4d5c75523103.png)  

<br></br>

### Kolmen komentoriviohjelman asentaminen
Tehtävä: Apt. Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla? 

##### Cowsay

      sudo apt-get update
      sudo apt-get -y install cowsay


![Näyttökuva (100)](https://user-images.githubusercontent.com/118609353/213946654-6e8bb33a-2f0e-4388-95ee-46badef03fca.png)

      cowsay moi linux
      
![Näyttökuva (101)](https://user-images.githubusercontent.com/118609353/213946724-305357f9-0764-4416-a876-00013d687e02.png)  

<br></br>

##### Nano

      sudo apt-get -y install nano
      
![Näyttökuva (102)](https://user-images.githubusercontent.com/118609353/213946880-e7830406-5bc7-4856-9a2c-8523255f41cd.png)

      nano newfile 
      
![Näyttökuva (103)](https://user-images.githubusercontent.com/118609353/213947372-58fa9cfb-49e2-4354-a879-0aebf1133c08.png)  

<br></br>

##### Asciijump

      sudo apt-get update
      sudo apt-get install asciijump
      
![Näyttökuva (106)](https://user-images.githubusercontent.com/118609353/213948514-bd1bce2a-8496-4528-bd56-75c11e0ea9ca.png)

      asciijump
      
![Näyttökuva (105)](https://user-images.githubusercontent.com/118609353/213948533-10a9d5be-e014-4e22-9b72-e6299333245b.png)

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
<!--### The Friendly M
Tehtävä: The Friendly M. Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta.  -->

      






#### Lähteet:  
Karvinen, Tero: [Linux Palvelimet 2023 alkukevät](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).  
Karvinen, Tero: [Command Line Basics Revisited](https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited), 2020.  
Karvinen, Tero: [Command Line Basics](https://terokarvinen.com/2009/command-line-basics-4/), 2009.  
Karvinen, Tero: [Commands for Admin](https://terokarvinen.com/2008/commands-for-admin-4/), 2008.  
Installati.one: [How To Install cowsay on Debian](https://installati.one/debian/10/cowsay/).  
Installati.one: [Debian10](https://installati.one/debian/10/).




