# Apache 2.4 palvelinohjelman asennus 

Installing Apache HTTP Server Version 2.4

### Asennus

Tarkistetaan päivitykset:  

    sudo apt-get update  
    
![Näyttökuva (140) apache](https://user-images.githubusercontent.com/118609353/215133885-125686e4-6c37-4763-9dcd-2e1db324db9f.png)

Asennetaan Apache:  

    sudo apt-get install apache2  
    
![Näyttökuva (141) Apache 2](https://user-images.githubusercontent.com/118609353/215134354-644f6649-a27b-4852-b7e8-943e9a810f98.png)

    
Palomuuri, jos sitä ei ole jo asennettu:  

    sudo apt-get install ufw
    
    
Käynnistetään Apache:  

    sudo systemctl start apache2.service
    
Tarkistetaan toimiiko:  

    sudo service apache2 status  
    
![Näyttökuva (146) Apache 7 kaynnistysjatarkistus](https://user-images.githubusercontent.com/118609353/215133585-83120211-8fe6-4f58-a64d-98405764505a.png)

    
Localhost -sivu selaimessa:  
    
    
    
![Näyttökuva (147) Apache8 localhost](https://user-images.githubusercontent.com/118609353/215133158-a5db380d-708f-440b-9131-dac91b14b6da.png)

    
<br></br>  
<br></br>  

### Testailua   

![Näyttökuva (145) Apache 6 httpdeny](https://user-images.githubusercontent.com/118609353/215134817-f9dfaa1f-82f5-4f0d-94aa-570018b01323.png)

##### Sallitaan http-portti 80 (localhost)

    sudo ufw allow http
    
Tarkistetaan, onnistuiko tämä:  

    sudo ufw status    
    
##### sudo ufw allow -komennon kumoaminen ja tarkistus:  

    sudo ufw deny http
    sudo ufw status

<br></br>
<br></br>
# Käyttöönotto  

Linux-palvelimet tunnilla 31.01.2023.  


Kun Apache2 on asennettu, käynnistetään se:  

      $ sudo systemctl start apache2  
      
Tarkistetaan:  

      $ sudo service apache2 status  
      

 ![Näyttökuva (154)](https://user-images.githubusercontent.com/118609353/215799847-d3cf079f-d43d-4526-b8f4-b5223b600a41.png)

Siirrytään kotihakemistoon:   

        $ cd  
        
        $ pwd
    
![Näyttökuva (155)](https://user-images.githubusercontent.com/118609353/215800969-dbd7bec1-cbe1-48a1-8ce0-8fbfe10cf6af.png)  

        $ echo "Moi"|sudo tee /var/www/html/index.html
        
 Testataan:  
  
        $ curl 'http://localhost'  
        
![Näyttökuva (168) localhostRootIndexHtml](https://user-images.githubusercontent.com/118609353/216348596-c5d6c01f-8bc8-4a60-94bd-5bcf985e2442.png)

        
Annetaan komento "a2enmod userdir" ja käynnistetään Apache2 uudelleen:  

        $ sudo a2enmod userdir  
        
        $ sudo systemctl restart apache2
        
Ja hakemisto, missä tällä hetkellä ollaan on siis kotihakemisto, /home/nadja. 

        $ mkdir public_html
        $ cd public_html
        $ ls
        $ micro index.html
        $ nano toinensivu.html
        
        $ curl 'http://localhost/~nadja' 
        
        
        
Katsotaan vielä Mozilla Firefoxilla, toimiiko.  
http://localhost/~nadja (index.html)  
http://localhost/~nadja/toinensivu (toinensivu.html)  

![Näyttökuva (156)](https://user-images.githubusercontent.com/118609353/215804575-7d51bc69-6c4b-4a22-92b0-9926adda6716.png)


Bonus, lisätään testikäyttäjä: 

        $ sudo adduser debbie01  
        
Käyttäjänhallintakomennot:  

Lisääminen:  

        $ sudo adduser userAbc
        
Poistaminen:  
        
        $ sudo deluser userAbc
        
 
 
 
 
<br></br>
<br></br>
# Apache2 asennuksen poistaminen  

        $ sudo apt-get purge apache2 apache2-bin  
        $ sudo systemctl stop apache2




##### Materiaalia: 

[Apache HTTP Server Project - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/)  

Apachen asennusta käsitellään [Tero Karvisen Linux-palvelimet alkukevät 2023 -kurssilla](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

    
    
