

# h10_DJ_Ango  

**Tehtävänanto**  

a) Kannattavaa. Tee oma tietokantasovellus. jossa on weppiliittymä. Kirjautuneet käyttäjät saavat lisätä, muokata ja poistaa tietueita. (Voit käyttää Djangon kehityspalvelinta. Tee jotain muuta kuin asiakastietokanta.)  
b) Vapaaehtoinen: Suhde. Tee monesta yhteen -suhde (many-to-one relationship) kahden taulun välille. Esim. Yksi yritys - monta työntekijää.  

**Vinkit:**

- [Karvinen 2022: Django 4 Instant Customer Database Tutorial](https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django)  
- Djangon testipalvelinta ei saa laittaa Internetiin näkyviin. Eli './manage.py runserver' ei sovi tuotantoon.  
- Tuotantoasennus tehdään Apachen ja mod_wsgi:n kanssa, mutta sitä ei tarvita tässä harjoituksessa  
- Käytä aina hyviä salasanoja.  
Bonustehtäviin:  
- [Django 4.1 Documentation: Many-to-one relationships](https://docs.djangoproject.com/en/4.1/topics/db/examples/many_to_one/)  
- ForeignKey tulee many-puolelle  

[Linux-palvelimet 2023 alkukevät](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)   


---
## Tehtävät  


###  a) Kannattavaa. Tee oma tietokantasovellus. jossa on weppiliittymä. Kirjautuneet käyttäjät saavat lisätä, muokata ja poistaa tietueita. (Voit käyttää Djangon kehityspalvelinta. Tee jotain muuta kuin asiakastietokanta.) 



#### Kehitysympäristön asennus ja käyttöönotto  

Pip-paketit voivat sisältää mitä vain mm. haittaohjelmia, eli kannattaa 
olla tietoinen mitä pakettia on lataamassa ja 
sen lisäksi olla tarkkana että kirjoittaa paketin nimen oikein. 

    nadja@debbiedebian:~$ sudo apt-get update  
    
    nadja@debbiedebian:~$ sudo apt-get install virtualenv python3-pip   
    
    
Tehdään projektille uusi kansio ja siirrytään sinne:  

    nadja@debbiedebian:~$ mkdir django  

    nadja@debbiedebian:~$ cd django/  
    
    
Laitetaan kaikki siististi samaan paikkaan env-kansioon:  

    nadja@debbiedebian:~/django$ virtualenv -p python3 --system-site-packages env/  
    
"Herätetään" kehitysympäristö:  

    nadja@debbiedebian:~/django$ source env/bin/activate  
    
.. ja tarkistetaan vielä:  

    (env) nadja@debbiedebian:~/django$ which pip



![Näyttökuva (237)](https://user-images.githubusercontent.com/118609353/221434625-c4819f06-4fa2-4e0c-9d55-08999bf5b3c0.png)  


Luodaan requirements.txt -tiedosto, joka sisältää tekstin 'django':   

    (env) nadja@debbiedebian:~/django$ cat requirements.txt  
    
    (env) nadja@debbiedebian:~/django$ pip install -r requirements.txt  
    
    
Kokeillaan ajaa komento, jolla saadaan selville, mikä Djangon versio on asennettu:  

    (env) nadja@debbiedebian:~/django$ django-admin --version  
    
![Näyttökuva (238)](https://user-images.githubusercontent.com/118609353/221435505-17880525-b857-43d0-b791-a90d734fb2b6.png)


    (env) nadja@debbiedebian:~/django$ which django-admin

---> /home/nadja/django/env/bin/django-admin



---


#### Projektin luominen 

Luodaan projekti ja sille kansio:  

    (env) nadja@debbiedebian:~/django$ django-admin startproject nlilj  
    (env) nadja@debbiedebian:~/django$ ls  


![Näyttökuva (239)](https://user-images.githubusercontent.com/118609353/221435799-b1acb4f4-a59f-424f-ae53-874f61836a0e.png)

Siirrytään äsken luotuun 'nlilj'-kansioon:  

    (env) nadja@debbiedebian:~/django$ cd nlilj/
    
    (env) nadja@debbiedebian:~/django/nlilj$ ls  
    
![Näyttökuva (240)](https://user-images.githubusercontent.com/118609353/221436445-cc9370a3-f81c-4079-8d09-71de012bf758.png)

Tämä on "päätaso", josta manage.py -tiedosto löytyy. Kaikki Djangon komennot komentoriviltä annetaan './manage.py':llä.  



----

#### Kehityspalvelimen käynnistäminen  

Käynnistetään kehityspalvelin, joka on siis kehityskäyttöön tarkoitettu. Ei julkaistavaksi siis.  

    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py runserver 

![Näyttökuva (242)](https://user-images.githubusercontent.com/118609353/221437047-7108e5e7-79a6-478d-a015-afe4841a645d.png)  

Asennus siis onnistui, mutta nyt käytössä on vasta "kehys". Tarvitaan siis vielä jonkin verran toimenpiteitä. 

Suljen serverin:

    CTRL + C

---

#### Käyttäjät ja oikeudet   

Aina kun tietokantaan tehdään muutoksia:  

    $ ./manage.py makemigrations  
    $ ./manage.py migrate  
  
Jotta tietokantaa voidaan käsitellä, tarvitaan käyttäjä ja tietenkin itse tietokanta:    

    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py makemigrations  

    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py migrate  

![Näyttökuva (246)](https://user-images.githubusercontent.com/118609353/221438867-83cb3ee9-aa63-4165-ad28-94a4a6fff92e.png)  

Luodaan Djangoon käyttäjä:  
    
    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py createsuperuser


![Näyttökuva (247)](https://user-images.githubusercontent.com/118609353/221439137-47019104-5f18-4662-9d83-59ede8680f24.png)  

Kokeillaan kirjautumista selaimen käyttöliittymässä (http://127.0.0.1:8000/admin):  

![Näyttökuva (248)](https://user-images.githubusercontent.com/118609353/221439302-52690bb0-8835-4885-9720-d9356e674d22.png)  


Onnistuneen kirjautumisen jälkeen voidaankin lisätä muutama käyttäjä.  


![Näyttökuva (248)](https://user-images.githubusercontent.com/118609353/221440114-8f738467-a5ee-4422-b695-92a356e4282a.png)


![Näyttökuva (249)](https://user-images.githubusercontent.com/118609353/221440144-79abab9d-5b6d-4cd4-ab4b-fcf6c089f4d6.png)  

Muokataan myös oikeuksia:  


![Näyttökuva (250)](https://user-images.githubusercontent.com/118609353/221440362-2722a8f8-32c0-4f7f-b3c1-aedcb16c66b7.png)  


#### Tietokanta  

Katsellaan  hieman ympäristöä missä ollaan:   

    (env) nadja@debbiedebian:~/django/nlilj$ ls nlilj/  
    (env) nadja@debbiedebian:~/django/nlilj$ ls  
    
**Luodaan "app":**  

    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py startapp staffmembers   
    (env) nadja@debbiedebian:~/django/nlilj$ ls   
    (env) nadja@debbiedebian:~/django/nlilj$ ls staffmembers/

![Näyttökuva (252)](https://user-images.githubusercontent.com/118609353/221441533-800a5b78-df66-4c92-821e-3c3c9d33a1cb.png)


<!--Muistettavaa:  
-  "Appeja" voi olla useampikin, vähintään yksi täytyy tehdä että voidaan koodata mitään. 
-  app nimetään pienellä monikossa, luokka taas on yksikössä ja alkaa isolla kirjaimella esim tuotteet ja Tuote()-->

App pitää myös lisätä **'settings.py'** -tiedostoon. <!--(Ollaan yhä "päätasolla", missä manage.py -tiedosto)-->  

    (env) nadja@debbiedebian:~/django/nlilj$ micro nlilj/settings.py
    
    -> INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'staffmembers', # lisää app tänne
    ]  
    
    
![Näyttökuva (253)](https://user-images.githubusercontent.com/118609353/221442050-6d7faaff-dbd3-4ee5-afed-39ca108af1fb.png)

Täytyy myös luoda luokka **'Staffmember'**, jonka avulla määritellään tietokantaan menevät tiedot(mm. attribuutin nimi, tietotyyppi).   

    (env) nadja@debbiedebian:~/django/nlilj$ ls
    
    (env) nadja@debbiedebian:~/django/nlilj$ micro staffmembers/models.py  
    
![Näyttökuva (256)](https://user-images.githubusercontent.com/118609353/221442631-cae2b429-611a-41ba-b09f-93f8d8a6e10f.png)

    
    
    from django.db import models  

    
    class Staffmember(models.Model):  
	     name = models.CharField(max_length=250)
	     city = models.CharField(max_length=250)
	     departmentname = models.CharField(max_legth=250)
	

![Näyttökuva (254)](https://user-images.githubusercontent.com/118609353/221442480-85fd780f-a394-400a-9e57-73448b792a41.png)

Ja muistetaan:  

    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py makemigrations  
    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py migrate  
    
    
<!-- .. ja tarkistetaan että ollaan päätasolla..-->


Seuraavaksi muokataan tiedostoa **admin.py**:  

    (env) nadja@debbiedebian:~/django/nlilj$ micro staffmembers/admin.py  


    from django.contrib import admin  
    from . import models  

    admin.site.register(models.Staffmember)





![Näyttökuva (257)](https://user-images.githubusercontent.com/118609353/221443132-03fbaebf-ad47-40de-9bf1-81e7b4993a43.png)


Sitten kokeillaan selaimessa, saako käyttäjä 'Heikki' oikeuksillaan (staff&superuser) lisättyä, muokattua ja poistettua tietueita. Näyttää onnistuvan:  





![Näyttökuva (258)](https://user-images.githubusercontent.com/118609353/221443658-fa00f441-b2b6-4c04-97de-1fdfeb2d5549.png)  

Laitetaan vielä nimet näkymään käyttöliittymässä, sillä eihän Heikki löydä henkilökunnan tietoja jos kaikki ovat objekteja:  



![Näyttökuva (260)](https://user-images.githubusercontent.com/118609353/221443811-69af0ce0-7e78-4180-9eb8-9bfac857f1ad.png)


    (env) nadja@debbiedebian:~/django/nlilj$ ls  
    (env) nadja@debbiedebian:~/django/nlilj$ micro staffmembers/models.py  
    
Lisätään **models.py** tiedostoon:  

    
    from django.db import models  
    
    class Staffmember(models.Model):  
	      name = models.CharField(max_length=250)  
	      city = models.CharField(max_length=250)  
	      departmentname = models.CharField(max_length=250)  

	      def __str__(self): #tämä lisätään  
	        return self.name  
          
          
![Näyttökuva (261)](https://user-images.githubusercontent.com/118609353/221444211-6d053a6e-419e-484b-bd1e-5b3c36a685b3.png)

---

#### Toimiminen kahdella välilehdellä:  

Avataan yksi terminaalivälilehti lisää jo aukiolevan lisäksi. 

    nadja@debbiedebian:~/django/nlilj$ ls
    
    nadja@debbiedebian:~/django/nlilj$ ./manage.py runserver


Vaikka ollaan ihan oikeassa kansiossa, silti tulee virheilmoitus: "/usr/bin/env: ‘python’: No such file or directory". Kehitysympäristö täytyy aktivoida uudelleen:  

    nadja@debbiedebian:~/django/nlilj$ cd ..  
    nadja@debbiedebian:~/django$ ls  

    nadja@debbiedebian:~/django$ source env/bin/activate  
    
    (env) nadja@debbiedebian:~/django$ ls  
    (env) nadja@debbiedebian:~/django$ cd nlilj/  
    (env) nadja@debbiedebian:~/django/nlilj$ ls  
    
    (env) nadja@debbiedebian:~/django/nlilj$ ./manage.py runserver  




![Näyttökuva (244)](https://user-images.githubusercontent.com/118609353/221438165-2e646974-89a8-4b10-8bef-4f77b4414371.png)




### b) Vapaaehtoinen: Suhde. Tee monesta yhteen -suhde (many-to-one relationship) kahden taulun välille. Esim. Yksi yritys - monta työntekijää.


    




---

**Pip** - Pythonilla kirjoitettu paketinhallintajärjestelmä, jota käytetään ohjelmistopakettien asentamiseen ja hallintaan. [(Wikipedia)](https://en.wikipedia.org/wiki/Pip_(package_manager))


---
---

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  


[Karvinen 2022: Django 4 Instant Customer Database Tutorial](https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django)  
[Django Tutorial: Many-to-one relationships](https://docs.djangoproject.com/en/4.1/topics/db/examples/many_to_one/)  



<!--- 
---
--->











