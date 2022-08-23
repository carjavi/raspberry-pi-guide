<p align="center"><img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/raspberry_logo.png" height="220" alt=" " /></p>
<br>
<h1 align="center">Raspberry Pi Guide</h1> 
<h4 align="right">Aug 22</h4>

<img src="https://img.shields.io/badge/OS%20-Raspbian%20GNU%2FLinux%2011%20(bulleye)-yellowgreen">
<img src="https://img.shields.io/badge/Hardware-Raspberry%20ver%203 & 4-red">

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

# Enabling SSH

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

# SSH Shell desde Linux, Mac o Windows OS
```
ssh pi@<IP>
ssh <USER>@<IP-ADDRESS> 
e.g. pi@192.168.1.10
e.g. eben@192.168.1.5
```
Next you will be prompted for the password for the pi login: the default password on Raspberry Pi OS is raspberry.

# Copying Files to your Raspberry Pi
```
scp myfile.txt pi@192.168.1.3:
```
Copy the file to the /home/pi/project/ directory on your Raspberry Pi (the project folder must already exist):
```
scp myfile.txt pi@192.168.1.3:project/
```
# Copying Files from your Raspberry Pi
Copy the file myfile.txt from your Raspberry Pi to the current directory on your other computer:
```
scp pi@192.168.1.3:myfile.txt .
```
# Copying Multiple Files
```
scp myfile.txt myfile2.txt pi@192.168.1.3:
scp *.txt pi@192.168.1.3:
scp m* pi@192.168.1.3:
scp m*.txt pi@192.168.1.3:
```

# Copying a Whole Directory
Copy the directory project/ from your computer to the pi user’s home folder of your Raspberry Pi at the IP address 192.168.1.3
```
scp -r project/ pi@192.168.1.3:
```

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

# Daemon Service (SYSTEMD)

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

# Systemd Commands Summary
```
sudo systemctl daemon-reload
sudo systemctl enable systemd-networkd
sudo systemctl disable clock.service
sudo systemctl status clock.service
sudo systemctl stop clock.service
sudo systemctl start clock.service

```
<br>

# DHCP Server
```
$ sudo apt-get install isc-dhcp-server
```
Modify the configuration in /etc/default/isc-dhcp-server
```
DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf
INTERFACESv6="eth0"
```

In /etc/dhcp/dhcpd6.conf you need to specify the TFTP server address and setup a subnet. Here the DHCP server is configured to supply some made up unique local addresses (ULA). The host test-rpi4 line tells DHCP to give a test device a fixed address.
```
not authoritative;

# Check if the client looks like a Raspberry Pi
if option dhcp6.client-arch-type = 00:29 {
        option dhcp6.bootfile-url "tftp://[fd49:869:6f93::1]/";
}

subnet6 fd49:869:6f93::/64 {
        host test-rpi4 {
                host-identifier option dhcp6.client-id 00:03:00:01:e4:5f:01:20:24:0b;
                fixed-address6 fd49:869:6f93::1000;
        }
}

```
Your server has to be assigned the IPv6 address in /etc/dhcpcd.conf

```
interface eth0
static ip6_address=fd49:869:6f93::1/64
```

Now start the DHCP server.
```
$ sudo systemctl restart isc-dhcp-server.service
```
 revisar: https://www.raspberrypi.com/documentation/computers/remote-access.html#introduction-to-remote-access







---
Copyright &copy; 2022 [carjavi](https://github.com/carjavi). <br>
```www.instintodigital.net``` <br>
carjavi@hotmail.com <br>
<p align="center">
    <a href="https://instintodigital.net/" target="_blank"><img src="https://raw.githubusercontent.com/carjavi/raspberry-pi-guide/master/img/developer.png" height="100" alt="www.instintodigital.net"></a>
</p>
