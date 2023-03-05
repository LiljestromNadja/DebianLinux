

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

(20:55):  

	nadja@debian:~/publicwsgi$ chmod ugo-rwx nlilj/

Selaimessa 'localhost/admin':  

![Näyttökuva 2023-03-05 205538](https://user-images.githubusercontent.com/118609353/222980153-8bcc1d8c-1383-4cfb-91b2-010c2918c2e5.png)  

Apachen error log:  

	nadja@debian:~$ sudo tail -F /var/log/apache2/error.log

![Näyttökuva 2023-03-05 205836](https://user-images.githubusercontent.com/118609353/222980277-f003a186-6ceb-4903-a275-aca7f38ae5e4.png)



Palautetaan äskeinen, toimiva tila:  

	nadja@debian:~/publicwsgi$ chmod ugo+wx nlilj/
	
<!-- 
en ottanut selkoa:  
 	
	nadja@debian:~/publicwsgi$ chmod u+rx nlilj/-->


---

### d) Kirjoitusvirhe Apachen asetustiedostossa (/etc/apache2/sites-available/terokarvinen.conf tms)  

Mennään kansioon /etc/apache2/sites-available/:  

	nadja@debian:~$ cd  /etc/apache2/sites-available/
	nadja@debian:/etc/apache2/sites-available$ ls
	
	nadja@debian:/etc/apache2/sites-available$ micro djfrontpage.conf 
	
![Näyttökuva 2023-03-05 182408](https://user-images.githubusercontent.com/118609353/222972820-0a7c5be6-5438-4ab7-a763-6bcd4b2865b9.png)


Muutetaan tätä kohtaa:  
	
	Define TDIR /home/nadja/publicwsgi/nlilj
	
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

Apachen error log:  

![Näyttökuva 2023-03-05 191951](https://user-images.githubusercontent.com/118609353/222975694-66ee27c0-d176-4c97-a12e-be4f3e433fe5.png)


![Näyttökuva 2023-03-05 191917](https://user-images.githubusercontent.com/118609353/222975700-698fcb73-85e6-4057-9f57-74c6fd49b77f.png)

ModuleNotFoundError: No module named 'nlilj.settings', eli kyseisen nimistä moduulia ei löydy.  

Korjataan tilanne:  

	nadja@debian:/etc/apache2/sites-available$ micro djfrontpage.conf 
	
	Define TDIR /home/nadja/publicwsgi
	
	-> 
	
	Define TDIR /home/nadja/publicwsgi/nlilj  

Käynnistetään Apache uudelleen (19:26):  

	nadja@debian:/etc/apache2/sites-available$ sudo systemctl restart apache2  
	
Mennään selaimeen 'localhost/admin/':  	

![Näyttökuva 2023-03-05 192752](https://user-images.githubusercontent.com/118609353/222976065-16c86a2a-7ae7-4ecd-9557-6a6110ff7d87.png)

	



---

### e) Apachen WSGI-moduli puuttuu ('sudo apt-get purge libapache2-mod-wsgi-py3' tms)  

Poistetaan (20:28):  

	nadja@debian:~$ sudo apt-get purge libapache2-mod-wsgi-py3   
	
Käynnistetään Apache uudelleen(20:27):  

	nadja@debian:~$ sudo systemctl restart apache2

Heti tuli viesti:  

![Näyttökuva 2023-03-05 202816](https://user-images.githubusercontent.com/118609353/222978836-5bf77172-45a7-4974-93bb-39232bbc30a9.png)

	nadja@debian:~$ /sbin/apache2ctl configtest  
	

![Näyttökuva 2023-03-05 203011](https://user-images.githubusercontent.com/118609353/222978924-0540b74a-1564-4671-a167-5c672eb3eb37.png)


Korjataan äsken aiheutettu error (20:33):  

	nadja@debian:~$ sudo apt-get install libapache2-mod-wsgi-py3  
	
Käynnistetään Apache uudelleen(20:35):  

	nadja@debian:~$ sudo systemctl restart apache2  
	
	nadja@debian:~$ /sbin/apache2ctl configtest  

![Näyttökuva 2023-03-05 203718](https://user-images.githubusercontent.com/118609353/222979257-39fa18e3-6a25-4cfd-a3cc-01dbabbfba90.png)


	


	




---

### f) Väärät domain-nimet ALLOWED_HOSTS-kohdassa (settings.py, ja DEBUG=False)  

---

Mennään tiedostoon **settings.py**:  

	nadja@debian:~/publicwsgi/nlilj/nlilj$ micro settings.py 

Muokataan kohtaa ALLOWED_HOSTS :  
	
	DEBUG = False
	ALLOWED_HOSTS = ['localhost']
	
	-> 
	
	DEBUG = False
	ALLOWED_HOSTS = []
	

![Näyttökuva 2023-03-05 204351](https://user-images.githubusercontent.com/118609353/222979552-416e303f-94dd-49cc-9691-8a2b6b273ea4.png)  

Selain 'localhost/admin/':  


![Näyttökuva 2023-03-05 204615](https://user-images.githubusercontent.com/118609353/222979687-e5a9018a-def4-4a86-90a3-98015ef01852.png)  

Kokeillaan testipalvelinta:  

	(env) nadja@debian:~/publicwsgi/nlilj$ ./manage.py runserver

Saadaan viesti:  

![Näyttökuva 2023-03-05 204900](https://user-images.githubusercontent.com/118609353/222979807-30e08818-e7fe-4e74-90f0-675442caedba.png)

Korjataan error:  

	nadja@debian:~/publicwsgi/nlilj/nlilj$ micro settings.py 

Muokataan kohtaa ALLOWED_HOSTS :  
	
	DEBUG = False
	ALLOWED_HOSTS = []
	
	-> 
	
	DEBUG = False
	ALLOWED_HOSTS = ['localhost']

 

---

  

	
	



---
---

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  












