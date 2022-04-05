# Kodi su Raspberry Pi OS (64-bit)
Procedura di installazione e configurazione di Kodi su sistema operativo Raspberry Pi OS (64-bit)

# Lista Hardware
1. Raspberry Pi 4 Model B 4Gb
2. **(Opzionale)** Hard Disk SSD Kingston A400 da 240GB
3. **(Opzionale)** Adattatore Sata UGREEN USB 3.0
4. **(Opzionale)** Geekworm Modulo X735 con pulsante
5. **(Opzionale)** Display SSD1306 OLED 0.96"
6. **(Opzionale)** Cavi Estensione per HDMI
7. **(Opzionale)** Cavi Estensione per audio

# Requisiti Software
1. Sistema Operativo: **Raspberry Pi OS Lite (64-bit)**
2. Client SSH: **Putty**
3. Utility per la generazione delle chiavi RSA e DSA: **Puttygen**

# Installare e configurare il sistema operativo su Raspberry
Aprire Raspberry Pi Imager e selezionare il sistema operativo. In questo caso:
  * <kbd>CHOOSE OS</kbd>
  * <kbd>Raspberry Pi OS (other)</kbd>
  * <kbd>Raspberry Pi OS Lite (64-bit)</kbd>

Dopodichè, selezionare la scheda SD:
  * <kbd>CHOOSE STORAGE</kbd>
  * selezionare la scheda SD dall'elenco
    >**ATTENZIONE!!!** Questa operazione cancellerà tutti i dati sul dispositivo selezionato. Quindi, porre molta attenzione sulla scelta del dispositivo.

Prima di passare alla scrittura, premere i tasti <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>x</kbd>. Con questa combinazione di tasti, si aprirá una finestra di configurazione iniziale del sistema.
> Le opzione avanzate sono **Opzionali** e possono essere modificate anche dopo l'installazione del sistema con il comando
> ```bash
> sudo raspi-config
> ```

Infine, cliccare su <kbd>Write</kbd>. Attendere che Imager abbia terminato la scrittura e la verifica.

Inserire la scheda SD nel Raspberry e avviarlo.

# Accedere al Raspberry
Si può accedere al Raspberry in 2 modi
  1. Collegare monitor, tastiera e mouse (solo se si è stata installata la versione del OS con Desktop) al Raspberry.
  2. Conoscendo l'indirizzo IP del Raspberry, collegarsi aprendo una sessione ssh.
     > **Nota**: per procedere in questa modalità, bisogna aver inserito i parametri relativi all'accesso con SSH nelle `opzioni avanzate` di cui sopra

