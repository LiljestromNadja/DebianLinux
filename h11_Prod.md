

# h11_Prod 

**Tehtävänanto**  

a) Tee Djangon tuotantoasennus.  
b) Vapaaehtoinen, vaikeahko: dev&prod: tee ja kokeile Django-projekti eri käyttäjällä tai koneella testipalvelimella ('./manage.py runserver'). Kopioi se tuotantopalvelimelle ja ota käyttöön ('touch */wsgi.py').  
c) Vapaaehtoinen, vaikea: muutto: jatkoa b-kohtaan: muokkaa tietokannan rakennetta kehityspalvelimella. Kopioi koodi tuotantopalvelimelle, ja päivitä tietokannan rakenne migraatioilla.  

**Vinkit:**  

[Karvinen 2022: Deploy Django 4 - Production Install](https://terokarvinen.com/2022/deploy-django/)  


[Lähde: Linux-palvelimet 2023 alkukevät](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)    


---
## Tehtävät  


###  a) Tee Djangon tuotantoasennus.  



#### Päivitykset, palomuuri ja Apachen asennus  

	$ sudo apt-get update   

	$ sudo apt-get -y dist-upgrade  

	$ sudo apt-get -y install ufw  

	$ sudo ufw enable  
	
	$ sudo apt-get -y install apache2  
	
	$ sudo systemctl start apache2  
	
Apachen testisivun korvaaminen:  

	$ echo "Vaihdettu"|sudo tee /var/www/html/index.html  
	
	
sites-enabled muuttaminen:  

	$ sudo a2ensite nli.conf  
	$ sudo a2dissite 000-default.conf  
	
Apachen uudelleenkäynnistys:  

	$ sudo systemctl restart apache2
	
Apachen tila:  

	$ sudo service apache2 status
	
Tehtyjen määrittelyjen toimivuuden tarkastaminen:  

	$ /sbin/apache2ctl configtest  
	
---
	
#### Alkutilanteen kartoittaminen  


	nadja@debbiedebian:~$ ls /etc/apache2/sites-enabled/  
	
	-> nli.conf  
	
	nadja@debbiedebian:~$ cat /etc/apache2/sites-enabled/nli.conf  
	
	nadja@debbiedebian:~$ /sbin/apachectl configtest  
	
	
Luodaan kansio **publicwsgi** ja tehdään sinne index.html:    

	nadja@debbiedebian:~$ pwd
	-> '/home/nadja'

	mkdir -p publicwsgi/nlilj/static

	micro index.html
	-> 'hellothere'

Mennään määrittelemään polut oikeaksi:  

	nadja@debbiedebian:~$ cd /etc/apache2/
	nadja@debbiedebian:~$ /etc/apache2$ cd sites-enabled/


	nadja@debbiedebian:~$ /etc/apache2/sites-enabled$ ls
	
	nadja@debbiedebian:~$ sudo cp frontpage.conf djfrontpage.conf    
	
	nadja@debbiedebian:~$ sudoedit djfrontpage.conf  
	
	->
	
	<VirtualHost *:80>
            DocumentRoot /home/nadja/publicwsgi/nlilj/static/
            <Directory /home/nadja/publicwsgi/nlilj/static/>
                    require all granted
            </Directory>
    	</VirtualHost>  
	
Käynnistetään Apache uudelleen:  

	nadja@debbiedebian:~$ sudo systemctl restart apache2
	
Säädetään sites-enabled -määrittelyä:  
	
	nadja@debbiedebian:~$ sudo a2dissite nli.conf

	nadja@debbiedebian:~$ sudo a2ensite djfrontpage.conf
	
Apachen uudelleenkäynnistys:  
	
	nadja@debbiedebian:~$ sudo systemctl restart apache
	
Muutetaan djfrontpage.conf aliakseksi:  


	<VirtualHost *:80>
            Alias /static/ /home/nadja/publicwsgi/nlilj/static/
            <Directory /home/nadja/publicwsgi/nlilj/static/>
                    require all granted
            </Directory>
    </VirtualHost>
    
 
Tarkastetaan, näkyykö selaimessa, 'http://localhost/static'.

---

#### Virtual-env  
	
	($ sudo apt-get update)  
	
	nadja@debbiedebian:~$ sudo apt-get -y install virtualenv
	
Mennään kotihakemistoon ja valitaan kansio **publicwsgi**:  

	nadja@debbiedebian:~$  cd  
	nadja@debbiedebian:~$ cd publicwsgi/  

Asennetaan:  

	nadja@debbiedebian:~$ virtualenv -p python3 --system-site-packages env  

**Virtual envin aktivoiminen, Django:**  

	nadja@debbiedebian:~/publicwsgi$ source env/bin/activate
	
Tarkistetaan: 	
	
	(env) nadja@debbiedebian:~/publicwsgi$ which pip
	->/home/nadja/publicwsgi/env/bin/pip  
	
Django:  
	
	(env) nadja@debbiedebian:~/publicwsgi$ micro requirements.txt
	->
	django  
	
	(env) nadja@debbiedebian:~/publicwsgi$ pip install -r requirements.txt   
	
Testataan:  

	(env) nadja@debbiedebian:~/publicwsgi$ django-admin --version
	-> 
	4.1.7
	
Luodaan uusi django-projekti:  

	(env) nadja@debbiedebian:~/publicwsgi$ django-admin startproject nlilj  
	
	-> "CommandError: '/home/nadja/publicwsgi/nlilj' already exists"
	-> valittaa koska static laitettiin tänne aikaisemmin  
	
Poistetaan siis hetkeksi samanniminen (nlilj) kansio (ja alikansio static, sekä siellä oleva index.html):  

	(env) nadja@debbiedebian:~/publicwsgi$ rm -r nlilj  
	
Ja yritetään django-projektin luomista uudelleen:  

	(env) nadja@debbiedebian:~/publicwsgi$ django-admin startproject nlilj

	(env) nadja@debbiedebian:~/publicwsgi$ cd nlilj/
	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ ls
	
	-> 
	'manage.py'  'nlilj'  
	
Onnistui, eli laitetaan static-kansio ja index.html takaisin:  

	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ cat /etc/apache2/sites-enabled/djfrontpage.conf  
	
    <VirtualHost *:80>
            Alias /static/ /home/nadja/publicwsgi/nlilj/static/
            <Directory /home/nadja/publicwsgi/nlilj/static/>
                    require all granted
            </Directory>
    </VirtualHost>  
	
	
	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ mkdir /home/nadja/publicwsgi/nlilj/static/

	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ pwd
	->
	/home/nadja/publicwsgi/nlilj

	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ ls
	->
	'manage.py'  'nlilj'  'static'
	
	
Kokeillaan vielä tekemällä muutos index.html -tiedostoon:  

	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ cd static
	(env) nadja@debbiedebian:~/publicwsgi/nlilj/static$ ls
	(env) nadja@debbiedebian:~/publicwsgi/nlilj/static$ micro index.html
	
	-> 
	New static
	
Testataan:  

	curl localhost/static/


	
**Virtual envin deaktivoiminen:**

	$ deactivate

---

#### mod_wsgi  

	nadja@debbiedebian:~/publicwsgi/nlilj$ cd /etc/apache2/

	nadja@debbiedebian:/etc/apache2$ cd sites-available/

	nadja@debbiedebian:/etc/apache2/sites-available$ ls

	nadja@debbiedebian:/etc/apache2/sites-available$ micro djfrontpage.conf 



	
	Define TDIR /home/nadja/publicwsgi/nlilj
	Define TWSGI /home/nadja/publicwsgi/nlilj/nlilj/wsgi.py
	Define TUSER nadja
	Define TVENV /home/nadja/publicwsgi/env/lib/python3.9/site-packages

	<VirtualHost *:80>
        	Alias /static/ ${TDIR}/static/
        <Directory ${TDIR}/static/>
                Require all granted
        </Directory>

        WSGIDaemonProcess ${TUSER} user=${TUSER} group=${TUSER} threads=5 python-path="${TDIR}:${TVENV}"
        WSGIScriptAlias / ${TWSGI}
        <Directory ${TDIR}>
             WSGIProcessGroup ${TUSER}
             WSGIApplicationGroup %{GLOBAL}
             WSGIScriptReloading On
             <Files wsgi.py>
                Require all granted
             </Files>
        </Directory>

	</VirtualHost>

	Undefine TDIR
	Undefine TWSGI
	Undefine TUSER
	Undefine TVENV  
	
Testataan, tuleeko syntax erroreita:  
	
	
	nadja@debbiedebian:/etc/apache2/sites-available$ /sbin/apache2ctl configtest
	->
	syntax ok
	
Näinkin voi käydä:  

	"Invalid command 'WSGIDaemonProcess', perhaps misspelled or defined by a module not included in the server 		configuration
	Action 'configtest' failed. "

	sudo apt-get install libapache2-mod-wsgi-py3
	sudo systemctl restart apache2

	nadja@debbiedebian:/etc/apache2/sites-available$ /sbin/apache2ctl configtest
	->
	syntax ok
	
Selaimessa 'http://localhost/'.  

	nadja@debbiedebian:$ curl -s localhost | grep title
        ->
	<title>The install worked successfully! Congratulations!</title>
		
<!--localhost/admin

 nk 268 -->

	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ ./manage.py makemigrations
	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ ./manage.py migrate  
	
Tehdään käyttäjä:  

	(env) nadja@debbiedebian:~/publicwsgi/nlilj$ ./manage.py createsuperuser

<!--
nk269
-->

Debuggaus pois päältä:  

	nadja@debbiedebian:~/publicwsgi/nlilj$ micro nlilj/settings.py 
	->
	DEBUG = False

	ALLOWED_HOSTS = ['localhost'] <- tänne myös muut sivustot ('nli.website', 'kokeilu.com')  
	
Muutetaan wsgi.py tiedoston muokkauspäivää:  

	nadja@debbiedebian:~/publicwsgi/nlilj$ touch nlilj/wsgi.py  
	
---

#### Ulkoasu

	nadja@debbiedebian:~/publicwsgi/nlilj/nlilj$ micro settings.py

Lisätään settings.py -tiedostoon:  

	import os <- import alkuun

	STATIC_ROOT = os.path.join(BASE_DIR, 'static/') <- tämä hieman "peremmälle" tiedostoon, ei toimi jos on heti 		importin perässä


	$ ./manage.py collectstatic
	Are you sure you want to do this?
	Type 'yes' to continue, or 'no' to cancel: yes
	128 static files copied to '/home/nadja/publicwsgi/nlilj/static'.

---


### b) Vapaaehtoinen, vaikeahko: dev&prod: tee ja kokeile Django-projekti eri käyttäjällä tai koneella testipalvelimella ('./manage.py runserver'). Kopioi se tuotantopalvelimelle ja ota käyttöön ('touch */wsgi.py').  

---

### c) Vapaaehtoinen, vaikea: muutto: jatkoa b-kohtaan: muokkaa tietokannan rakennetta kehityspalvelimella. Kopioi koodi tuotantopalvelimelle, ja päivitä tietokannan rakenne migraatioilla.  






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











