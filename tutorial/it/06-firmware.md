## Installazione firmware
Il firmware è basato su un'installazione standard di Raspbian, la distribuzione Debian
specializzata per Raspberry PI.

Come prima cosa installare Raspbian base secondo le indicazioni sul sito di Raspberry:

https://www.raspberrypi.org/downloads/raspbian/

Scaricare lo zip da GitHub oppure usare git per scaricare il seguente repository:

https://github.com/daniele-athome/thermorasp-deploy

Il repository non contiene il software in sé, piuttosto mette a disposizione degli script
per configurare un ambiente in grado di autoinstallarsi e aggiornarsi direttamente
all'interno della Raspberry PI.

Per questa fase è necessario il sistema operativo Linux sul proprio computer in quanto
andremo a lavorare su file system ext4.

All'interno del repository troverete il file di configurazione `local.properties.dist`.
Copiatelo in un nuovo file chiamandolo `local.properties` e procediamo alla sua modifica.
Di seguito la descrizione dei parametri.

* `SD_PATH_ROOT` - path alla directory dove è montata la partizione di root di Raspbian
* `SD_PATH_BOOT` - path alla directory dove è montata la partizione di boot di Raspbian
* `WIFI_SSID` - SSID della rete WiFi a cui connettersi
* `WIFI_WPA2PSK` - chiave WPA2 della rete WiFi
* `DEV_HOSTNAME` - hostname del futuro termostato
* `NETWORK_IPADDR` - indirizzo IP che dovrà avere il dispositivo nella forma IP/PREFISSO
* `NETWORK_GATEWAY` - default gateway da usare per uscire su Internet
* `NETWORK_DNS` - server DNS da usare
* `SSH_PUBLICKEY` - chiave pubblica da installare per l'accesso remoto in SSH
* `TEMPERATURE_GPIO_PIN` - numero del pin GPIO dove avete collegato il pin dati del sensore di temperatura

A questo punto eseguite lo script di setup **come utente root**:

```
# ./setup
```

Lo script copierà alcuni file dentro la vostra SD card. Terminato lo script, smontate
entrambe le partizioni e mettete la SD card nella Raspberry per farla partire.

### Installazione software termostato
Alla prima installazione sarà necessario eseguire lo script di aggiornamento manualmente
per installare subito tutto il software necessario. Entrate in SSH sul termostato come utente pi
ed eseguite:

```
$ sudo /etc/cron.daily/thermostat-updater
```

Lo script si connetterà ad Internet e scaricherà automaticamente il software direttamente dai
repository preposti. Lo script sarà eseguito anche ogni mattina alle 6:25 e scaricherà eventuali
aggiornamenti, se disponibili. Dopo alcuni minuti il demone del termostato dovrebbe essere attivo.
Potete controllarlo con il comando:

```
$ systemctl status thermostatd
```

### Configurazione termostato
A seconda della vostra configurazione o della vostra rete, dovreste poter accedere via web
all'interfaccia del termostato usando l'hostname configurato in precedenza:

http://thermostat.local/

In alternativa usate direttamente l'indirizzo IP.

TODO guida rapida configurazione termostato
