# DebianLinux
Installing Debian Linux on Virtualbox (Windows 10)


## h1 Linux Debianin asennus VirtualBoxilla virtuaalikoneeseen 

Tämä tehtävä osa Haaga-Helia ammattikorkeakoulun Linux-palvelimet -kurssia. Asensin onnistuneesti Linux Debianin VirtualBoxilla virtuaalikoneeseen näiden vaiheiden kautta. Käyttöjärjestelmänä Windows 10. 

### Ennen asennusta 
Latasin koneelleni debian-live-11.6.0-amd64-xfce+nonfree.iso -tiedoston, johon oli linkki kurssin opettajan ylläpitämällä sivustolla (https://terokarvinen.com/2021/install-debian-on-virtualbox/). 
Lisäksi latasin Oracle VM VirtualBox Manager -asennustiedoston (https://www.virtualbox.org/wiki/Downloads).  
Asensin Virtualboxin ja käynnistin sen.

### Asennuksen vaiheet Oracle VM VirtualBox Managerissa

Valitsin **New** -vaihtoehdon aloitusvalikosta ja sieltä **Expert Moden**
-> 



**Create Virtual Machine**  

**Hardware**  
Base Memory : 4096  
Processors : 2 CPUs  

**Hard disk**  
Create a Virtual Hard Disk Now  
Hard disk file location and size: Size 60.00GB  
Hard disk file type and variant: VDI (VirtualBox Disk Image)  


Seuraavaksi valitsin aloitusvalikosta harjoitetuksessa käytettävän virtuaalikoneen ja sen asetukset eli **Settings**
->

**System**  
System -> Motherboard -> Extended Features -> Valitsin Enable EFI(Special OSes only)  

**Storage**  
Storage -> Storage Devices -> Controller:IDE -> Valitsin kohdan “Empty”  
Storage -> Attributes -> Klikkasin CDROM -kuvaketta -> Choose a disk file -> Valitsin vaihtoehdon the virtual optical disk file (debian-live-11.6.0-amd64-xfce+nonfree)  

Muutosten hyväksymisen jälkeen valitsin virtuaalikoneen ja aloitusvalikosta **Start**.   

Valitsin (enterillä) listasta **Debian GNU/Linux Live (kernel 5.10.0-20-amd64)**,  
jonka jälkeen ainakin tällä koneella ja näillä asetuksilla jouduin odottamaan hieman pidemmän pienen hetken.  
Kun työpöytä avautui, valitsin pikakuvakkeen **Install Debian**.

**Debian**  
Language : American English  
Next ->  

Region: Europe  
Zone: Helsinki  
Next ->  

Keyboard: Finnish, Default (testasin ääkköset)  
Next ->  

Select Storage Device: VBOX HARDDISK  
Chose Erase Disk  
Next ->  

Added name  
added user name  
computer name  
password   
Next ->  

Lopuksi valitsin **Install**, jonka jälkeen kuluikin hieman pidempi tovi (n. 10 min) Linuxin asentuessa. 

Asennuksen jälkeen tuli mutka matkaan, sillä vaikka syötin oikean salasanan niin tuli virheilmoitus väärästä salasanasta.  
Tähän auttoi virtuaalikoneen käynnistäminen uudelleen. 

### Laitteen ja käyttöjärjestelmän tiedot

Laite     ASUS R520QA-EJ143T  
Suoritin      AMD A12-9720P RADEON R7, 12 COMPUTE CORES 4C+8G   2.70 GHz  
Asennettu     RAM	8,00 Gt (7,45 Gt käytettävissä)  
Järjestelmätyyppi     64-bittinen käyttöjärjestelmä, x64-suoritin  

Käyttöjärjestelmä	Windows 10 Home  


### Tarvittavat asennustiedostot: 

Debian 11.6.0  
https://cdimage.debian.org/images/unofficial/non-free/images-including-firmware/current-live/amd64/iso-hybrid/debian-live-11.6.0-amd64-xfce+nonfree.iso

Virtualbox 7.0.6  
https://www.virtualbox.org/wiki/Downloads


### Aineisto, jota harjoituksessa on hyödynnetty: 

Tero Karvinen - Install Debian on Virtualbox - Updated 2023:  
https://terokarvinen.com/2021/install-debian-on-virtualbox/

How to Install Debian Linux in VirtualBox on Windows 10 | Beginners Guide | (Buster):    
https://www.youtube.com/watch?v=cx8GzudB6uE

How to Install Debian Linux on VirtualBox in Windows | Beginners Guide:  
https://www.youtube.com/watch?v=poCSq_0OmjE




## The same story in English
I installed Linux Debian succesfully on virtual machine through these steps. 
First, I had to download Debian Linux iso -file, there was a link to it on https://terokarvinen.com/2021/install-debian-on-virtualbox/  
and Oracle VM VirtualBox Manager installation file https://www.virtualbox.org/wiki/Downloads. After downloading these files I installed the VirtualBox. 

Steps in Oracle VM VirtualBox Manager

New ->  

(Selected Expert Mode)  

Create Virtual Machine  
Name : This time it was LinuxDebian  

Hardware  
Base Memory : 4096  
Processors : 2 CPUs  

Hard disk  
Selected Create a Virtual Hard Disk Now  
Hard disk file location and size: Size 60.00GB  
Hard disk file type and variant: VDI (VirtualBox Disk Image)  

Settings ->  

System -> Motherboard -> Extended Features -> Selected Enable EFI(Special OSes only)  

Storage -> Storage Devices -> Controller:IDE -> Selected “Empty”  
Storage -> Attributes -> Clicked CDROM icon -> Choose a disk file -> Searched and selected the virtual optical disk file (debian-live-11.6.0-amd64-xfce+nonfree)  

After admitting the changes, started the “LinuxDebian”  

Selected Debian GNU/Linux Live (kernel 5.10.0-20-amd64) (by clicking enter) from the list  

Patiently waited for a while. When the desktop finally opened, i chose Install Debian.  

Language : American English
Next ->  
Region: Europe
Zone: Helsinki
Next ->  
Keyboard: Finnish, Default (tested äö etc)
Next ->  
Select Storage Device: VBOX HARDDISK
Chose Erase Disk 
Next ->  
Added name   
Added user name   
Added computer name   
Added password  
Next -> 
Chose Install 

And another, longer while of waiting (about 10 minutes).

Restarted the virtual machine after installing Linux because for some reason the user name and password didn’t work. 
  
  

Materials:

Tero Karvinen - Install Debian on Virtualbox - Updated 2023:
https://terokarvinen.com/2021/install-debian-on-virtualbox/

How to Install Debian Linux in VirtualBox on Windows 10 | Beginners Guide | (Buster):
https://www.youtube.com/watch?v=cx8GzudB6uE

How to Install Debian Linux on VirtualBox in Windows | Beginners Guide:
https://www.youtube.com/watch?v=poCSq_0OmjE

Debian 11.6.0  
https://cdimage.debian.org/images/unofficial/non-free/images-including-firmware/current-live/amd64/iso-hybrid/debian-live-11.6.0-amd64-xfce+nonfree.iso

Virtualbox 7.0.6  
https://www.virtualbox.org/wiki/Downloads


![Näyttökuva (55)](https://user-images.githubusercontent.com/118609353/213276250-9bc0040a-9568-46b8-8b17-71dde3bbdb29.png)

![Näyttökuva (56)](https://user-images.githubusercontent.com/118609353/213276313-e806fd43-113d-48d4-8d0f-f4500fb07436.png)

![Näyttökuva (57)](https://user-images.githubusercontent.com/118609353/213276333-dfc49006-d6ee-4ad8-b66c-4f79c4083e09.png)

![Näyttökuva (58)](https://user-images.githubusercontent.com/118609353/213276358-d435c827-957f-4579-a3e0-3b30ba309b3c.png)

![Näyttökuva (60)](https://user-images.githubusercontent.com/118609353/213276480-091e9d33-c34e-49bd-833a-8b132ed6c918.png)

![Näyttökuva (61)](https://user-images.githubusercontent.com/118609353/213279849-6f374c52-2d83-4b49-8c7d-450854ec838b.png)

![Näyttökuva (62)](https://user-images.githubusercontent.com/118609353/213276547-9bad50e7-9535-4dbc-b2aa-9123902f16ac.png)

![Näyttökuva (63)](https://user-images.githubusercontent.com/118609353/213276578-8efb9409-cabd-49c2-bc10-5bf136db333f.png)

![Näyttökuva (64)](https://user-images.githubusercontent.com/118609353/213276621-dee8a780-1b03-4c36-a0a7-41f1fbeec205.png)

![Näyttökuva (65)](https://user-images.githubusercontent.com/118609353/213276639-693895e5-d4e4-44be-afd0-ef2e312700f5.png)

![Näyttökuva (66)](https://user-images.githubusercontent.com/118609353/213276655-ad823e3b-bbdd-4937-816d-93a26af1404a.png)

![Näyttökuva (67)](https://user-images.githubusercontent.com/118609353/213276667-6b819577-0e07-4fb5-b582-47bbded7840f.png)

![Näyttökuva (68)](https://user-images.githubusercontent.com/118609353/213276686-9f2facb2-8737-4052-9718-96ebf21ae0a6.png)

![Näyttökuva (69)](https://user-images.githubusercontent.com/118609353/213286350-96052566-ce83-4daa-a897-8f4f96553651.png)
![Näyttökuva (70)](https://user-images.githubusercontent.com/118609353/213286354-ac83a5d9-5b3d-40df-9e95-457657521cc3.png)
![Näyttökuva (72)](https://user-images.githubusercontent.com/118609353/213286355-6d1ba351-51cd-4035-b49f-f0220bdce9a3.png)

