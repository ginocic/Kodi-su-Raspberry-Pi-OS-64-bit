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
4. 

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

