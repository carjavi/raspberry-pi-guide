<p align="center"><img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/raspberry_logo.png" height="220" alt=" " /></p>
<br>
<h1 align="center">Raspberry Pi Guide</h1> 
<h4 align="right">Aug 22</h4>

<img src="https://img.shields.io/badge/OS%20-Raspbian%20GNU%2FLinux%2011%20(bulleye)-yellowgreen">
<img src="https://img.shields.io/badge/Hardware-Raspberry%20ver%203 & 4-red">

<br>

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Updating](#updating)
- [Raspberry Pi elimina la contraseña por defecto para máxima seguridad](#raspberry-pi-elimina-la-contraseña-por-defecto-para-máxima-seguridad)
  - [08 de abril, 2022.](#08-de-abril-2022)
- [Headless Raspberry Pi SSH WiFi Setup](#headless-raspberry-pi-ssh-wifi-setup)
  - [Firmware with SSH/VNC/Wi-Fi-SSID-PASSWORD/HOSTNAME from started.  Acceder a RPI sin  ni Mouse](#firmware-with-sshvncwi-fi-ssid-passwordhostname-from-started--acceder-a-rpi-sin--ni-mouse)
  - [Otras Opciones](#otras-opciones)
  - [Editing Wi-Fi on a Prewritten Card](#editing-wi-fi-on-a-prewritten-card)
  - [Habilitar SSH RPi en el arranque sin usar un Monitor](#habilitar-ssh-rpi-en-el-arranque-sin-usar-un-monitor)
  - [Configurar el Resto de Opciones](#configurar-el-resto-de-opciones)
  - [Encontrar la dirección IP Raspberry Pi](#encontrar-la-dirección-ip-raspberry-pi)
  - [Conexión Ethernet directa](#conexión-ethernet-directa)
  - [Conexión USB directa (solo Pi Zero / Zero W)](#conexión-usb-directa-solo-pi-zero--zero-w)
- [How to Find your IP Address](#how-to-find-your-ip-address)
- [IP Address Local](#ip-address-local)
- [Ethernet MAC address](#ethernet-mac-address)
- [Enabling SSH RPi](#enabling-ssh-rpi)
- [SSH Shell desde Linux](#ssh-shell-desde-linux)
  - [Mac o Windows OS](#mac-o-windows-os)
- [Setup a Static IP Address](#setup-a-static-ip-address)
  - [Terminal Method](#terminal-method)
    - [Install from RASPI-CONFIG](#install-from-raspi-config)
    - [Install from CONSOLE](#install-from-console)
    - [Enable Network Manager/ Start Network Manager/ Verify the Status](#enable-network-manager-start-network-manager-verify-the-status)
    - [(Optional) Disable the Default dhcpcd Service](#optional-disable-the-default-dhcpcd-service)
    - [Run](#run)
    - [Going back to non static IP](#going-back-to-non-static-ip)
  - [ip static Rasbian dhcpcd method](#ip-static-rasbian-dhcpcd-method)
  - [Conectarse a una RPi con IP estatica en Eth0 desde Windows](#conectarse-a-una-rpi-con-ip-estatica-en-eth0-desde-windows)
- [Adding Multiple Wireless Network Configurations](#adding-multiple-wireless-network-configurations)
  - [Tener configurado multiples Redes WiFi en RPi](#tener-configurado-multiples-redes-wifi-en-rpi)
  - [Otros parametros](#otros-parametros)
- [Copying Files to your Raspberry Pi from SSH](#copying-files-to-your-raspberry-pi-from-ssh)
  - [Copying Files from your Raspberry Pi](#copying-files-from-your-raspberry-pi)
  - [Copying Multiple Files](#copying-multiple-files)
  - [Copying a Whole Directory](#copying-a-whole-directory)
- [Habilitación y conexión a través de VNC](#habilitación-y-conexión-a-través-de-vnc)
- [Run a Program On Your Raspberry Pi At Startup](#run-a-program-on-your-raspberry-pi-at-startup)
  - [**(rc.local)**](#rclocal)
    - [Debugging](#debugging)
    - [Cómo detener su programa](#cómo-detener-su-programa)
  - [**.bashrc**](#bashrc)
  - [**(init.d)**](#initd)
- [Daemon Service SYSTEMD](#daemon-service-systemd)
    - [Unit File (No GUI)](#unit-file-no-gui)
  - [Unit File (GUI)](#unit-file-gui)
  - [Troubleshooting](#troubleshooting)
  - [Debugging](#debugging-1)
  - [Logging to a File](#logging-to-a-file)
  - [Use a Specific Version of Python](#use-a-specific-version-of-python)
  - [Checking the Service](#checking-the-service)
  - [Starting and Stopping the Service](#starting-and-stopping-the-service)
  - [How to Stop Your Program from Running on Boot](#how-to-stop-your-program-from-running-on-boot)
  - [Sample: Create A Unit File](#sample-create-a-unit-file)
  - [Configure systemd](#configure-systemd)
- [Systemd Commands Summary (administrador del sistema y servicios)](#systemd-commands-summary-administrador-del-sistema-y-servicios)
- [Para saber que modelo de raspberry](#para-saber-que-modelo-de-raspberry)
- [Memoria free](#memoria-free)
- [Poner hora en la RPi desde la consola](#poner-hora-en-la-rpi-desde-la-consola)
- [Setting LCD Touch on Raspberry](#setting-lcd-touch-on-raspberry)
  - [Setting](#setting)
  - [Instalacion de driver para LCD 3.5" 480×320 ~ 1920×1080(dots)](#instalacion-de-driver-para-lcd-35-480320--19201080dots)
    - [otras LCD](#otras-lcd)
  - [Instalacion de driver para LCD 7" 800 × 480 ~ 1920x1080](#instalacion-de-driver-para-lcd-7-800--480--1920x1080)
    - [Setting](#setting-1)
      - [Resource](#resource)
- [Visual Code On Raspberry](#visual-code-on-raspberry)
- [Raspberry Pi Compute Module 4 RPI CM4](#raspberry-pi-compute-module-4-rpi-cm4)
- [Flashing RPi CM4 with eMMC on Windows](#flashing-rpi-cm4-with-emmc-on-windows)
  - [Pasos](#pasos)
  - [Referencias:](#referencias)
- [CM4 Dual Eth mini Board](#cm4-dual-eth-mini-board)
- [Desactivar Screen Saver Raspbian](#desactivar-screen-saver-raspbian)
- [Abrir el browser al iniciar raspberry](#abrir-el-browser-al-iniciar-raspberry)
- [Start chromium browser from the terminal](#start-chromium-browser-from-the-terminal)
- [Scan Serial Port](#scan-serial-port)
- [Scan port USB](#scan-port-usb)
- [Error puerto](#error-puerto)
  
<br>

more: https://www.raspberrypi.com/documentation/computers/configuration.html#conclusion

<br>

# Updating

```
sudo apt-get update && sudo apt-get dist-upgrade -y
```
```sudo apt-get update```  Actualiza el listado con todos los paquetes que tenemos disponibles para instalar.

```sudo apt-get dist-upgrade -y``` Actualiza los paquetes que tenemos instalados con los programas y si hay algún paquete del sistema operativo, también lo actualiza. ```-y``` Supone una respuesta afirmativa a todas las preguntas, de esta forma ```apt-get``` se ejecuta sin necesidad de intervención posterior para tomar decisione


> :warning: Solo se actualizarían los programas, pero no el sistema operativo.
```
sudo apt-get upgrade 
```

> :warning: Actualizar el firmware. Este paso solo es necesario hacerlo cuando sea estrictamente necesario.
```
sudo rpi-update 
```
> :bulb: **Tip:** Siempre es recomendable reiniciar después de una actualización.
```
sudo reboot
```
<br>

# Raspberry Pi elimina la contraseña por defecto para máxima seguridad
## 08 de abril, 2022.
Nuevas leyes 2022 prohíben que cualquier dispositivo conectado a Internet tenga credenciales de inicio de sesión predeterminadas. La última versión del sistema operativo Raspberry Pi elimina el nombre de usuario **pi** predeterminado y un nuevo asistente obliga al usuario a crear un nombre de usuario en el primer arranque de una imagen del sistema operativo Raspberry Pi recién flasheada, aunque son conscientes de posibles incompatibilidades sobre todo al comienzo del cambio.

Raspberry Pi todavía permitirá a los usuarios establecer el nombre de usuario en **pi** y la contraseña en **raspberry**, pero emitirá una advertencia de que elegir los valores predeterminados no es aconsejable.

<br>

# Headless Raspberry Pi SSH WiFi Setup 
## Firmware with SSH/VNC/Wi-Fi-SSID-PASSWORD/HOSTNAME from started.  Acceder a RPI sin  ni Mouse

from Raspberry Pi Imager (https://www.raspberrypi.com/software/) 

con ```CTRL + Shift + X``` se abre el menú Advanced options, habilitamos:

- Set hostname
- Enable SSH
- Set usename and password
- Configure wiewless LAN
- Wireless LAN  country

```Save & Write```

> :memo: **Note:** Hay que tomar en cuenta que si la contraseña ```raspberry``` con el nombre de usuario ```pi```, puede recibir un mensaje de advertencia cuando inicie sesión, recomendándole (pero no obligándolo) que cambie la contraseña.

<br>

## Otras Opciones
___
## Editing Wi-Fi on a Prewritten Card 
Si no se agregó la configuración de la red Wifi en Raspberry Pi Imager, se puede hacer desde un archivo de configuración colocado en la partición Boot de la SD. Esto se puede hacer sin conectar una pantalla ni un teclado al Pi.

Se necesita abrir la tarjeta microSD en la PC y Luego crear un archivo de texto llamado ```wpa_supplicant.conf``` y colóquelo en el directorio raíz (BOOT) de la tarjeta microSD: 

```
country=CL
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
scan_ssid=1
ssid="your_wifi_ssid"
psk="your_wifi_password"
}
```
Sin embargo, si está en una red Wi-Fi pública que requiere que haga clic en "Aceptar" en una página de bienvenida antes de conectarse a Internet, este método no funcionará.

¿Preferimos usar Ethernet? Si conectamos Raspberry Pi directamente a una red cableada, debería poder acceder a ella por su nombre ```raspberrypi o raspberrypi.local``` sin cambiar ningún otro archivo.
<br>

## Habilitar SSH RPi en el arranque sin usar un Monitor
Acceder a la tarjeta microSD en la que se instaló Raspbian desde un ordenador externo y crear un archivo llamado ```ssh``` en el directorio de arranque **BOOT** (FAT32) partition of the SD card (boot folder). En este caso, es importante que ```no utilices una extensión de archivo``` y que te asegures de que esta no se ha añadido automáticamente como sucede a menudo en Windows. Si reinicias la RPi, el acceso SSH estará habilitado.

Desde la consola podemos crear el archivo SSH. En la unidad BOOT de la SD.

Desde Windows
```
type nul > ssh
```
Desde linux 
```
touch ssh
```

## Configurar el Resto de Opciones
Una vez que tenemos acceso SSH a Raspberry Pi ya podemos configurar el resto de opciones de forma habitual usando ```raspi-config```. También es posible activar el **VNC server** en la RPI.

<br>

## Encontrar la dirección IP Raspberry Pi
Podemos probar varias opciones:<br>
- Intentar conectar usando ```raspberrypi.local```. Probar con ```ping raspberrypi.local```.
- **IP Scanner**: https://www.advanced-ip-scanner.com/es/ (Windows) ```-Mejor Opción-```<br>
- Buscar la IP del dispositivo accediendo a la configuración del Router.
- Usar un programa de escáner de IPs en la red como, por ejemplo:<br>
**IP Scan**: https://www.mediafire.com/file/lzxseb45ej9mr97/ipscan.rar/file (Windows)<br>

**Fing** (Android)

💡 Tip: Desde el shell de Windows (funciona en redes pequeñas):
```
arp -a
```
lista las IP activas. Solo se muestra las IP y no su Hostname


## Conexión Ethernet directa
Solo asegúrate de tener Bonjour instalado en su PC y SSH habilitado en el Pi (ver arriba). Luego, puede simplemente conectar los dos dispositivos a través de Ethernet.

1. Navega hasta el menú Conexiones de red /Control Panel\Network and Internet\Network Connections/ en ```WiFI``` botón derecho (Propiedades) 
2. Habilitar "Permitir que otros usuarios de la red se conecten" en la pestaña "Compartir"
3. Seleccionar el puerto Ethernet que está conectado a la Raspberry Pi en el menú "Conexión de red doméstica" y haga clic en Aceptar.

<br>

## Conexión USB directa (solo Pi Zero / Zero W)
Este método es excelente porque funciona sin importar dónde se encuentre (incluso si no hay Wi-Fi disponible) y proporciona energía y una conexión a Pi, a través de un solo cable. Sin embargo, solo puede hacer esto en un Pi Zero o Zero W:

1. Necesitamos abrir el archivo ```config.txt``` en el directorio raíz de la tarjeta micro SD y agregar la línea ```dtoverlay=dwc2``` al final del archivo y guárdelo.

2. Necesitamos abrir el ```cmdline.txt``` y agregar el texto ```modules-load=dwc2,g_ether``` después de la palabra ```rootwait``` y guardar el archivo. No hay saltos de línea en este archivo.
   
3. Necesitamos descargue e instale los servicios de impresión de ```Bonjour``` de apple.com **(si tiene Windows)**. Esto ayuda a que tu PC vea la RPi.
4. Conectamos el cable micro USB al puerto con la etiqueta "USB" en el Pi Zero. Esto no funcionará si se conecta al puerto con la etiqueta "PWR". Sin embargo, el puerto "USB" también suministrará energía a su Pi, por lo que no necesita conectar un cable de alimentación dedicado. 


<br>

More inf: https://desertbot.io/blog/headless-raspberry-pi-4-ssh-wifi-setup

<br>


# How to Find your IP Address
test connection in the same net:
```
ping raspberrypi.local
```

# IP Address Local 
```
hostname -I
```

# Ethernet MAC address
```
ethtool -P eth0
```
<br>


# Enabling SSH RPi

Raspberry Pi OS has the SSH server disabled by default. It can be enabled manually from the desktop:

1. Launch Raspberry Pi Configuration from the Preferences menu
2. Navigate to the Interfaces tab
3. Select Enabled next to SSH
4. Click OK

Alternatively you can enable it from the terminal using the raspi-config application,

1. Enter sudo raspi-config in a terminal window
2. Select Interfacing Options
3. Navigate to and select SSH
4. Choose Yes
5. Select Ok
6. Choose Finish

<br>

# SSH Shell desde Linux
## Mac o Windows OS
```
ssh pi@<IP>
ssh <USER>@<IP-ADDRESS> 
e.g. pi@192.168.1.10
e.g. eben@192.168.1.5
```
Next you will be prompted for the password for the pi login: the default password on Raspberry Pi OS is raspberry. 

<br>

<br>

# Setup a Static IP Address
## Terminal Method

Se usa un cable de red punto a punto a la RPI, sirve para configurar la SSID y PSK en la RPI cuando no hay monitor ni teclado por ejemplo.

***Opcion 1 with Network Manager in Terminal Tool (nmtui)*** <br>

> [!WARNING]
> If your system doesn't have nmtui package installed, you may install it. (con sistema BOOKWORM no require instalacion)

### Install from RASPI-CONFIG

<p align="center"><img src="./img/rc1.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/rc2.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/rc3.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/rc4.png" height="350" alt=" " /></p>

After installing, you might need to reboot your Raspberry Pi for the changes to take effect: 
```
sudo reboot
```

<br>

### Install from CONSOLE
```
sudo apt update && sudo apt install network-manager
```

### Enable Network Manager/ Start Network Manager/ Verify the Status
```
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager
sudo systemctl status NetworkManager
```

### (Optional) Disable the Default dhcpcd Service
Raspberry Pi OS uses dhcpcd by default for network management. You may want to disable it to prevent conflicts with Network Manager:
```
sudo systemctl disable dhcpcd && sudo systemctl stop dhcpcd
```

After installing, you might need to reboot your Raspberry Pi for the changes to take effect: 
```
sudo reboot
```

<br>

### Run 
```
sudo nmtui
```

<p align="center"><img src="./img/nm1.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/nm2.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/nm3.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/nm4.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/nm5.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/nm6.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/nm7.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/nm8.png" height="350" alt=" " /></p>


Restart your Pi for the changes to take effect. You have successfully set up static IP on Raspberry Pi.

### Going back to non static IP
How? Simply edit the network connection in question again. This time, change the IPv4 configuration to 'automatic' and save your changes. And that's it. You don't have to provide IP address, gateway IP etc anymore


<br>

***Option 2***
## ip static Rasbian dhcpcd method 

> :bulb: **Tip:** hay acceso a internet desde la ip ```Ethernet``` y si desde la ip ```WiFi``` siempre que este configurada la red Wifi. Sino hay que reload el adaptador de red.

Here is an example which configures a static address, routes and dns.
```
sudo nano /etc/dhcpcd.conf
```
```
# carjavi static IP eth0 configuration:
interface eth0
static ip_address=192.168.2.2/24
#static ip6_address=fd51:42f8:caae:d92e::ff/64
static routers=192.168.2.1
static domain_name_servers=192.168.2.1 8.8.8.8 
```

```
# wlan static ip
interface wlan0
static ip_address=192.168.1.200/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8
```

Where,

```interface``` = Name of the interface we want to configure <br>
```static ip_address``` = Fixed address we want (leave the /24 at the end)
static routers = Gateway address (router)<br>
```static domain_name_servers``` = DNS server address (usually that of the router, or external ones like Google’s 8.8.8.8). If you want more than one DNS server, you can add them separated by a space.<br>

you need:
```
sudo reboot
```

> :warning: **Warning:** para conectarse a la RPI desde el computador primero se debe poner el computador en la misma red.

info: https://raspberrypi.stackexchange.com/questions/37920/how-do-i-set-up-networking-wifi-static-ip-address-on-raspbian-raspberry-pi-os/74428#74428

## Conectarse a una RPi con IP estatica en Eth0 desde Windows
En este caso la RPi tiene como IP fija: ```192.168.2.2```, Bastara con estar en la misma sub red para poder tener conexión con este dispositivo.

<p align="center"><img src="./img/ip-static_1.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/ip-static_2.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/ip-static_3.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/ip-static_4.png" height="350" alt=" " /></p>
<p align="center"><img src="./img/ip-static_5.png" height="350" alt=" " /></p>

<br>

# Adding Multiple Wireless Network Configurations
## Tener configurado multiples Redes WiFi en RPi 

```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

Sample:

```
country=CL
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="carjavi"
    psk=d0611293f3e612439a6db28f18d59333e2274117902a95e85503bc2b2a8f895a
    id_str="main"
    priority=1
}

network={
    ssid="MQT"
    psk="password"
    key_mgmt=WPA-PSK
    id_str="work"
    priority=2
}
```

```country=CL```  Donde el código de país debe establecerse el código de dos letras ISO/IEC alpha2 para el país en el que está utilizando.<br>

```priority=<numero>``` A mayor valor de la prioridad se conectará primero a esa red wifi antes que a otra con menor valor.<br>

```id_str="<nombre>"``` Esta cadena se utiliza en ```/etc/network/interfaces``` como identificador de interfaz virtual. Esto permite crear bloques de configuración específicos para cada red.<br>

## Otros parametros
```key_mgmt=WPA-PSK```  list of accepted authenticated key management protocols.<br>
```scan_ssid=1``` SSID scan technique; 0 (default) or 1.<br>
```ap_scan=1```<br>
```pairwise=CCMP```<br>
```auth_alg=OPEN```<br>

<br>

# Copying Files to your Raspberry Pi from SSH
```
scp myfile.txt pi@192.168.1.3:
```
Copy the file to the /home/pi/project/ directory on your Raspberry Pi (the project folder must already exist):
```
scp myfile.txt pi@192.168.1.3:project/
```
## Copying Files from your Raspberry Pi
Copy the file myfile.txt from your Raspberry Pi to the current directory on your other computer:
```
scp pi@192.168.1.3:myfile.txt .
```
## Copying Multiple Files
```
scp myfile.txt myfile2.txt pi@192.168.1.3:
scp *.txt pi@192.168.1.3:
scp m* pi@192.168.1.3:
scp m*.txt pi@192.168.1.3:
```

## Copying a Whole Directory
Copy the directory project/ from your computer to the pi user’s home folder of your Raspberry Pi at the IP address 192.168.1.3
```
scp -r project/ pi@192.168.1.3:
```
<br>

# Habilitación y conexión a través de VNC
```
sudo raspi-config
```
Interfacing Options / VNC / enabled ? YES Finish

<br>

# Run a Program On Your Raspberry Pi At Startup
## **(rc.local)**
This is especially useful if you want to power up your Pi  without a connected monitor, and have it run a program without configuration or a manual start.

1.  permiso de ejecución al archivo
```
    $ sudo chmod +x fichero.py
```
2. sudo nano /etc/rc.local
```
...
python3 /home/pi/fichero.py
/usr/bin/python3 /home/pi/example.py
node /home/pi/fichero.js
sudo bash /home/pi/di_update/Raspbian_For_Robots/upd_script/rc.sh

exit 0
```   
**Nota:** si programa debe devolver el control al script o la Raspberry Pi nunca podrá terminar de arrancar. Si su programa realiza un bucle infinito, debe ejecutarlo en segundo plano agregando un & después de ordenar. En nuestro caso esto daría:
```
/usr/bin/python3 /home/pi/example.py &
```
### Debugging
Es posible que observe que no ve ningún error o resultado de su secuencia de comandos, ya que rc.local no registra ni genera ninguna información. Para obtener eso, cambie la llamada de python en su archivo rc.local a lo siguiente:
```
sudo bash -c 'python /home/pi/blink.py > /home/pi/blink.log 2>&1' &
```
Esto crea un nuevo shell con sudo (privilegios de superusuario), ejecuta su secuencia de comandos y redirige la salida (stdout) al archivo blink.log. 2>&1 Dice que los errores (stderr) también deben redirigirse al mismo archivo de registro. Al reiniciar, cualquier resultado de su secuencia de comandos de Python (por ejemplo, declaraciones de impresión ()), así como los errores, deben guardarse en blink.log. Para ver el registro, ingrese lo siguiente en una terminal (tenga en cuenta que es posible que primero deba detener su programa para ver el contenido del archivo de registro):
```
cat blink.log
```
Resulta que rc.local se ejecuta antes que .bashrc, por lo que el comando python todavía se refiere a Python 2 en nuestro script de inicio. Para llamar explícitamente a Python 3, debemos cambiar nuestro comando rc.local a:
```
sudo bash -c '/usr/bin/python3 /home/pi/blink.py > /home/pi/blink.log 2>&1' &
```
### Cómo detener su programa
Puede notar que su programa funciona muy bien, ¡pero no hay una manera fácil de detenerlo! El método más simple sería eliminar (o comentar) la línea que agregó en rc.local seguido de un reinicio, pero eso lleva mucho tiempo.

La forma más rápida de detener su programa es matar su proceso de Linux. En una terminal, ingresa el siguiente comando:
```
sudo ps -ax | grep python
```
ps -ax le dice a Linux que enumere todos los procesos actuales. Canalizamos esa lista a grep, lo que nos permite buscar palabras clave. Estamos buscando python en este ejemplo, pero siéntase libre de cambiarlo por el nombre de su programa o lo que esté usando para ejecutar su programa. Busque el número de ID del proceso (PID) a la izquierda del proceso enumerado y use el comando kill para finalizar ese proceso:
```
sudo kill <PID>
```

<br>



## **.bashrc**
rc.local es un buen lugar para iniciar su programa cada vez que se inicia el sistema (antes de que los usuarios puedan iniciar sesión o interactuar con el sistema). Si desea que su programa se inicie cada vez que un usuario inicie sesión o abra una nueva terminal, considere agregar una línea similar a /home/pi/.bashrc.

The second method to run a program on your Raspberry Pi at startup is to modify the .bashrc  file. With the .bashrc method, your python program will run when you log in (which happens automatically when you boot up and go directly to the desktop) and also every time when a new terminal is opened, or when a new SSH connection is made. Put your command at the bottom of ‘/home/pi/.bashrc’. The program can be aborted with ‘ctrl-c’ while it is running!
```
sudo nano /home/pi/.bashrc
```
Go to the last line of the script and add:
```
echo Running at boot 
sudo python /home/pi/sample.py
```
```
sudo reboot
```

## **(init.d)**
/etc/init.d directory.  This directory contains the scripts which are started during the boot process (in addition, all programs here are  executed when you shutdown or reboot the system).

Add the program to be run at startup to the init.d directory using the following lines:
```
sudo cp /home/pi/sample.py /etc/init.d/
```
Move to the init directory and open the sample script
```
cd /etc/init.d
sudo nano sample.py

# /etc/init.d/sample.py
### BEGIN INIT INFO
# Short-Description: Start daemon at boot time
# Description:       Enable service provided by daemon.
### END INIT INFO
```
info: https://wiki.debian.org/LSBInitScripts

```
sudo chmod +x sample.py
sudo update-rc.d sample.py defaults
sudo reboot
```

<br>

# Daemon Service SYSTEMD

systemd es el método preferido para iniciar aplicaciones al inicio, pero también es uno de los más complicados de usar. Con systemd, tiene la ventaja de poder decirle a Linux que inicie ciertos programas solo después de que se hayan iniciado ciertos servicios. Como resultado, es una herramienta muy robusta para inicializar sus scripts y aplicaciones.

**Unit File** es un archivo de texto sin formato que brinda información a systemd sobre un servicio, dispositivo, punto de montaje, etc.

### Unit File (No GUI)
Si su programa no requiere una GUI entonces puede usar la siguiente plantilla para crear un servicio systemd:
```
sudo nano /lib/systemd/system/blink.service

[Unit]
Description=Blink my LED
After=multi-user.target

[Service]
ExecStart=/usr/bin/python3 /home/pi/blink.py

[Install]
WantedBy=multi-user.target
```
**Description** Descripción

**After** indica cuándo debe ejecutarse nuestro programa.

**multi-user.target** es el estado del sistema en el que el control se otorga al usuario (un "shell multiusuario") pero antes de que se inicie el sistema X Windows. ¡Eso significa que nuestro programa se ejecutará incluso sin iniciar sesión! Puede cambiar esto, según los servicios que necesite activar antes de ejecutar su programa (por ejemplo, network.target si necesita redes).
para mas information: https://www.freedesktop.org/software/systemd/man/systemd.special.html

**Service**  especificamos algunas variables de entorno.

**ExecStart** es el comando (o conjunto de comandos) que se utiliza para iniciar nuestro programa. Tenga en cuenta que estamos usando rutas absolutas a la versión de Python que queremos, así como la ubicación de nuestro programa.

**WantedBy** en la sección **Install**  especifica el objetivo con el que queremos que se incluya nuestro servicio. En este ejemplo, queremos que nuestro servicio se ejecute cuando se ejecute la unidad multi-user.target (o, más específicamente, justo después, según el parámetro After).

Necesitamos decirle a systemd que reconozca nuestro servicio, así que ingrese:
```
sudo systemctl daemon-reload
```
Tenga en cuenta que deberá ingresar este comando cada vez que cambie su archivo .service, ya que systemd necesita saber que se ha actualizado.

Luego, debemos decirle a systemd que queremos que nuestro servicio se inicie en el arranque, así que ingrese:
```
sudo systemctl enable blink.service
```
Reboot con 
```
sudo reboot
```

## Unit File (GUI)
Si su programa requiere componentes gráficos (como en nuestro ejemplo clock.py), se recomienda la siguiente plantilla para crear un servicio systemd.

Cree un nuevo archivo .service en el directorio systemd:
```
sudo nano /lib/systemd/system/clock.service

[Unit]
Description=Start Clock

[Service]
Environment=DISPLAY=:0
Environment=XAUTHORITY=/home/pi/.Xauthority
ExecStart=/usr/bin/python3 /home/pi/clock.py
Restart=always
RestartSec=10s
KillMode=process
TimeoutSec=infinity

[Install]
WantedBy=graphical.target
```
Queremos conectarnos a nuestra pantalla principal (esto supone que solo una pantalla está conectada a nuestra Pi), por lo que configuramos DISPLAY en: 0 y le indicamos a nuestra aplicación dónde encontrar las credenciales necesarias para usar el sistema X windows con XAUTHORITY. ExecStart es el comando que queremos ejecutar (iniciar nuestro programa de reloj de Python, en este caso).

Desafortunadamente, con systemd, no podemos decir exactamente cuándo se iniciará el sistema X, y no podemos garantizar necesariamente que un usuario inicie sesión (a menos que haya habilitado el inicio de sesión automático con sudo raspi-config). Para dar cuenta de esto, aplicaremos fuerza bruta a nuestro programa para que se reinicie (con Reiniciar) cada 10 segundos (con RestartSec) si falla o se cierra. KillMode le dice a systemd que elimine cualquier proceso asociado con nuestro programa si el servicio falla (o se cierra), y TimeoutSec=infinity significa que nunca queremos dejar de intentar ejecutar nuestro programa.

Necesitamos decirle a systemd que reconozca nuestro servicio, así que ingrese:
```
sudo systemctl daemon-reload
```
Tenga en cuenta que deberá ingresar este comando cada vez que cambie su archivo .service, ya que systemd necesita saber que se ha actualizado.

Luego, debemos decirle a systemd que queremos que nuestro servicio se inicie en el arranque, así que ingrese:
```
sudo systemctl enable clock.service
```
Reboot con 
```
sudo reboot
```

## Troubleshooting
No pasa nada. Si su programa no parece ejecutarse en el arranque, pueden estar sucediendo varias cosas. Para obtener información sobre el servicio systemd, intente registrar la salida en un archivo o verificar el estado del servicio.
## Debugging
La salida de systemd (por ejemplo, sentencias print() o mensajes de error) es capturada por el sistema journalctl y se puede ver con el siguiente comando:
```
journalctl -u clock.log
```
Esto puede dar una idea de lo que está pasando con su servicio o programa.
## Logging to a File
Si journalctl no está a la altura de sus expectativas, puede intentar registrar la salida en un archivo. Para hacer eso, cambie la llamada ExecStart a lo siguiente (usando clock.py como ejemplo):
```
ExecStart=/bin/bash -c '/usr/bin/python3 /home/pi/clock.py > /home/pi/clock.log 2>&1'
```
Esto inicia un nuevo shell bash, ejecuta su programa y redirige la salida (stdout) a un nuevo archivo de texto clock.log. El comando 2>&1 dice que cualquier error (stderr) también debe redirigirse (escribirse en) el mismo archivo de registro. Cualquier resultado (p. ej., de los comandos print() de Python) o errores se guardarán en clock.log. Puede ver el registro con el siguiente comando (tenga en cuenta que es posible que deba detener el servicio y el programa antes de ver el registro):
```
cat clock.log
```
## Use a Specific Version of Python
Debido a que su archivo de unidad systemd probablemente se ejecutará antes de que .bashrc pueda convertir el comando python en Python 3, es posible que deba llamar explícitamente al comando python3. Para hacer eso, solo asegúrese de que su llamada a Python sea una ubicación de archivo absoluta, por ejemplo, /usr/bin/python3.
## Checking the Service
Si sospecha que su servicio no se está ejecutando, es posible que desee verificar el estado del mismo. Para hacer eso, ingrese el siguiente comando:
```
systemctl status clock.service
```

## Starting and Stopping the Service
```
sudo systemctl stop clock.service
sudo systemctl start clock.service
```
Esto puede ser útil para reiniciar un servicio si ha realizado cambios sin tener que reiniciar el sistema. ¡Solo recuerde ejecutar sudo systemctl daemon-reload si realiza algún cambio en un archivo .service!

## How to Stop Your Program from Running on Boot
```
sudo systemctl disable clock.service
```
Tenga en cuenta que no es necesario que elimine el archivo .service, ya que deshabilitarlo evitará que se ejecute al inicio. Sin embargo, si desea eliminar el archivo, puede usar los siguientes comandos (una vez más, reemplazando clock.service con el nombre de archivo de su servicio):
```
sudo rm /lib/systemd/system/clock.service
sudo systemctl daemon-reload
```


## Sample: Create A Unit File 
```
sudo nano /lib/systemd/system/sample.service

 [Unit]
 Description=My Sample Service
 After=multi-user.target

 [Service]
 Type=idle
 ExecStart=/usr/bin/python /home/pi/sample.py

 [Install]
 WantedBy=multi-user.target
```
This defines a new service called “Sample Service” and we are requesting that it is launched once the multi-user environment is available. The “ExecStart” parameter is used to specify the command we want to run. The “Type” is set to “idle” to ensure that the ExecStart command is run only when everything else has loaded. Note that the paths are absolute and define the complete location of Python as well as the location of our Python script.

In order to store the script’s text output in a log file you can change the ExecStart line to:
```
ExecStart=/usr/bin/python /home/pi/sample.py > /home/pi/sample.log 2>&1
```
The permission on the unit file needs to be set to 644 :
```
sudo chmod 644 /lib/systemd/system/sample.service
```
## Configure systemd
Now the unit file has been defined we can tell systemd to start it during the boot sequence :
```
sudo systemctl daemon-reload
sudo systemctl enable sample.service
```
Reboot the Pi and your custom service should run:
```
sudo reboot
```

otro ejemplo: 
```
sudo nano /lib/systemd/system/sample.service
```

```
sudo nano /lib/systemd/system/sample.service

[Unit]
Description=InicioPython
After=multi-user.target
[Service]
Type=idle
ExecStart=/usr/bin/python3 /home/pi/myphython.py &
Restart=always
User=pi
[Install]
WantedBy=multi-user.target

```

```
$ sudo systemctl daemon-reload
$ sudo systemctl enable sample.service
$ sudo systemctl status sample.service
```

more information : https://www.dexterindustries.com/howto/run-a-program-on-your-raspberry-pi-at-startup/

https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files

<br>

# Systemd Commands Summary (administrador del sistema y servicios)
```
$ systemctl status   //Show system status using  (General)
$ systemctl  //List running units 
$ systemctl –failed // List failed
$ systemctl list-unit-files // List installed unit files
# systemctl start unit //Start a unit immediately
# systemctl stop unit //Stop a unit immediately
# systemctl restart unit //Restart a unit
# systemctl reload unit  //Ask a unit to reload its configuration
$ systemctl status unit //Show the status of a unit
# systemctl enable unit  //Enable a unit to be started on bootup
# systemctl disable unit //Disable a unit to not start during bootup
# systemctl mask unit  //Mask a unit to make it impossible to start it
# systemctl unmask unit  // Unmask a unit
# systemctl daemon-reload  //Reload systemd, scanning for new or changed units
$ systemctl reboot  //Shut down and reboot the system
$ systemctl poweroff   //Shut down and power-off the system
$ systemctl hibernate  //Put the system into hibernation
$ systemctl hybrid-sleep


examples:
sudo systemctl daemon-reload
sudo systemctl enable systemd-networkd
sudo systemctl disable clock.service
sudo systemctl status clock.service
sudo systemctl stop clock.service
sudo systemctl start clock.service
sudo systemctl restart <<service-name>>

```
<br>

# Para saber que modelo de raspberry
```
cat /proc/cpuinfo | grep Models
```

# Memoria free
```
free -m
```


# Poner hora en la RPi desde la consola
```
sudo date 08050822
```
donde: <br>
08 es el mes<br>
05 es el día<br>
08 es la hora<br>
22 son los minutos

<br>

# Setting LCD Touch on Raspberry
wiki: http://www.lcdwiki.com/3.5inch_HDMI_Display-B

## Setting

```
sudo rm -rf LCD-show
git clone https://github.com/goodtft/LCD-show.git
chmod -R 755 LCD-show
cd LCD-show/
```

##  Instalacion de driver para LCD 3.5" 480×320 ~ 1920×1080(dots)
<p align="center">
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/RPI-3-inch.jpg" height="300" alt="www.instintodigital.net">
   
</p>

```
sudo ./MPI3508-show // 3.5” HDMI Display-B(MPI3508)
```

### otras LCD 
```
sudo ./LCD35-show // 3.5” RPi Display(MPI3501)
sudo ./LCD24-show // 2.4” RPi Display (MPI2401)
sudo ./LCD24-3A+-show // 2.4” RPi Display For RPi 3A+ (MPI2411)
sudo ./LCD28-show // 2.8” RPi Display (MPI2801)
sudo ./LCD32-show // 3.2” RPi Display (MPI3201)
```
https://github.com/goodtft/LCD-show
http://www.lcdwiki.com/3.5inch_HDMI_Display-B

> :warning: **Warning:** si no funciona el touch puedes tener el driver equivocado.

##  Instalacion de driver para LCD 7" 800 × 480 ~ 1920x1080

<p align="center">
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/RPI-7-inch-model-f.png" height="300" alt="www.instintodigital.net"><br>
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/RPI-7-inch-model-b.png" height="360" alt="www.instintodigital.net">
   
</p>

### Setting
1. Edit  ```config.txt``` file
```
sudo nano /boot/config.txt
```
add the following code at the end of the file:
```
max_usb_current=1
hdmi_force_hotplug=1
config_hdmi_boost=7
hdmi_group=2
hdmi_mode=87
hdmi_drive=1
hdmi_cvt 800 480 60 6 0 0 
```
2. Save & reboot


> :memo: **Note:** Si no hay video verificar que el swith de backlight en la parte trasera este en ON.

#### Resource
http://www.lcdwiki.com/7inch_HDMI_Display-B<br>
http://www.lcdwiki.com/res/MPI7001/7inch_HDMI_Display-B_User_Manual(En).pdf

<br>

# Visual Code On Raspberry

Visual Code ver 1.55.0 amd64.deb

<img  align="middle" width="32" height="32" src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/vcode.svg"> [visual-code-v1.55.0.deb](https://www.mediafire.com/file/r29ir46aun9ot81/visualcode_1.55.0-1617120720_amd64.deb/file)

<br>

# Raspberry Pi Compute Module 4 RPI CM4

<p align="center">
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/132984509.webp" height="200" alt="www.instintodigital.net">
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/CM4-Component-Identification-1.png" height="300" alt="www.instintodigital.net">
</p>

# Flashing RPi CM4 with eMMC on Windows 

> :warning: **Warning:** No funciona para RPi CM4 lite (no posee el eMMC), tiene otro procedimiento.
no se necesita una SD-ext en la placa base (se usa el eMMC).

## Pasos

1. Ponemos el swich Boot en On para que arranque desde USB (debe ser un OTG cable) 
2. Conectamos al PC (en Control Panel/System/Device encontraremos un dispositivo BCM2711 Boot)
3. Correr [rpiboot.exe](https://www.mediafire.com/file/bo6gg4sxd9rkk95/Rpiboot_setup.zip/file) como administrator (esto flashea la eMMC del modulo)
4. Se abre el [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
	* Seleccionar Storage: eMMC RPi-MSD-0001 - 31.3GB
	* Choose OS/Erase FAT32 
	* Habilitamos SSH, SSID-PASSWORD, VNC
	* Escribimos OS
5. Al terminar de instalar OS cerramos RaspberryPi-Imager y quitamos cable USB
6. Pasamos el swith BOOT a off (para que inicie desde la eMMC) 
7. Ready!
8. Update & Upgrade

```
sudo apt-get update && sudo apt-get dist-upgrade -y
```
<br>

> :memo: **Note:** 
l USB Port esta desabilitado por default para ahorrar energia. para habilitarlo
se edita el config.txt y agregar:
```
sudo nano /boot/config.txt
```
add the following code at the end of the file
```
  dtoverlay=dwc2,dr_mode=host
```
> :memo: **Note:** Solo esta habilitado un solo puerto Ethernet por default, el Eth port de la esquina. 

## Referencias:
Documentation
https://www.raspberrypi.com/documentation/computers/compute-module.html

flashing RPi CM4
https://www.waveshare.com/wiki/Write_Image_for_Compute_Module_Boards_eMMC_version

imagen firmware
https://www.raspberrypi.com/software/operating-systems/


# CM4 Dual Eth mini Board

<p align="center">
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/CM4-DUAL-ETH-MINI-details-intro.jpg" height="300" alt="www.instintodigital.net">
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/CM4-DUAL-ETH-MINI-details-intro2.png" height="300" alt="www.instintodigital.net">
    <img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/CM4-DUAL-ETH-MINI-details-size.jpg" height="270" alt="www.instintodigital.net">
</p>

wiki
https://www.waveshare.com/wiki/CM4-DUAL-ETH-MINI

<br>

# Desactivar Screen Saver Raspbian
```
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
```
Alli, debemos comentar la linea:
```
#@xscreensaver -no-splash
```

y agregamos:
```
@xset dpms 0 0 0          #Standby: 0   Suspend:0    Off:0
@xset s off -dpms		  #Desabilita el DPMS
```

con esos comandos deshabilitamos las características DPMS (Energy Star) y evitamos el salvapantalla. Evita 
evita el apagado automatico de la pantalla.

para verificar la configuracion DPMS:
```
xset q 
```
Otros commandos desde la consola:
```
xset s off
xset -dpms
xset s noblank
```

# Abrir el browser al iniciar raspberry
Edit this file
```
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
```
And add this:
```
@xset s off
@xset -dpms
@xset s noblank
@chromium-browser --kiosk http://google.com/
```

> :bulb: **Tip:** You can also add this line if you want the mouse to disappear:
```
@unclutter -idle 0.1 -root
```
requires ```sudo apt-get install unclutter```

revisar también la forma en que abre el navegador:
```
chromium-browser --start-fullscreen
on chromium you can use --start-fullscreen (like F11)
```
# Start chromium browser from the terminal
start a webpage, fullscreen (in Kiosk mode) it work when you specify the desktop variable 
```
DISPLAY=:0 chromium-browser --kiosk --app=localhost:8080

DISPLAY=:0 chromium-browser --app=https://your.website —kiosk &

DISPLAY=:0 chromium-browser -kiosk
```
inicia una versión de pantalla completa de Chrome sin mostrar ninguna de las opciones o barras de marcadores. La única forma de salir de la ventana es ```Alt+Tab``` out o ```Alt+F4```para cerrar la ventana por completo.

```
DISPLAY=:0 chromium-browser -start-maximized
```
```
start chrome %192.168.100.19:8080%
chromium-browser %192.168.100.19:8080%
```
<br>

# Scan Serial Port
```
 dmesg | grep tty
```
```
ls /dev/tty*
```

# Scan port USB
```
ls /dev/*USB*
```

# Error puerto
https://devicetests.com/fix-permission-denied-error-xubuntu-serial-port <br>
https://serialport.io/docs/api-serialport

<br>

---
Copyright &copy; 2022 [carjavi](https://github.com/carjavi). <br>
```www.instintodigital.net``` <br>
carjavi@hotmail.com <br>
<p align="center">
    <a href="https://instintodigital.net/" target="_blank"><img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/developer.png" height="100" alt="www.instintodigital.net"></a>
</p>
