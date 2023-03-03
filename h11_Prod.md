

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

Asensin tehtävää varten täysin uuden virtuaalikoneen. 

#### Päivitykset, palomuuri ja Apachen asennus  

	$ su root  (jos uusi virtuaalikone)
	
	root:# sudo adduser nadja sudo (jos uusi virtuaalikone)
	
	root:# su nadja (jos uusi virtuaalikone)

	$ sudo apt-get update   

	$ sudo apt-get -y dist-upgrade  

	$ sudo apt-get -y install ufw  

	$ sudo ufw enable  
	
	$ sudo apt-get -y install apache2  
	
	$ sudo systemctl start apache2  
	
	$ sudo service apache2 status
	
Apachen testisivun korvaaminen:  

	$ echo "Vaihdettu"|sudo tee /var/www/html/index.html  
	
Testaaminen, onnistuiko:  

	$ curl localhost  
	
	
	
![Näyttökuva (271)](https://user-images.githubusercontent.com/118609353/222438047-df9ca9c0-9020-409e-ae1b-38f95eb286c4.png)

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


	nadja@debian:~$ ls /etc/apache2/sites-enabled/  
	
	-> 000-default.conf  
	
	nadja@debian:~$ cat /etc/apache2/sites-enabled/000-default.conf  
	
	nadja@debian:~$ /sbin/apachectl configtest  
	
	
Luodaan kansio **publicwsgi** ja tehdään sinne index.html:    

	nadja@debian:~$ pwd
	-> '/home/nadja'

	nadja@debian:~$ mkdir -p publicwsgi/nlilj/static
	
Asennetaan micro -editori:  

	nadja@debian:~$ sudo apt-get install micro
	
Mennään kansioon **publicwsgi**:  

	nadja@debian:~$ ls
	
	nadja@debian:~$ cd publicwsgi/nlilj/static
	
Luodaan tiedosto **index.html**:  
	
	nadja@debian:~$ micro index.html
	-> 'hellothere'

Mennään määrittelemään polut oikeaksi:  

	nadja@debian:~$ cd /etc/apache2/
	nadja@debian:~$ ls
	nadja@debian:~$ /etc/apache2$ cd sites-enabled/
	nadja@debian:~$ /etc/apache2/sites-enabled$ ls
	
	nadja@debian:~$ sudo cp 000-default.conf djfrontpage.conf    
	
	nadja@debian:/etc/apache2/sites-enabled$ micro djfrontpage.conf  
	
	->
	
	<VirtualHost *:80>
            DocumentRoot /home/nadja/publicwsgi/nlilj/static/
            <Directory /home/nadja/publicwsgi/nlilj/static/>
                    require all granted
            </Directory>
    	</VirtualHost>  
	
	
![Näyttökuva (274)](https://user-images.githubusercontent.com/118609353/222451198-0a3a3814-5686-42dc-b02d-f0ef412c026f.png)

Käynnistetään Apache uudelleen:  

	nadja@debian:~$ sudo systemctl restart apache2
	
Säädetään sites-enabled -määrittelyä:  
	
	nadja@debian:~$ sudo a2ensite djfrontpage.conf 
	
Tuli error:  

![Näyttökuva (275)](https://user-images.githubusercontent.com/118609353/222453176-d9e46327-ad8f-4267-8e5f-1deea8d9de68.png)

Siirrän **djfrontpage.conf** -tiedoston sites-available-kansioon ja kokeilen uudestaan: 

	nadja@debian:/etc/apache2/sites-available$ sudo a2ensite djfrontpage.conf
	
	nadja@debian:/etc/apache2/sites-available$ sudo a2dissite 000-default.conf  
	
	
Näytti onnistuvan: 

	
![Näyttökuva (276)](https://user-images.githubusercontent.com/118609353/222454408-0e9c879d-b657-4d18-8767-7468ca859db3.png)


Apachen uudelleenkäynnistys:  
	
	nadja@debian:~$ sudo systemctl restart apache
	
Muutetaan djfrontpage.conf aliakseksi:  


	<VirtualHost *:80>
            Alias /static/ /home/nadja/publicwsgi/nlilj/static/
            <Directory /home/nadja/publicwsgi/nlilj/static/>
                    require all granted
            </Directory>
    </VirtualHost>
    
 
Tarkastetaan, näkyykö selaimessa, 'http://localhost/static/'.

![Näyttökuva (277)](https://user-images.githubusercontent.com/118609353/222455866-9dab482e-c89a-4825-b1c9-2fede7dd10da.png)

---

#### Virtual-env  

Sitten virtuaalikehitysympäristön vuoro. 
	
	($ sudo apt-get update)  
	
	nadja@debian:~$ sudo apt-get install virtualenv

	
Mennään kotihakemistoon ja valitaan kansio **publicwsgi**:  

	nadja@debian:~$  cd  
	nadja@debian:~$ cd publicwsgi/  

Asennetaan:  

	nadja@debian:~/publicwsgi$ virtualenv -p python3 --system-site-packages env
	
![Näyttökuva (278)](https://user-images.githubusercontent.com/118609353/222457028-cf7ee06b-f3f1-495e-81b3-dad36c8c43a9.png)

**Virtual envin aktivoiminen, Django:**  

	nadja@debian:~/publicwsgi$ source env/bin/activate

	
Tarkistetaan: 	
	
	(env) nadja@debian:~/publicwsgi$ which pip

	->/home/nadja/publicwsgi/env/bin/pip  
	
![Näyttökuva 2023-03-02 163105](https://user-images.githubusercontent.com/118609353/222457518-d1642da4-fb83-4e74-8335-3e9e789e14ea.png)

Django:  
	
	(env) nadja@debian:~/publicwsgi$ micro requirements.txt

	->
	django  
	
	(env) nadja@debian:~/publicwsgi$ pip install -r requirements.txt  

	
Testataan:  

	(env) nadja@debian:~/publicwsgi$ django-admin --version
	-> 
	4.1.7
	
![Näyttökuva 2023-03-02 163341](https://user-images.githubusercontent.com/118609353/222458097-35f3dd76-a1c3-42a6-9542-9e310939aa28.png)

Luodaan uusi django-projekti:  

	(env) nadja@debian:~/publicwsgi$ django-admin startproject nlilj
 
	
	-> "CommandError: '/home/nadja/publicwsgi/nlilj' already exists"
	-> valittaa koska static laitettiin tänne aikaisemmin nlilj-nimiseen kansioon

![Näyttökuva 2023-03-02 163341](https://user-images.githubusercontent.com/118609353/222458443-734c2f9a-9541-4e3f-82dd-ea9c698536b4.png)

Poistetaan siis hetkeksi samanniminen (nlilj) kansio (ja alikansio static, sekä siellä oleva index.html):  

	(env) nadja@debian:~/publicwsgi$ rm -r nlilj
	
Ja yritetään django-projektin luomista uudelleen:  

	(env) nadja@debian:~/publicwsgi$ django-admin startproject nlilj


	(env) nadja@debian:~/publicwsgi$ cd nlilj/
	(env) nadja@debian:~/publicwsgi/nlilj$ ls
	
	-> 
	'manage.py'  'nlilj'  
	
![Näyttökuva 2023-03-02 163749](https://user-images.githubusercontent.com/118609353/222459280-736858e9-adeb-481c-b075-58f775069ff1.png)

Onnistui, eli laitetaan static-kansio ja index.html takaisin:  

	(env) nadja@debian:~/publicwsgi/nlilj$ cat /etc/apache2/sites-enabled/djfrontpage.conf  
	
    <VirtualHost *:80>
            Alias /static/ /home/nadja/publicwsgi/nlilj/static/
            <Directory /home/nadja/publicwsgi/nlilj/static/>
                    require all granted
            </Directory>
    </VirtualHost>  
	
	
	(env) nadja@debian:~/publicwsgi/nlilj$ mkdir /home/nadja/publicwsgi/nlilj/static/

	(env) nadja@debian:~/publicwsgi/nlilj$ pwd
	->
	/home/nadja/publicwsgi/nlilj

	(env) nadja@debian:~/publicwsgi/nlilj$ ls
	->
	'manage.py'  'nlilj'  'static'
	
![Näyttökuva 2023-03-02 163955](https://user-images.githubusercontent.com/118609353/222459961-3745af59-3adc-4139-8e67-1ae12736ee3d.png)


Tehdään vielä index.html -tiedosto:  

	(env) nadja@debian:~/publicwsgi/nlilj$ cd static
	(env) nadja@debian:~/publicwsgi/nlilj/static$ ls
	(env) nadja@debian:~/publicwsgi/nlilj/static$ micro index.html
	
	-> 
	New static
	
Testataan:  

	curl localhost/static/

![Näyttökuva 2023-03-02 164454](https://user-images.githubusercontent.com/118609353/222461200-6b811c0a-18bb-4bac-8803-d97d28c8bcdf.png)

	
**Virtual envin deaktivoiminen:**

	$ deactivate

---

#### mod_wsgi  

	nadja@debian:~/publicwsgi/nlilj$ cd /etc/apache2/

	nadja@debian:/etc/apache2$ ls

	nadja@debian:/etc/apache2$ cd sites-available/

	nadja@debian:/etc/apache2/sites-available$ ls

	nadja@debian:/etc/apache2/sites-available$ micro djfrontpage.conf 


	->
	
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
	
	
	nadja@debian:/etc/apache2/sites-available$ /sbin/apache2ctl configtest
	
	
![Näyttökuva 2023-03-02 164910](https://user-images.githubusercontent.com/118609353/222462313-0b212464-8a66-49f5-8426-1dcfcfd93e2e.png)

Näinkin voi käydä:  

	"Invalid command 'WSGIDaemonProcess', perhaps misspelled or defined by a module not included in the server 		configuration
	Action 'configtest' failed. "

Kokeillaan:  

	sudo apt-get install libapache2-mod-wsgi-py3
	sudo systemctl restart apache2

	nadja@debian:/etc/apache2/sites-available$ /sbin/apache2ctl configtest
	->
	syntax ok
	
![Näyttökuva 2023-03-02 165135](https://user-images.githubusercontent.com/118609353/222463008-37a3a7a4-cec4-4391-839f-d7fe90823547.png)

Selaimessa 'http://localhost/'.  

	nadja@debian:$ curl -s localhost | grep title
        ->
	<title>The install worked successfully! Congratulations!</title>
		
![Näyttökuva 2023-03-02 170310](https://user-images.githubusercontent.com/118609353/222466246-62b6d5d0-2711-45c9-b296-1aa6e0947d91.png)

Selaimessa 'localhost/admin/':


![Näyttökuva 2023-03-02 170443](https://user-images.githubusercontent.com/118609353/222466637-9d8c4d00-36c4-4d91-9aaa-52059504f0d2.png)


Luodaan tietokanta, jotta saadaan käyttäjä lisättyä:  
 

	(env) nadja@debian:~/publicwsgi/nlilj$ ./manage.py makemigrations
	(env) nadja@debian:~/publicwsgi/nlilj$ ./manage.py migrate  
	
Tehdään käyttäjä:  

	(env) nadja@debian:~/publicwsgi/nlilj$ ./manage.py createsuperuser

![Näyttökuva 2023-03-02 170715](https://user-images.githubusercontent.com/118609353/222467285-c7910872-5bc6-4baf-bae9-9587fdab5c7c.png)


Debuggaus pois päältä:  

	nadja@debian:~/publicwsgi/nlilj$ micro nlilj/settings.py 
	->
	DEBUG = False

	ALLOWED_HOSTS = ['localhost'] <- tänne myös muut sivustot ('nli.website', 'kokeilu.com')  

![Näyttökuva 2023-03-02 170946](https://user-images.githubusercontent.com/118609353/222468002-1f38215c-5c05-4fa2-820b-554aac433f12.png)

Muutetaan wsgi.py tiedoston muokkauspäivää:  

	nadja@debian:~/publicwsgi/nlilj$ touch nlilj/wsgi.py  
	
---

#### Ulkoasu

	nadja@debian:~/publicwsgi/nlilj/nlilj$ micro settings.py

Lisätään settings.py -tiedostoon:  

	import os <- import tiedoston alkuun

	STATIC_ROOT = os.path.join(BASE_DIR, 'static/') <- tämä hieman "peremmälle" tiedostoon, ei toimi jos on heti 		importin perässä
	
![Näyttökuva 2023-03-02 171227](https://user-images.githubusercontent.com/118609353/222468776-f9caf52f-732c-450b-b2a7-c8d5b874a832.png)


	(env) nadja@debian:~/publicwsgi/nlilj$ ./manage.py collectstatic

	Are you sure you want to do this?
	Type 'yes' to continue, or 'no' to cancel: yes
	128 static files copied to '/home/nadja/publicwsgi/nlilj/static'.
	

![Näyttökuva 2023-03-02 171404](https://user-images.githubusercontent.com/118609353/222469202-16811f50-5d1e-4518-8bf2-46bda738b779.png)

Selaimessa 'localhost/admin/':


![Näyttökuva 2023-03-02 171531](https://user-images.githubusercontent.com/118609353/222469557-23e97545-cfbe-424c-bf73-0bacc67a4f28.png)



---


### b) Vapaaehtoinen, vaikeahko: dev&prod: tee ja kokeile Django-projekti eri käyttäjällä tai koneella testipalvelimella ('./manage.py runserver'). Kopioi se tuotantopalvelimelle ja ota käyttöön ('touch */wsgi.py').  

---

### c) Vapaaehtoinen, vaikea: muutto: jatkoa b-kohtaan: muokkaa tietokannan rakennetta kehityspalvelimella. Kopioi koodi tuotantopalvelimelle, ja päivitä tietokannan rakenne migraatioilla.  


---
VirtualBoxin skaalautuvuus:  

	nadja@debian:/media/cdrom0$ sudo bash VBoxLinuxAdditions.run 

Lisäksi Copy-Paste toimimaan molempiin suuntiin:  
Graafisesta käyttöliittymästä Devices -> Shared ClipBoard -> Bidirectional



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











