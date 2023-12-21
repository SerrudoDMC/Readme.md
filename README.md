# Readme.md
# PROYECTO FINAL GRUPO 8
## INTRODUCCION
###### En el presente documento estaremos viendo como se instala una distribución de Linux  y está la estaremos ejecutando en “Oracle VM VirtualBox.
###### TYPO3 es un sistema de gestión de contenidos gratuito y de código abierto escrito en PHP. Es un CMS de clase empresarial que combina el código abierto con la fiabilidad y la verdadera escalabilidad. Se ejecuta en un servidor web y es compatible con muchos sistemas operativos, como Windows, Linux, macOS, etc. Es un CMS sencillo, con capacidad de respuesta, preparado para dispositivos móviles y seguro, y puede personalizarse y ampliarse fácilmente sin necesidad de escribir ningún código. Es una opción muy popular y estupenda para poner en marcha tu sitio web rápidamente.
###### Acontinuacion, te mostraremos cómo instalar el CMS TYPO3 con el servidor web Apache y Let’s Encrypt SSL en Ubuntu (LINUX MINT)

# DESARROLLO/INSTALACION
#### **Requisitos previos**
- Un servidor con Ubuntu 20.04.
- Un nombre de dominio válido apuntado con la IP de tu servidor.
- Un contraseña de root configurada el servidor.

## ¿Como Empezar?

### PASO 1
En primer lugar, se recomienda actualizar los paquetes de tu sistema con la última versión. Puedes actualizar todos los paquetes ejecutando el siguiente comando, para ello tienes que ingresar como super usuario(root):
  
	sudo su
	apt-get update -y
