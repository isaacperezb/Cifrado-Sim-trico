# Cifrado Simétrico
El cifrado simétrico es una de las técnicas de criptografía más antiguas y que aún ofrece un alto nivel de seguridad frente a diferentes situaciones de uso.
Utilizamos una misma clave para cifrar y descifrar los datos que vamos a mandar por la red para que solo nosotros y la persona correspondiente pueda leer y/o ver el contenido del mensaje enviado y viceversa, dicha clave debe ser lo más difícil de adivinar. Para ello deberemos utilizar caracteres especiales, numéricos, alfabéticos...

Un ejemeplo de esto sería si queremos llevarle un papel muy importante de nuestra empresa a un abogado y lo llevamos en una carpeta, a simple vista no podrán ver el contenido del papel, pero sigue siendo susceptible de que puedan quitarnos la carpeta y ver el contenido con total claridad.

En esta práctica nos centraremos en el cifrado simétrico tanto con GPG como con OpenSSL. Para ello ambas máquinas deben verse y una de ella debe actuar como router para poder ver con wireshark los paquetes que se envían.

El cifrado simétrico en comparación con el asimétrico es más rápido, pero también más inseguro ya que la compartición de la clave secreta se puede ver comprometida por un tercero. En cambio, en el cifrado asimétrico publicamos nuestra clave publica y cuando nos envíen datos, se encriptarán con dicha clave pública siendo nosotros los únicos que poseemos la clave privada para poder ver el contenido.

## GPG

En el siguiente ejemplo vamos a cifrar un mensaje y por FTP lo vamos a pasar a otra máquina para descifrarlo (Estamos trabajando con dos máquinas virtuales).

Por defecto GPG cifra con el algoritmo AES256, pero este lo podemos cambiar eligiéndolo en el comando. Para ello deberemos elegir entre los algoritmos de cifrado simétrico que dispone GPG.

![Algoritmos](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/11.JPG)

El primer fichero lo haremos con el comando por defecto.

Para ello primero crearemos el fichero a cifrar y escribimos el comando para cifrarlo.
La opción *-c* es para indicar que vamos a cifrarlo.

![fichero a cifrar](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/1.JPG)

Al dar enter nos pedirá que pongamos la clave de cifrado y nos pedirá confirmarla

![contraseña cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/2.JPG)

Una vez creado haciendo un *ls* veremos el fichero cifrado

![fichero cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/4.JPG)

Ahora pasaremos el fichero por FTP hacia la otra máquina virtual para descifrarlo.

![FTP](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/6.JPG)

En la otra máquina haciendo *ls* veremos que tenemos descargado el fichero encriptado.

![fichero en la otra máquina](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/7.JPG)
	
Y una vea tengamos el fichero lo desencriptaremos con el comando correspondiente y nos pedirá la clave que pusimos antes.

![Descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/8.JPG)

La opción *-d* es para indicar que vamos a desencriptarlo.

![contraseña descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/9.JPG)

Ahora vamos a crear nuevos ficheros y encriptarlos con otros algoritmos, siguiendo los mismos pasos que antes: comando de encriptado, contraseña, pasarlo por FTP y desencriptarlo en la otra máquina.

### BLOWFISH
![BLOWFISH](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/12.JPG) 

Las opciopnes son:
- **--symmetric**: para cifrar de forma simétrica
- **--cipher-algo NOMBRE_ALGORITMO**: para indicar con que algoritmo de GPG queremos cifrar el archivo

![descifrado blowfish](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/14.JPG)

### 3DES

![3DES](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/15.JPG)
![3DES desenciptado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/17.JPG)

Podemos encriptar con todos los algoritmos que tiene GPG siguiendo el comando que hemos estado utilizando para encriptar con BLOWFISH y 3DES: 
(**gpg --symmetric --cipher-algo NOMBRE_ALGORITMO NOMBRE_FICHERO**)
Para desencriptar siempre usaremos el mismo comando:
(**gpg -d NOMBRE_FICHERO.gpg**)

Para ponerle el nombre que nosotros queramos al archivo encriptado para que por defecto no nos aparezca con el mismo nombre y la extensión gpg debemos poner la opción *-o* 
![crear_fichero](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/18.JPG)
![nombre_que_queramos](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/19.JPG)
![resultado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/22.JPG)

Para cifrar en formato ASCII debemos poner la opción --armor.

![ASCII](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/20.JPG)

Para descifrar en formato de ASCII usaremos la opción -o para indicarle el nombre del fichero que queremos para identificarlo de forma fácil y la opción por defecto para desencriptar -d.

![descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/21.JPG)

## OpenSSL

Vamos a realizar varias pruebas de cifrado simétrico con OpenSSL utilizando diferentes algoritmos.
Para ello voy a crear el fichero open.txt y lo iré cifrado con los algoritmos, usando el siguiente comando:
**openssl aes-128-cbc -in open.txt -out cifrado.enc**
Los parámetros del comando son los siguientes:
- **aes-128-cbc**: es el algoritmo que vamos a utilizar para encriptar el fichero.
- **-in**: en el fichero a encriptar, en este caso open.txt
- **-out**: fichero encriptado con el nombre que hayamos decidido, en mi caso le he puesto *cifrado.enc*

Una vez aceptemos nos pedirá que escribamos la contraseña con la que queremos cifrar y que la confirmemos.

![cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/1.JPG)

Para descifrar utilizaríamos el siguiente comando:
**openssl aes-128-cbc -d -in cifrado.enc -out descifrado**
Las opciones serían iguales que con el comando de cifrado, pero añadiríamos -d para indicar que vamos a descifrar y en *-in* pondríamos el fichero cifrado y en *-out* el fichero descifrado con el nombre que hayamos querido ponerle.
Al aceptar nos pedirá la contraseña puesta al cifrarlo y lo tendríamos descifrado.

![descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/2.JPG)

Vamos a realizar una serie de cifrados del mismo fichero, pero con diferentes algoritmos.

**rc4**

![rc4](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/8.JPG)


**chacha20**

![chacha20](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/9.JPG)


**des**

![des](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/10.JPG)

Ahora vamos a hacer la prueba de pasarlo por FTP a otra máquina la cual la controla Pepe y él quiere desencriptar el mensaje.
Lo primero que Pepe debe saber es la clave que le hemos puesto al mensaje o sino no podrá ver el contenido.

Primero crearemos el archivo a cifrar y lo ciframos.

![creación pepe.txt](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/11.JPG)
![cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/12.JPG)

Ahora lo pasamos por FTP a Pepe

![FTP](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/13.JPG)

Y Pepe al saber la clave usada para cifrar podrá descifrarlo.

![descifrado de Pepe](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/14.JPG)

## Enlace al video

[Criptografía Simétrica](https://www.youtube.com/watch?v=qN5fwEqG8Yk)

### Bibliografía
- https://tutonics.com/2012/11/gpg-encryption-guide-part-4-symmetric.html
- https://www.openssl.org/docs/manmaster/man1/openssl-enc.html
- https://lamiradadelreplicante.com/2015/12/26/cifrado-de-archivos-con-openssl/
