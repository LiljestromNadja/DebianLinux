

# h12_Vianselvitys

**Tehtävänanto**  
Haasteita horisontissa. Tutki ongelmia Djangon tuotantotyyppisessä asennuksessa:  

- Aiheuta ongelma  
- Näytä oireet (esim. selaimella)  
- Etsi siihen liittyvät lokimerkinnät  
- Analysoi lokimerkinnät (eli selitä perusteellisesti, mitä eri kohdat tarkoittavat ja mitä kohdista on pääteltävissä)  
- Korjaa ongelma  
- Osoita testillä, että vika on korjattu  


**Tutkittavat ongelmat:**  

a) Kirjoitusvirhe Python-tiedostossa  
b) Django-projektikansio väärässä paikassa (siis se, jossa on manage.py)  
c) Projektikansiolla väärät oikeudet ('chmod ugo-rwx teroco/', 'chmod u+rx teroco/')  
d) Kirjoitusvirhe Apachen asetustiedostossa (/etc/apache2/sites-available/terokarvinen.conf tms)  
e) Apachen WSGI-moduli puuttuu ('sudo apt-get purge libapache2-mod-wsgi-py3' tms)  
f) Väärät domain-nimet ALLOWED_HOSTS-kohdassa (settings.py, ja DEBUG=False)  
e) Vapaaehtoinen bonus: oma, itse keksitty ongelma.  

**Vinkit**  

- Aloita toimivasta tilanteesta. Silloin tiedät, ettei asennuksessa ole muita ongelmia kuin ne, joita olet itse aiheuttanut.  
- 'sudo tail -F /var/log/apache2/access.log /var/log/apache2/error.log /var/log/apache2/other_vhost.log'
  - ja tähän voi lätkiä rivinvaihtoja, niin erottaa, mitkä rivit tulevat mistäkin sivunlatauksesta  
- '/sbin/apache2ctl configtest'  
- 'sudo systemctl status apache2'  


---

### Alkutilanne  