Per conoscere l'indirizzo IP del raspberry, utilizzare:
  1. software tipo [Advanced IP Scanner](http://www.advanced-ip-scanner.com/link.php?lng=it&ver=2-5-3850&beta=n&page=about).
     > Basta googlare `ip scanner`. Esistono centinaia di software del genere. Scegliere quello che più ci aggrada.
  2. Interrogando il proprio router (in genere, attraverso la relativa pagina web o software dedicato).

Una volta ottenuto l'indirizzo IP del Raspberry, aprire una sessione SSH e collegarsi al sistema. 

Anche qui, ci sono diversi software. Per esempio:
  1. [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/)
  2. [MobaXterm](https://mobaxterm.mobatek.net/)
  3. PowerShell e Prompt dei Comandi di Windows

# Installazione del software necessario su Raspberry Pi
### Preparazione
```bash
cd
wget https://raw.githubusercontent.com/ginocic/bash_aliases/main/.bash_aliases
```

Testare in una sessione ssh duplicata e se tutto funziona correttamente
```bash
aggiorna
riavvia
```

### Note
Se si vuole disabilitare bluetooth e WiFi, aprire il il file `config.txt` con `nano`
```bash
sudo nano /boot/config.txt
```
Trovare la seguente linea
```
# Additional overlays and parameters are documented /boot/overlays/README
```
e aggiungere queste 2 linee sotto
```
dtoverlay=disable-wifi
dtoverlay=disable-bt
```
# Impostare un indirizzo IP statico
>**Nota**: Questa sezione è opzionale ma io la consiglio.

Seguire questa [guida](https://github.com/ginocic/Impostare-indirizzo-IP-statico-al-raspberry)

# Spostare il file system di root del Raspberry Pi su SSD e abilitare il TRIM
>**Nota**: Questa sezione è opzionale. Io la consiglio per migliorare le prestazioni del sistema e allungare la vita della Micro SD.

Seguire questa [guida](https://gist.github.com/ginocic/3322d84c035f09ca956418c88c8f9b43)

# Installare il software per il Geekworm X735 V2.5
>**Nota**: Questa sezione è opzionale e non necessaria.

Seguire questa [guida](https://github.com/ginocic/Geekworm-X735-V2.5-Software)

# Connettere e programmare un display OLED
>**Nota**: Questa sezione è opzionale e non necessaria.

Seguire questa [guida](https://github.com/ginocic/RaspberryPi-Display-OLED)

# Installare Kodi
Riferimenti:
1. [Wiki Kodi](https://kodi.wiki/view/HOW-TO:Install_Kodi_on_Raspberry_Pi)
2. [PiMyLifeUp](https://pimylifeup.com/raspberry-pi-kodi/)

Per sicurezza, aggiornare il sistema
```bash
aggiorna
```
Dopo l'aggiornamento, con il comando seguente, installare Kodi e uno degli addon che non sono disponibili nel repository ufficiale di Kodi.
```bash
sudo apt install -y kodi kodi-inputstream-adaptive
```
### Configurare l'accelerazione hardware sul Raspberry
Aprire il file di configurazione d'avvio
```bash
sudo nano /boot/config.txt
```
Premere la combinazione di tasti <kbd>Ctrl</kbd>+<kbd>w</kbd> per cercare la stringa ```[pi4]``` e aggiungere, subito sotto l'intestazione trovata, la riga seguente per far caricare all'avvio il driver per l'accellerazione hardware HEVC
```
dtoverlay=rpivid-v4l2
```
Se si ha intenzione di usare anche file 4K HEVC, bisogna aumentare l'allocazione CMA.

Premere la combinazione di tasti <kbd>Ctrl</kbd>+<kbd>w</kbd> per cercare la stringa ```dtoverlay=vc4-kms-v3d``` e sostituirla con la linea seguente
```
dtoverlay=vc4-kms-v3d,cma-512
```
Salvare e uscire dall'editor con <kbd>CTRL + x</kbd>, <kbd>y</kbd>, <kbd>ENTER</kbd> e riavviare il sistema
```bash
riavvia
```

### Lanciare Kodi da terminale
Con il raspberry collegato ad un monitor o alla TV, lanciare la versione standalone di Kodi
```bash
kodi-standalone
```
Oppure, con questo comando, lanciare Kodi in background. Questo ci permetterà di operare sul sistema via la console
```bash
kodi-standalone &
```
A questo punto, si dovrebbe aver accesso all'interfaccia di Kodi

# Avvio automatico di Kodi all'avvio del Raspberry
Creare il file di servizio
```bash
sudo nano /lib/systemd/system/kodi.service
```
Aggiungere nel file appena creato le seguenti linee
```
[Unit]
Description = Kodi Media Center
After = remote-fs.target network-online.target
Wants = network-online.target

[Service]
User = pi
Group = pi
Type = simple
ExecStart = /usr/bin/kodi-standalone
Restart = on-abort
RestartSec = 5

[Install]
WantedBy = multi-user.target
```
Salvare e uscire dall'editor con <kbd>CTRL + x</kbd>, <kbd>y</kbd>, <kbd>ENTER</kbd>.
Abilitare e avviare il servizio
```bash
sudo systemctl enable kodi
sudo systemctl start kodi
```
# Addons da installare
### Add-on:Extras
Questo addon fornisce un modo semplice per vedere gli extra (corti, scene cancellate, bloopers, ecc) di film e serie TV. Gli Extra sono accessibili via il menu di contesto nella libreria Video. Di default, l'addon cercherà gli "extra" nella sottocartella ```Extras```.

**Installazione**

Dalla Home di Kodi, seguire questi menù:
  - Settings
  - Add-ons
  - Install from repository
  - Context items
  - Extras
  - Install

**Posizione della cartella Extras**

Tipicamente, l'addon cerca una cartella chiamata ```Extras```. Il nome può essere cambiato nelle impostazioni dell'addon.

Per Films
```
...\Lucy (2014)\
...\Lucy (2014)\Extras\
```

Per le serie TV
```
...\Childhood's End
...\Childhood's End\Childhood's End S01E01
...\Childhood's End\Childhood's End S01E02
...\Childhood's End\Childhood's End S01E03
...\Childhood's End\Extras\
```

**Prevenire che gli Extra vengano aggiunti alla libreria**

Per prevenire che gli Extra vengano aggiunti alla libreria, creare il file ```Advancedsettings.xml``` e copiare il codice seguente
```xml
<advancedsettings version="1.0">
 	<video>
	 	 <excludefromscan>
		  	 <regexp>[-\._ ](extrafanart|sample|trailer|extrathumbs)[-\._ ]</regexp>
		  </excludefromscan>
		  <excludefromlisting>
			   <regexp>[-._ \\/](extrafanart|sample|trailer|extrathumbs)[-._ \\/]</regexp>
		  </excludefromlisting>
		  <!-- Extras: Section Start -->
		  <excludefromscan action="append">
			   <regexp>/extras/</regexp>
			   <regexp>[\\/]extras[\\/]</regexp>
		  </excludefromscan>
		  <excludetvshowsfromscan action="append">
			   <regexp>/extras/</regexp>
			   <regexp>[\\/]extras[\\/]</regexp>
		  </excludetvshowsfromscan>
		  <!-- Extras: Section End -->
 	</video>
</advancedsettings>
```
### Add-on:Backup
Questo addon fa un backup della libreria, delle playlists, degli addons installati e altri dettagli di configurazione su qualsiasi sorgente accessibile e scrivibile da Kodi (local, percorso di rete o cloud). I backup possono essere fatti manualmente o pianificati in automatico.

**Installazione**

Dalla Home di Kodi, seguire questi menù:
  - Settings
  - Add-ons
  - Install from repository
  - Program Add-ons
  - Backup
  - Install

**Utilizzo**
  - Home
  - Programs
  - XBMC Backup
  - Backup o Restore

# Configurare una libreria condivisa per instanze multiple di Kodi
Se si hanno moltleplici dispositivi Kodi nella rete locale, si può sincronizzarli condividendo il database della libreria via protocollo MySQL.

Questo permette di:
- condividere lo stato di visione dei media su tutti i dispositivi.
- terminare la visione di un media in una stanza e riprendere la visione in un'altra stanza.
- una sola libreria da gestire per tutti i dispositivi.

Fare riferimento alle pagine del [Wiki di Kodi](https://kodi.wiki/view/MySQL) per una corretta installazione del software necessario, la configurazione e la gestione.
> **Nota:** Come segnalato anche nella suddetta pagina, questa procedura è da considerarsi ***avazanta e sperimentale***

# ToDo-List
Abilitare il telecomando (per esempio [leggere qui](https://pimylifeup.com/kodi-remote-controls/))
