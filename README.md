# Cifrado Simétrico
El cifrado simétrico es una de las técnicas que tenemos en seguridad informática para pasar información  con otra persona a través de la red. pero  sin que sea legible a simple vista.
Es como si queremos llevarle un papel muy importante de nuestra empresa a un abogado y lo llevamos en una carpeta, a simple vista no podrán ver el resultado, pero sigué siendo susceptible de que puedan quitarnos la carpeta y ver el contenido con total claridad.
El cifrado simétrico es más rápido y sencillo que el cifrado asimétrico pero también más inseguro. En esta práctica nos centraremos en el cifrado simétrico tanto con GPG como con OpenSSL.

## GPG
El cifrado simétrico en GPG es muy simple ya no que no tenemos que descargarnos el par de claves como en el simétrico. Solo necesitamos una contraseña la cual conocamos nosotros y la persona con la que queremos compartir el archivo.

En el siguiente ejemplo vamos a cifrar un mensaje y por FTP lo vamos a pasar a otra máquina para descifrarlo (Estamos trabajando con dos máquinas virtuales).



El resto de opciones con GPG ya nos pediría el par de claves con las que conseguimos el cifrado asimétrico.
