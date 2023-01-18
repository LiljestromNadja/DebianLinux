# DebianLinux
Installing Debian Linux on Virtualbox (Windows 10)


## Linux Debianin asennus VirtualBoxilla virtuaalikoneeseen. 

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


Seuraavaksi valitsin aloitusvalikosta asetukset eli **Settings**
->

**System**  
System -> Motherboard -> Extended Features -> Selected Enable EFI(Special OSes only)  

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

Lopuksi valitsin **Install**, jonka jälkeen kuluikin hieman pidempi tovi Linuxin asentuessa. 

Asennuksen jälkeen tuli mutka matkaan, sillä vaikka syötin oikean salasanan niin tuli virheilmoitus väärästä salasanasta.  
Tähän auttoi virtuaalikoneen käynnistäminen uudelleen. 

### Laitteen ja käyttöjärjestelmän tiedot

Laite ASUS R520QA-EJ143T  
Suoritin AMD A12-9720P RADEON R7, 12 COMPUTE CORES 4C+8G   2.70 GHz  
Asennettu RAM	8,00 Gt (7,45 Gt käytettävissä)  
Järjestelmätyyppi	64-bittinen käyttöjärjestelmä, x64-suoritin  

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
I installed Linux Debianin succesfully on virtual machinethrough these steps. 
First, I had to download Debian Linux iso -file, there was a link to it on https://terokarvinen.com/2021/install-debian-on-virtualbox/  
and Oracle VM VirtualBox Manager installation file.  After downloading these files I installed the VirtualBox. 

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

And another, longer while of waiting

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



