# h6_Based

Tehtävänanto:  

x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)  
[Apache Software Foundation 2023: Getting Started](https://httpd.apache.org/docs/2.4/getting-started.html)  
[Apache Software Foundation 2023: Name-based Virtual Host Support](https://httpd.apache.org/docs/current/vhosts/name-based.html)  
a) Vaihda Apachelle uusi etusivu. Varmista, että voit muokata sivua normaalilla käyttäjällä (ilman sudoa).  
b) Tee Apachen asetustiedostoon kirjoitusvirhe. Etsi se työkalujen avulla. Vertaa 'apache2ctl configtest' ja virhelokin /var/log/apache2/error.log virheilmoituksia.  
n) Vapaaehtoinen: Tee Apachelle kaksi nimipohjaista palvelua (name based virtual host), foo.example.com ja bar.example.com. Voit simuloida nimipalvelun toimintaa hosts-tiedoston avulla.  


### x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)  

Getting Started  

- Netissä URL-osoite sisältää: 
    - protokollan (http)  
    - palvelimen nimen (www.something.com)  
    - URL-polun (/public_sites/index.html)  
    - mahdollisesti  palvelimelle lähetettävää tietoa (?name=Pentti&ika=12)  
- Yhteys esimerkiksi Internet-selaimesta (client) palvelimeen (esim. Apache) muodostetaan pyynnöllä (request). 
- Palvelin vastaa pyyntöön (response) tunnuksella (esim. 404 client error), joka kertoo onko yhteyden muodostaminen onnistunut vai ei.  
- Mikäli yhteyden muodostamisessa on tapahtunut virhe, virheen tyyppi selviää tästä tunnuksesta (status code).  
- Tapahtumat, esimerkiksi virheet kirjataan lokiin.  
 
- Jotta yhteys voidaan muodostaa, palvelimen nimellä täytyy olla IP-osoite, joka on sen "sijainti" Internetissä.  
- Useampi hostname voi osoittaa samaan IP-osoitteeseen.  
- Useampi IP-osoite voi sijaita samalla palvelinlaitteella.  

- Apache on määritelty yksinkertaisilla tekstitiedostoilla.  
- Näiden asetuksia määrittelevien tiedostojen sisältö on jaettu useampaan pieneen tiedostoon hallinnan helpottamiseksi.  

- Nettisivujen sisältö voidaan jakaa karkeasti staattiseen (esim. html-, kuva- ja css-tiedostot) ja dynaamiseen sisältöön (generoidaan pyyntöä vastaanotettaessa).  

- Järjestelmänvalvojan "arvokkainta omaisuutta" ovat lokitiedostot, erityisesti virheloki. Vianetsintää ilman virhelokia verrataan ajamiseen silmät kiinni.  
- Virhelokin merkinnöistä käy ilmi, missä ja milloin virhe on tapahtunut, sekä mahdollisesti toimet virheen korjaamiseksi. 

