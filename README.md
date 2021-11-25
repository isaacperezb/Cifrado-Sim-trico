# Cifrado Simétrico
El cifrado simétrico es una de las técnicas de criptofrafía más antiguas y que aún ofrece un alto nivel de seguridad frente a diferentes situaciones de uso.
Utilizamos una misma clave para cifrar y descifrar los datos que vamos a mandar por la red para que solo nosotros y la persona correspondiente pueda leer y/o ver el contenido del mensaje enviado y viceversa, dicha clave de ser lo más difícil de adivinar. Para ello deberemos utilizar carácteres especiales, numéricos, alfabeticos...

Es como si queremos llevarle un papel muy importante de nuestra empresa a un abogado y lo llevamos en una carpeta, a simple vista no podrán ver el contenido del papel, pero sigué siendo susceptible de que puedan quitarnos la carpeta y ver el contenido con total claridad.

En esta práctica nos centraremos en el cifrado simétrico tanto con GPG como con OpenSSL.

## GPG
El cifrado simétrico en comparación con el asimétrico es más rápido pero también más inseguro ya que la compartición de la clave secreta se puede ver comprometida por un tercero. En cambio en el cifrado asimétrico publicamos nuestra clave publica y cuando nos envíen datos, se encriptarán con dicha clave pública siendo nosotros los únicos que poseemos la clave privada solo nosotros podremos ver el contenido.

En el siguiente ejemplo vamos a cifrar un mensaje y por FTP lo vamos a pasar a otra máquina para descifrarlo (Estamos trabajando con dos máquinas virtuales).

Por defecto gpg cifra con el algoritmo AES256 pero este lo podemos cambiar eligiendolo en el comando. Para ello deberemos elegir entre los algoritmos de cifrado simétrico que dispone GPG.

![Algoritmos](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/11.JPG)

El primer fichero cerrado lo haremos con el comando por defecto.

Para ello primero crearemos el fichero a cifrar y escribimos el comando para cifrarlo.

![fichero a cifrar](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/1.JPG)

Al dar enter nos pedirá que pongamos la clave de cifrado y nos pedirá confirmarla

![contraseña cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/2.JPG)

Una vez creado haciendo un ls veremos el fichero cifrado

![fichero cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/4.JPG)

Ahora pasaremos el fichero por FTP hacia la otra máquina virtual para descifrarlo.

![FTP](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/6.JPG)

En la otra máquina haciendo ls veremos que tenemos descargado el fichero encriptado.

![ficharo en la otra máquina](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/7.JPG)

Y una vea tengamos el fichero lo desencriptaremos con el comando correspondiente y nos pedirá la clave que pusimos antes.

![Descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/8.JPG)
![contraseña descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/9.JPG)

Ahora vamos a crear nuevos ficheros y encruiptarlos con otros algoritmos, siguiendo los mismos pasos que antes: comando de encriptado, contraseña, pasarlo por FTP y desencriptarlo en la otra máquina.

### BLOWFISH
![BLOWFISH](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/12.JPG) 
![descifrado blowfish](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/14.JPG)

### 3DES

![3DES](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/15.JPG)
![3DES desenciptado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/17.JPG)

Podemso encriptar con todos los algoritmos que tiene GPG siguiendo el comando que hemos estado utilizando para encriptar con BLOWFISH y 3DES (gpg --symmetric --cipher-algo NOMBRE_ALGORITMO NOMBRE_FICHERO) y para desencriptar siempre usaremos el mismo comando (gpg -d NOMBRE_FICHERO.gpg)

Para ponerle el nombre que nosotros queramos al archivo encriptado para que por defecto no nos aparezca con el mismo nombre y la extensión gpg debemos poner la opción -o 
![crear_fichero](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/18.JPG)
![nombre_que_queramos](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/19.JPG)
![resultado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/22.JPG)

Para cifrar en formato ASCII debemos poner la opción --armor.

![ASCII](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/20.JPG)

Para descifrar en formato de ASCII usaremos la opción -o para indicarle el nombre del fichero que queremos para identificarlo de forma fácil y la opción por defecto para desencriptar -d.

![descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/GPG/21.JPG)

## OpenSSL

Vamos a realizar varias pruebas de cifrado simétrico con OpenSSL utilizando diferentes algoritmos.
Para ello voy a crear el ficher open.txt y lo ire cifrado con los algoritmos, usando el siguiente comando:
**openssl aes-128-cbc -in open.txt -out cifrado.enc**
Los parametros del comando son los siguientes:
- aes-128-cbc --> es el algoritmo que vamos a utilizar para encriptar el fichero.
- in --> en el fichero a encriptar, en este caso open.txt
- out --> fichero encriptado con el nombre que hayamos decidido, en mi caso le he puesto cifrado.enc

Una vez aceptemos nos pedirá que escribamos la contraseña con la que queremos cifrar y que la confirmemos.

![cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/1.JPG)

Para descifrar utilizaríamos el siguiente comando:
**openssl aes-128-cbc -d -in cifrado.enc -out descifrado**
Las opciones serían iguales que con el comando de cifrado pero añadiriamos -d para indicar que vamos a descifrar y en -in pondríamos el fichero cifrado y en -out el fichero descifrado con el nombre que hayamos querido ponerle.
Al aceptar nos pedirá la contraseña puesta al cifrarlo y lo tendríamos descifrado.

![descifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/2.JPG)

Vamos a realizar una serie de cifrados del mismo fichero pero con diferentes algoritmos.

**rc4**

![rc4](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/8.JPG)


**chacha20**

![chacha20](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/9.JPG)


**des**

![des](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/10.JPG)

Ahora vamos a hacer la prueba de pasarlo por FTP a otra máquina la cual la controla Pepe y el quiere desencriptar el mensaje.
Lo primero que Pepe debe saber es la clave que le hemos puesto al mensaje o sino no podre ver el contenido.

Primero crearemos el archivo a cifrar y lo ciframos.
![creción pepe.txt](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/11.JPG)
![cifrado](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/12.JPG)

Ahora lo pasamos por FTP a Pepe

![FTP](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/13.JPG)

Y Pepe al saber la clave usada para cifrar podrá descifrarlo.

![descifrado de Pepe](https://github.com/isaacperezb/Cifrado-Sim-trico/blob/main/OpenSSL/14.JPG)

### Bibliografía
- https://tutonics.com/2012/11/gpg-encryption-guide-part-4-symmetric.html
- https://www.openssl.org/docs/manmaster/man1/openssl-enc.html
- https://lamiradadelreplicante.com/2015/12/26/cifrado-de-archivos-con-openssl/