Djangon tuotantoasennus tehty [edellisessä harjoituksessa](https://github.com/LiljestromNadja/DebianLinux/blob/main/h11_Prod.md). 

---
## Tehtävät  

### a) Kirjoitusvirhe Python-tiedostossa   

Mennään tiedostoon **settings.py**:  

    nadja@debian:~/publicwsgi/nlilj/nlilj$ micro settings.py

Merkitään tiedostossa **settings.py** kommentiksi:   

    #STATIC_ROOT = os.path.join(BASE_DIR, 'static/')  
    
![Näyttökuva 2023-03-05 161044](https://user-images.githubusercontent.com/118609353/222965928-412b4134-9aad-4a3c-8e1a-f5562b6f9894.png)


Aktivoidaan virtual env:  

    nadja@debian:~/publicwsgi$ source env/bin/activate  
    
Siirrytään kansioon, jossa **manage.py** -tiedosto:  

    
    (env) nadja@debian:~/publicwsgi$ ls
    (env) nadja@debian:~/publicwsgi$ cd nlilj/  
    
Ajetaan komento:  

    (env) nadja@debian:~/publicwsgi/nlilj$ ./manage.py collectstatic  
    

![Näyttökuva 2023-03-05 162043](https://user-images.githubusercontent.com/118609353/222966206-7e1fa4f9-4a6f-4f7d-8fdb-3a365ecc72ee.png)

Jolloin saadaan seuraava ilmoitus joka kertoo virheen tyypistä 'ImproperlyConfigured' sekä mistä virheilmoitus aiheutui 'You're using the staticfiles app without having set the STATIC_ROOT setting to a filesystem path':  

![Näyttökuva 2023-03-05 162805](https://user-images.githubusercontent.com/118609353/222966698-1866ee9a-1626-4855-b75f-61ed8c375e89.png)

Tilanteen korjaaminen:  

    nadja@debian:~/publicwsgi/nlilj/nlilj$ micro settings.py
    
Poistetaan kommenttimerkintä:  

    STATIC_ROOT = os.path.join(BASE_DIR, 'static/')  
    
Ajetaan komento:  

    (env) nadja@debian:~/publicwsgi/nlilj$ ./manage.py collectstatic  
    
    

![Näyttökuva 2023-03-05 164039](https://user-images.githubusercontent.com/118609353/222969985-c3f45a9f-81d1-4ba6-b01c-ae1e4f55c0fd.png)


<!-- 
#### väliotsikko 
-->

---

### b) Django-projektikansio väärässä paikassa (siis se, jossa on manage.py)  

Kopioidaan **nlilj** kansio eri paikkaan:  

    nadja@debian:~/publicwsgi$ cp -r nlilj/ /home/nadja
    
Tarkistetaan että kopio on olemassa ja meni sinne minne oli tarkoitus:  

    nadja@debian:~/publicwsgi$ cd ..   
    nadja@debian:~$ ls  
    
    nadja@debian:~$ cd nlilj/  
    nadja@debian:~/nlilj$ ls  


![Näyttökuva 2023-03-05 170534](https://user-images.githubusercontent.com/118609353/222970214-d4c162ee-0e67-43b8-a06f-c139d0f90a39.png)

Mennään takaisin **publicwsgi** -kansioon ja poistetaan **nlilj** -kansio (klo 17:13) josta äsken tehtiin kopio:  

     nadja@debian:~/nlilj$ cd ..  
     nadja@debian:~$ ls  
     nadja@debian:~$ cd publicwsgi/  
     nadja@debian:~/publicwsgi$ ls  
     
     nadja@debian:~/publicwsgi$ rm -r nlilj/  
     nadja@debian:~/publicwsgi$ ls  
     
     
![Näyttökuva 2023-03-05 171307](https://user-images.githubusercontent.com/118609353/222969017-654ea2da-f2d4-45c6-85d1-24a430341bdd.png)  

Avaan selaimen ja osoitteen 'localhost/admin/' ja saan ilmoituksen '403 forbidden':  


![Näyttökuva 2023-03-05 171458](https://user-images.githubusercontent.com/118609353/222970275-9ba1a7e3-c8dc-441d-99a8-7730bf538079.png)

Komentorivillä:   

    nadja@debian:~$ sudo tail -F /var/log/apache2/error.log


![Näyttökuva 2023-03-05 172606](https://user-images.githubusercontent.com/118609353/222969744-7874ae72-d472-4d06-b8bc-d7db38a82c7a.png)  

Menen vielä sijaintiin, missä **manage.py** -tiedosto tällä hetkellä on ja kokeilen:  

	(env) nadja@debian:~/nlilj$ ./manage.py runserver  
	
![Näyttökuva 2023-03-05 174353](https://user-images.githubusercontent.com/118609353/222970654-b810dcf0-be80-4a90-b3ac-3cd863c96e22.png)


Korjataan tilanne, kopioidaan **nlilj** -kansio takaisin kansioon **publicwsgi**:  

	nadja@debian:~$ ls  

	
	nadja@debian:~$ cp -r nlilj/ publicwsgi/  
	
	nadja@debian:~$ cd publicwsgi/  
	nadja@debian:~/publicwsgi$ ls  

	

![Näyttökuva 2023-03-05 174929](https://user-images.githubusercontent.com/118609353/222970926-f4434d6c-d19b-4f2f-9e76-f753e57401f6.png)

Poistetaan vielä **nlilj** -kansio sijainnista /home/nadja:  

	nadja@debian:~$ rm -r nlilj/


![Näyttökuva 2023-03-05 175208](https://user-images.githubusercontent.com/118609353/222971093-8cf1d524-b820-4ed8-a0fb-e766d205d6e9.png)  

Kokeillaan selaimessa 'localhost/admin/':  

![Näyttökuva 2023-03-05 175557](https://user-images.githubusercontent.com/118609353/222971272-27b90db2-9613-403c-9722-e0bf54b01056.png)


	



     
     

     

    

---

### c) Projektikansiolla väärät oikeudet ('chmod ugo-rwx teroco/', 'chmod u+rx teroco/')  

---

### d) Kirjoitusvirhe Apachen asetustiedostossa (/etc/apache2/sites-available/terokarvinen.conf tms)  

Mennään kansioon /etc/apache2/sites-available/:  

	nadja@debian:~$ cd  /etc/apache2/sites-available/
	nadja@debian:/etc/apache2/sites-available$ ls
	
	nadja@debian:/etc/apache2/sites-available$ micro djfrontpage.conf 
	
![Näyttökuva 2023-03-05 182408](https://user-images.githubusercontent.com/118609353/222972820-0a7c5be6-5438-4ab7-a763-6bcd4b2865b9.png)


Muutetaan tätä kohtaa:  
	
	Define TDIR /home/nadja/publicwsgi/nlil
	
	-> 
	
	Define TDIR /home/nadja/publicwsgi  
	
	
Käynnistetään Apache uudelleen (19:04):  

	nadja@debian:/etc/apache2/sites-available$ sudo systemctl restart apache2
	

Mennään Apachen error logiin:  

	nadja@debian:~$ sudo tail -F /var/log/apache2/error.log


![Näyttökuva 2023-03-05 190555](https://user-images.githubusercontent.com/118609353/222975032-911cd7a4-0f30-4693-83ed-32804fa5e023.png)

Virheilmoituksesta käy ilmi, että 'APACHE_RUN_DIR' on määrittelemättä, sekä miten tilanne korjataan. 

Mennään vielä selaimeen 'localhost' (19:12) ja 'localhost/admin' (19:13):  


![Näyttökuva 2023-03-05 191540](https://user-images.githubusercontent.com/118609353/222975495-35829c67-7a58-4542-9e48-d930b1d5f758.png)




---

### e) Apachen WSGI-moduli puuttuu ('sudo apt-get purge libapache2-mod-wsgi-py3' tms)  

---

### f) Väärät domain-nimet ALLOWED_HOSTS-kohdassa (settings.py, ja DEBUG=False)  

---

### e) Vapaaehtoinen bonus: oma, itse keksitty ongelma.  

---

  

	
	



---
---

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

[Karvinen 2022: Deploy Django 4 - Production Install](https://terokarvinen.com/2022/deploy-django/)  
[Django Documentation - How to manage static files (e.g. images, JavaScript, CSS)](https://docs.djangoproject.com/en/4.1/howto/static-files/)  


<!--- 
https://www.digitalocean.com/community/tutorials/how-to-install-django-and-set-up-a-development-environment-on-ubuntu-22-04
---
--->