**Lähteet**  
[Apache Software Foundation 2023: Getting Started](https://httpd.apache.org/docs/2.4/getting-started.html)  
[Apache Software Foundation 2023: Name-based Virtual Host Support](https://httpd.apache.org/docs/current/vhosts/name-based.html)  
 
### a) Vaihda Apachelle uusi etusivu. Varmista, että voit muokata sivua normaalilla käyttäjällä (ilman sudoa).  

Katsotaan missä tilassa Apache on:  
    
        $ sudo service apache2 status  
        
![Näyttökuva (170) sudo service apache2 status](https://user-images.githubusercontent.com/118609353/216847206-edf779b2-d0d5-4377-bf45-5700ec2929dd.png)  

**Apachen etusivun vaihtaminen**

**Sudona:**  

        $ sudoedit /etc/apache2/sites-available/frontpage.conf  
        
![Näyttökuva (171) sudoedit etcapache2sites-availablefrontpageconf](https://user-images.githubusercontent.com/118609353/216847291-e45f354c-0061-4d86-b724-e8bb90ab7d64.png)  

![Näyttökuva (172) frontpageconftiedostonäkymä](https://user-images.githubusercontent.com/118609353/216847342-38f8d954-7750-4787-9ba8-a72aa161f597.png)  

        cat /etc/apache2/sites-available/frontpage.conf  
        

        <VirtualHost *:80>
                DocumentRoot /home/nadja/public_sites/
                <Directory /home/nadja/public_sites/>
                        require all granted
                </Directory>
        </VirtualHost>  
        
 
a2ensite ja a2dissite manuaalissa:  

        man a2ensite  
                
        "a2ensite  is a script that enables the specified site (which contains a
       <VirtualHost> block) within the apache2 configuration.  It does this by
       creating  symlinks within /etc/apache2/sites-enabled.  Likewise, a2dis‐
       site disables a site by removing those symlinks.  It is not an error to
       enable  a site which is already enabled, or to disable one which is al‐
       ready disabled."   
       
<br></br>

        $ sudo a2ensite frontpage.conf  
        
![Näyttökuva (173) sudo a2ensite frontpageconf](https://user-images.githubusercontent.com/118609353/216847605-1a20218f-b1c4-4cfa-abce-42ce6874cfd2.png)

        $ sudo a2dissite 000-default.conf  
        
![Näyttökuva (174) sudo a2dissite 000-defaultconf](https://user-images.githubusercontent.com/118609353/216847621-f1af1769-b899-452d-ace6-04d6c929421b.png)

Käynnistetään Apache uudelleen:  
    
        $ sudo systemctl restart apache2.service

**Käyttäjänä**  

        cd 
        mkdir public_sites
        micro index.html   
        
![Näyttökuva (175) public_sites_indexhtml_muokataan_ilman sudoa](https://user-images.githubusercontent.com/118609353/216847682-6b770862-99c0-4b82-9d63-2d0984357f17.png)  

### b) Tee Apachen asetustiedostoon kirjoitusvirhe. Etsi se työkalujen avulla. Vertaa 'apache2ctl configtest' ja virhelokin /var/log/apache2/error.log virheilmoituksia.  

**Vianselvitykseen:**

        /usr/sbin/apache2ctl configtest
     
 ![Näyttökuva (176) usrsbinapache2ctl configtest](https://user-images.githubusercontent.com/118609353/216848396-d4452dd8-f639-4b58-b531-61b239d4176d.png)  
 
 ja  

        $ sudo tail -1 /var/log/apache2/error.log  
        
![Näyttökuva (183) apachekaynnissa ei erroria](https://user-images.githubusercontent.com/118609353/216848804-21f36b9a-da74-4dd0-a524-c527cf4368d6.png)  
        
Käynnistän Apachen uudelleen:  

        $ sudo systemctl restart apache2.service  
        

![Näyttökuva (184) apache kaynnistetty uudelleen joku error](https://user-images.githubusercontent.com/118609353/216848959-b6d0e8c2-112e-4f44-a73a-128e682ae623.png)  


Käydään kurkkaamassa  /etc/apache/apache2.conf ja samalla aiheutetaan virhe:

        nadja@debbiedebian:/etc/apache2$ sudo nano apache2.conf  
        
        CTRL + SHIFT + _ , line: 80  
        
        
        DefaultRuntimeDir ${APACHE_RUN_DIR}
        ->
        merkitään kommentiksi
        #DefaultRuntimeDir ${APACHE_RUN_DIR}

Tallennetaan 18.45.  

        $ sudo tail -5 /var/log/apache2/error.log | grep '/usr/sbin/apache2' --color

Ei näy vielä mitään, käynnistetäään apache uudestaan:  

        $ sudo systemctl restart apache2.service

...ja kokeillaan uudestaan:  

        $ sudo tail -5 /var/log/apache2/error.log | grep '/usr/sbin/apache2' --color  

sekä  

        $ '/usr/sbin/apache2'  


![Näyttökuva (179) uusi error apache run dir kommentiksi](https://user-images.githubusercontent.com/118609353/216849315-d4a4752a-6a38-4d9b-a4c2-19a2774e740e.png)  


Lähdetään palauttamaan:   

        $ sudo nano apache2.conf

        #DefaultRuntimeDir ${APACHE_RUN_DIR}
        ->
        DefaultRuntimeDir ${APACHE_RUN_DIR}

Tallennetaan. (18.5jotain)  

        sudo tail -5 /var/log/apache2/error.log | grep '/usr/sbin/apache2' --color

Ei näy kuin edellinen 18.47 error. Käynnistetäään siis Apache uudelleen:  

        sudo systemctl restart apache2.service

        sudo tail -5 /var/log/apache2/error.log | grep '/usr/sbin/apache2' --color  
        

![Näyttökuva (180) korjataan virhe otetaan kommenttimerkintä poist](https://user-images.githubusercontent.com/118609353/216849456-959ca8fd-e3c2-4a06-a711-5939fb7e00b3.png)

![Näyttökuva (181) aiheuttamani errorit korjattu](https://user-images.githubusercontent.com/118609353/216849486-605d0455-7850-4fa8-acbc-afedc6d33d50.png)  

Käynnistettään apache taas uudestaan 19.11 ja 19.12.  
    
        sudo systemctl restart apache2.service

        sudo tail -5 /var/log/apache2/error.log | grep '/usr/sbin/apache2' --color
        
        
![Näyttökuva (182) käynnistin apachen 2 kertaa uusiks sama ilmoitus tuli](https://user-images.githubusercontent.com/118609353/216849678-7d07eb54-6eb2-4f55-8567-4ae03e3fc61c.png)

Tämä error kirjataan Apachen uudelleenkäynnistyksen yhteydessä. "Config variable ${APACHE_RUN_DIR} is not defined", liittynee jonkin ajonaikaisen hakemiston määrittelyyn. 
"The directory where shm and other runtime files will be stored."




### n) Vapaaehtoinen: Tee Apachelle kaksi nimipohjaista palvelua (name based virtual host), foo.example.com ja bar.example.com. Voit simuloida nimipalvelun toimintaa hosts-tiedoston avulla.  
  





<br></br> 

**Muistilista**  

Apache kill, start, restart:  

        $ sudo systemctl stop apache2.service
        $ sudo systemctl start apache2.service
        $ sudo systemctl restart apache2.service

Apache status:  

        $ sudo service apache2 status 

Käyttäjän tarkistaminen:  

        $ whoami

Error.logissa hamuiluun:  

        $ sudo tail -5 /var/log/apache2/error.log | grep '/usr/sbin/apache2' --color

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  


[Apache Software Foundation 2023: Getting Started](https://httpd.apache.org/docs/2.4/getting-started.html)  
[Apache Software Foundation 2023: Name-based Virtual Host Support](https://httpd.apache.org/docs/current/vhosts/name-based.html)  









