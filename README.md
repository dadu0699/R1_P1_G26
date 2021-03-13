# **Manual de Construcción y Configuración**

## **Contenido**   
- [Tablas de configuraciones](#idTBConf)
- [Topología 1](#idTopo1)
- [Topología 2](#idTopo2)
- [Configuración VPN ](#idVPN)

## **Tabla de configuraciones**<a name="idTBConf"></a>
| VIRTUAL 	|         HOST        	| CONECTADO A 	|   DIRECCION IP  	| VLAN 	|
|:-------:	|:-------------------:	|:-----------:	|:---------------:	|:----:	|
|    Si   	| Informática 1       	|     SW1     	|  192.168.126.15 	|  36  	|
|    No   	| Informática 2       	|     SW3     	|  192.168.126.30 	|  36  	|
|    Si   	| Server Informática  	|     SW6     	| 192.168.126.150 	|  36  	|
|    Si   	| Ventas 1            	|     SW3     	|  192.168.226.15 	|  46  	|
|    No   	| Ventas 2            	|     SW4     	|  192.168.226.30 	|  46  	|
|    Si   	| Server Ventas       	|     SW7     	| 192.168.226.150 	|  46  	|
|    No   	| Contabilidad 1      	|     SW1     	|   192.168.26.15 	|  56  	|
|    Si   	| Contabilidad 2      	|     SW4     	|   192.168.26.30 	|  56  	|
|    Si   	| Server Contabilidad 	|     SW6     	|  192.168.26.150 	|  56  	|

## **Tabla de configuraciones de la nube**<a name="idTBConf"></a>

| TOPOLOGIA |     LOCAL PORT     	|  REMOTE HOST	|   REMOTE PORT  	|
|:-------:	|:-------------------:	|:-----------:	|:---------------:	|
|    1   	|         3223      	|    10.8.0.2  	|       5671     	|
|    2   	|         5671      	|    10.8.0.3   |       3223    	| 



## **Topología 1**<a name="idTopo1"></a>
Esta topología está compuesta por:
- 3 VPCS
- 3 computadoras virtualizadas en VMware
- 4 Switch
- 1 Cloud

### **Configuración de Switchs**
Para realizar la configuración necesaria de las vlans y los enlaces troncales en los switch, se debe dar doble clic encima del switch a configurar. En el área de puertos dar doble clic para seleccionar el que se desea configurar este aparecerá en el área de *settings*. Si se requiere configurar la vlan solo se debe cambiar el campo VLAN con el número de la vlan correspondiente. Si solo se requiere configurar como modo troncal se debe cambiar el campo type a modo *dot1q*. 

<div align="center">
    <img src="./assets/images/Topo1/1.png" width="400">
    <p align="center">Configuración SW1</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/2.png" width="400">
    <p align="center">Configuración SW2</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/3.png" width="400">
    <p align="center">Configuración SW3</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/4.png" width="400">
    <p align="center">Configuración SW4</p>
</div>

### **Configuración de VPCS**
Para realizar la configuración de las VPCS solo es necesario asignarles la dirección IP, máscara de subred y gateway correspondiente con el siguiente comando.

```bash
ip <IP Address> <Subnet Mask> <Default Gateway>
```

<div align="center">
    <img src="./assets/images/Topo1/5.png" width="400">
    <p align="center">Configuración VPCS Contabilidad</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/6.png" width="400">
    <p align="center">Configuración VPCS Ventas</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/7.png" width="400">
    <p align="center">Configuración VPCS Informática</p>
</div>

### **Computadoras virtualizadas**
#### GNS3
Para la utilización de las máquinas virtualizadas en VMware es necesario habilitar las interfaces de red necesarias.

- Para esto ingresamos al menú *edit* y luego en la opción *preferences*.

<div align="center">
    <img src="./assets/images/Topo1/9.png" width="400">
    <p align="center">Opción preferences</p>
</div>

- En la ventana desplegada buscamos el submenu *VMware* y luego en la pestaña *Advance local settings*, cambiamos la cantidad de interfaces a generar y le damos *Configure*.

<div align="center">
    <img src="./assets/images/Topo1/10.png" width="400">
    <p align="center">Opción preferences</p>
</div>

Luego de haber habilitado las interfaces, es necesario revisar que se hayan creado correctamente.

* Abrimos el programa *ejecutar* y escribimos el siguiente comando para abrir las conexiones de red.

```bash
ncpa.cpl
```

<div align="center">
    <img src="./assets/images/Topo1/27.png" width="400">
    <p align="center">Ventana ejecutar</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/28.png" width="400">
    <p align="center">Conexiones de red</p>
</div>

Se deben importar las máquinas virtuales para ser utilizadas.

* Debemos ingresar al menú *VMware VMs* y en luego en *New*.

<div align="center">
    <img src="./assets/images/Topo1/11.png" width="400">
    <p align="center">Máquinas virtuales</p>
</div>

#### VMware
Es necesario configurar a cada virtual su correspondiente dirección ip, máscara de red y gateway.

<div align="center">
    <img src="./assets/images/Topo1/15.png" width="400">
    <p align="center">Paso 1 configuración IP manual Linux Zorin</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/16.png" width="400">
    <p align="center">Paso 2 configuración IP manual Linux Zorin</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo1/17.png" width="400">
    <p align="center">Paso 3 configuración IP manual Linux Zorin</p>
</div>
<br/>

Luego de haber configurado las ip es necesario cambiar la configuración de las tarjetas de red en cada máquina virtual, por las generadas en GNS3.

<div align="center">
    <img src="./assets/images/Topo1/18.png" width="400">
    <p align="center">Configuración tarjeta de red</p>
</div>
<br/>


### **Consulta de Servidores Web**

* Departamento de Informática

<div align="center">
    <img src="./assets/images/Topo1/14.png" width="400">
    <p align="center">Sitio: 192.168.126.150/informatica/</p>
</div>
<br/>

* Departamento de Ventas

<div align="center">
    <img src="./assets/images/Topo1/13.png" width="400">
    <p align="center">Sitio: 192.168.226.150/ventas/</p>
</div>
<br/>

* Departamento de Contabilidad

<div align="center">
    <img src="./assets/images/Topo1/12.png" width="400">
    <p align="center">Sitio: 192.168.26.150/contabilidad/</p>
</div>
<br/>



## **Topología 2**<a name="idTopo2"></a>
Esta topología está compuesta por:
- 3 computadoras virtualizadas en VMware
- 3 Switch
- 1 Cloud

### **Configuración de Switchs**
Como en la [Topología 1](#idTopo1) es necesario configurar cada uno de los switch para generar la comunicación.  

<div align="center">
    <img src="./assets/images/Topo2/1.png" width="400">
    <p align="center">Configuración SW5</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo2/2.png" width="400">
    <p align="center">Configuración SW6</p>
</div>
<br/>

<div align="center">
    <img src="./assets/images/Topo2/3.png" width="400">
    <p align="center">Configuración SW7</p>
</div>

### **Computadoras virtualizadas**
#### GNS3
Es necesario realizar los pasos de la [Topología 1](#idTopo1) para configurar cada equipo y adicionalmente se debe configurar un servidor apache para desplegar paginas web. Para esto debemos seguir los siguientes pasos

* Debemos descargar los archivos que contienen la pagina web.
<div align="center">
    <img src="./assets/images/Topo2/11.png" width="400">
    <p align="center">Archivos pagina web informática</p>
</div>

* En una terminal se deben ejecutar los siguientes comandos, para instalar el servidor apache.

```bash
sudo apt-get update
sudo apt-get install apache2
```

* Cada uno de los siguientes comandos son para crear, copiar y desplegar la página web en el servidor.

```bash
sudo mkdir -p /var/www/html/<carpeta>
sudo chown -R $USER:$USER /var/www/html/<carpeta>
sudo chmod -R 755 /var/www/html/<carpeta>
sudo cp -r /home/user/Descargas/<carpeta>/* /var/www/html/<carpeta>/
sudo chown -R $USER:$USER /var/www/html/<carpeta>/assets
sudo chmod -R 755 /var/www/html/<carpeta>/assets
```

## **Configuración VPN**<a name="idVPN"></a>

### Google Cloud Platform 

Para la creacion de nuestro servidor VPN se utilizo una máquina virtual en Google Cloud. 

* Creamos un regla de Firewall para nuestro proyecto. 

<div align="center">
    <img src="./assets/images/VPN/1.png" width="400">
    <p align="center">Nueva regla de Firewall para el puerto 1194</p>
</div>

* Creamos una instancia de Máquina Virtual. 

<div align="center">
    <img src="./assets/images/VPN/2.png" width="400">
    <p align="center">Nombre de Máquina Virtual</p>
</div>

<div align="center">
    <img src="./assets/images/VPN/3.png" width="400">
    <p align="center">Sistema Operativo Ubuntu </p>
</div>

<div align="center">
    <img src="./assets/images/VPN/4.png" width="400">
    <p align="center">Configuración de etiqueta de red</p>
</div>
    

* Ejecutar los siguientes comandos en la Máquina Virtual. 

```bash
sudo apt-get update 
sudo apt-get upgrade
```

* Instalar OpenVPN. 

```bash
sudo wget https://skiddow.github.io/OpenVPN/openvpn-install.sh
sudo bash openvpn-install.sh
```

*  Ingresar la Dirección Privada. 

<div align="center">
    <img src="./assets/images/VPN/9.png" width="400">
    <p align="center">Ingresar IP interna asignada por GCP</p>
</div>

* Ingresar la Dirección Pública.

<div align="center">
    <img src="./assets/images/VPN/10.png" width="400">
    <p align="center">Ingresar IP externa asignada por GCP</p>
</div>

* Elegir el protocolo a utilizar.

<div align="center">
    <img src="./assets/images/VPN/11.png" width="400">
    <p align="center">Protocolo UDP</p>
</div>

*  Elegir el puerto que utilizara OpenVPN. 

<div align="center">
    <img src="./assets/images/VPN/12.png" width="400">
    <p align="center">Puerto 1194 configurado en la regla de Firewall</p>
</div>

* Elegir DNS a utilizar.

<div align="center">
    <img src="./assets/images/VPN/13.png" width="400">
    <p align="center">Se utiliza Google</p>
</div>

*  Nombre del cliente que se va a conectar. 

<div align="center">
    <img src="./assets/images/VPN/14.png" width="400">
    <p align="center">client1</p>
</div>


* Una vez finalizado el proceso de creación del cliente se descarga el archivo generado.  

<div align="center">
    <img src="./assets/images/VPN/16.png" width="400">
    <p align="center">Descargar archivo de client1</p>
</div>

*  Creamos otro cliente.

<div align="center">
    <img src="./assets/images/VPN/17.png" width="400">
    <p align="center">Opción 1</p>
</div>

<div align="center">
    <img src="./assets/images/VPN/18.png" width="400">
    <p align="center">client2</p>
</div>

* Una vez finalizado el proceso de creación del cliente se descarga el archivo generado.  

<div align="center">
    <img src="./assets/images/VPN/19.png" width="400">
    <p align="center">Descargar archivo de client2</p>
</div>