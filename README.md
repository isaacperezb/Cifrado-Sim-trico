# Cifrado Simétrico
El cifrado simétrico es una de las técnicas de criptofrafía más antiguas y que aún ofrece un alto nivel de seguridad frente diferentes situaciones de uso.
Utilizamos una misma clave para cifrar y descifrar la información que vamos a mandar por la red para que solo nosotros y la persona correspondiente pueda leer y/o ver el contenido del mensaje enviado y viceversa, dicha clave de ser lo más difícil de adivinar. Para ello deberemos utilizar carácteres especiales, numéricos, alfabeticos...

Es como si queremos llevarle un papel muy importante de nuestra empresa a un abogado y lo llevamos en una carpeta, a simple vista no podrán ver el contenido del papel, pero sigué siendo susceptible de que puedan quitarnos la carpeta y ver el contenido con total claridad.

En esta práctica nos centraremos en el cifrado simétrico tanto con GPG como con OpenSSL.

## GPG
El cifrado simétrico en comparación con el asimétrico es más rápido pero también más inseguro ya que la compartición de la clave secreta se puede ver comprometida por un tercero.

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

## OpenSSL
