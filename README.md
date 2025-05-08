# Notas de Clase **Sistemas Operativos** -- 2025
Profesor: Roger Asis  

TID material de estudio: [13.pdf](https://materiales.ies21.edu.ar/13.pdf)

## Clase 7 de Abril
Nos conectamos a un servidor hecho por el profe, iniciamos una terminal cmd o powershell y ponemos el comando:  

ssh -p 8632 usuario@190.210.55.43  

El usuario es la primera letra nombre, sumado al apellido, por ejemplo smarkoja.
La contraseña es el dni.  

Comandos que usamos:
pwd = muestra la ubicación actual
ls = listar archivos existentes o carpetas/directorios.
ls -R = para listar carpetas y ver los archivos que contienen. La R es de "recursivo".  

Vimos "direcciones absolutas" (completas que trazan todo el hilo de carpetas desde la unidad principal hasta el directorio o archivo que se busca), y "relativas" (que son más cortas, y dependen de la ubicación actual en la que se encuentra el usuario)
Ejemplo de dirección absoluta: D:\Home\Seba\Estudios\IES\semestre3\sistemas\clases\clase.txt
Ejemplo de dirección relativa: ..\sistemas\clases\clase.txt (estando ubicado inicialmente en una carpeta dentro de \semestre3 que no era \sistemas. Los dos puntos del inicio ".." significan que vuelve un nivel anterior en el esquema de carpetas.)  

la virguilla: ~ = equivale a el directorio principal del equipo, por ejemplo "/home/usuario". Se puede hacer con F8 dentro de la terminal, o con alt+126.  

cd = Es para moverse entre directorios. Significa Change Directory. Ejemplo: cd \seba. (se mueve a la carpeta seba con dirección relativa)  

man = Da info de cualquier comando, se pone al inicio y luego el comando a buscar. Ej: man mkdir
history = Muestra todos los comandos hechos.  

Apretando dos veces Tab se ven los archivos existentes cuando uno está escribiendo una dirección (abs o relativa) y no recuerda que carpetas hay.  

Al final de la sesion se recomienda salir con "exit", "logout" o ctrl+d. Es una "Graceful exit".  

## Clase 10 de Abril
Al poner el comando: ls -l  nos muestra todos los archivos del directorio e información adicional, la cual se puede leer de esta manera:

Total 20 => significa que el espacio utilizado alcanza los 20 bloques.

drwxrwxr-x 2 nuevo2 nuevo2 4096 abr  7 15:34 Actual => información del archivo
U G O
 primera d es el tipo de archivo. d = directorio,
 permisos del owner ejemplo: rwx read write execute.
 r-x = O. 
 2 = Enlaces 
 Propietario = nuevo2 
 Grupo nuevo2
 t.b 4096
 fecha abr 7 15:34 
 Actual es el archivo creado.


El - al inicio es un tipo de archivo regular, como fichero de texto. Los demás - guiones significan que no tiene ese permiso.

Si se usa touch para crear un archivo regular que ya existe, solo le modifica la fecha.

nano con el mismo archivo, entra al ya creado y permite editarlo.

less archivo1.txt nos permite visualizar el archivo pero no escribirlo.

... estos comandos llaman a aplicativos, o aplicaciones que nos dan estas funcionalidades.

El comando cat es otro aplicativo que permite incluso ver dos archivos a la vez:
Sintaxis básica:
	cat [opciones] [archivo(s)]. 
Ejemplos:
	cat archivo.txt: Muestra el contenido del archivo archivo.txt. 
	cat archivo1.txt archivo2.txt: Muestra el contenido de ambos archivos, uno después del otro. 
	cat > nuevo_archivo.txt: Permite crear un archivo y escribir contenido en él desde la terminal. 
	cat archivo.txt > nuevo_archivo.txt: Copia el contenido de archivo.txt a nuevo_archivo.txt. 
	cat archivo.txt | more: Muestra el contenido de archivo.txt paginado (útil para archivos grandes). 


cp archivo.txt archivo.txt-BKP => es para hacer backup. Esto va a copiar el mismo archivo en el directorio con la extension .txt-BKP

file => acompañado del nombre del archivo sirve para ver el tipo de archivo que es.
echo => para mostrar cosas en pantalla. echo $0 =>nos dice que interprete estamos utilizando.
 
Conceptos en Sistemas operativos
Cuando inicia el sistema operativo, se inica el SUPERVISOR.
Administradores.

System Calls - Interrupciones de sistema. Son de las interrupciones más importantes, que sirven en caso de falla.
Un intérprete transforma un código en objeto para luego poder ejecutarse.
Programa objeto.
Ensamblador o Asembler. Toma un objeto que ya ha sido compilado o programa objeto, y lo deja listo para ser ejecutable.
Cargador. Encargado de ejecutar y cargar el programa objeto procesado por el ensamblador para verlo.
A diferencia de un compilador, el intérprete lee línea por línea (sentencias).
Utilitarios:  programas que realizan tareas rutinarias y de propósitos específicos. Tales como el cp, mv, ls, etc. También desfragmentadores de disco, gestor  de cola de archivos, etc.

## Clase 14 de Abril

### Salidas Estandar  
Salida Estándar (stdout) / std out 1  //Es el flujo de salida predeterminado para la información normal y los resultados de un programa. Cuando un programa imprime algo sin especificar un destino, generalmente se dirige a la salida estándar.Por defecto, la salida estándar de un comando se muestra directamente en la ventana de la terminal.  
Entrada Estándar (stdin) / std in 0   // Aunque no es una salida, es fundamental para la interacción con los programas desde la terminal. La entrada estándar es el flujo de datos que un programa recibe. Por defecto, proviene del teclado. Los programas que esperan entrada del usuario la leen desde la entrada estándar.  
Error Estándar (stderr) / std error 2  //Está diseñado para mostrar mensajes de error, diagnósticos y otra información que indica problemas durante la ejecución de un programa. Separar los errores de la salida normal facilita la depuración y el manejo de errores en scripts.Por defecto, el error estándar también se muestra en la ventana de la terminal, mezclado con la salida estándar.  

```
ls -l 1 > fichero1.txt
```  

// el 1 está implácito. NO es necesario utilizarlo.   

Cuando se le vuelve a indicar el mismo se sobreescribe el archivo con los nuevos datos (sobreescribir accidentalmente datos, conocido como "Clobbering").
Append: concatenar cosas. Por ejemplo con:   

```
cat fichero 1
```   
Cuando se creó el archivo pesaba 0bytes, cuando se pone el comando ls -l del inicio, el valor real todavía estaba en el buffer. Luego cuando se invoca por segunda vez el comando ya aparece el dato real, pesando 912 bytes.  
```
ls -l >> redirecinSalidaEstandar.txt  
echo "El contenido del texto ...." >> RedirecionSalidaEstandar.txt  
cat RedirecionSalidaEstandar.txt  
```  
Esto ">>" imposibilita el clobbering, así no se sobreescribe el archivo.  

Se pueden combinar comandos de esta forma:  
```
cat fichero1.txt RedirecionSalidaEstandar.txt NoExiste.txt > salidaError.txt 2>&1
```  
En el contexto de la terminal de Linux (y otros sistemas Unix-like), 2>&1 es una redirección del error estándar (stderr) a la misma ubicación que la salida estándar (stdout). Vamos a desglosarlo:  

>2: Representa el descriptor de archivo asociado con el error estándar (stderr). En los sistemas Unix, a cada flujo de entrada/salida se le asigna un número de descriptor. El 0 es para la entrada estándar (stdin), el 1 para la salida estándar (stdout), y el 2 para el error estándar (stderr).  

>.>: Normalmente, este símbolo se utiliza para redirigir la salida. Cuando se usa solo con un descriptor de archivo (como 2>), redirige ese flujo a un archivo específico.  

>&1: Aquí, el & antes del 1 es importante. Indica que no se está redirigiendo al archivo llamado "1", sino que se está redirigiendo al mismo destino al que apunta el descriptor de archivo número 1 (stdout) en ese momento.  

En resumen, 2>&1 toma todo lo que normalmente se enviaría al error estándar y lo dirige al mismo lugar donde se está enviando la salida estándar.

Usamos "wc -l" como ejercicio de ejemplo de standard in. Este comando cuenta la cantidad de líneas. Como no le ingresamos ningun archivo, le escribimos a mano las frases que queramos.  

## Clase 21 de Abril

Ejercicio práctico. 

Para crear los directorios el profe propuso:
```
mkdir -p Practica/Primero Practica/Segundo
```
Sin el -p no se podría, ya que este indica que se creen los directorios padres.  

A partir del punto 5, creamos un fichero. Se puede crear de dos formas, con touch o nano. Y poner una ruta relativa o absoluta.  

Hacemos dos directorios con un archivo en cada uno. Para el segundo tenemos que mandar la salida estandar de listar. Para ello hicimos:
```
ls > Segundo/SalidaEstandar.txt
```  

Luego para modificar el archivo MiPrimerFichero.txt usamos nano, o como prefirió el profe, echo y una redirección:
```
echo Pedrito tenia un perrito chiquitito 1> MiPrimerFichero.txt
```  
luego con este comando copio el mismo contenido pero evitando el clobering o la sobreescritura (con ">>")...
```
echo Pedrito tenia un perrito chiquitito >> MiPrimerFichero.txt
``` 
## Clase 28 de Abril  
Vimos desde pág. 61. Hay que leer hasta pág 72. 

| Significado     | Letra  |
|-----------------|--------|
| Archivo regular |    -   |
| Directorio      |    d   | 
| Leer            |    r   |
| Escribir        |    w   |
| Ejecutar        |    x   |

Enlaces simbolicos (acceso directo) y enlaces duros.
Le hacemos un softlink a un fichero en nuestra carpeta.
ln -s path nombredelacceso.ln

La ruta que pongamos debe de ser Absoluta. Porque al usar este acceso directo desde otra ubicación no va a funcionar.

Los "modos" en linux son los permisos de un archivo.  

| U  |  G  | O   |
|----|-----|-----|
|rwx | +w+ | rw- |   

(Usuario (User), Grupo (Group) y Otros (Others))

```
chmod g+x Ejecutable.sh //Esto utilizó el profe para darnos permisos de Ejecución sobre el archivo 
chmod g-r Ejecutable.sh //Para SACAR permisos de lectura sobre el archivo   
```  
* Modo caracter  
chmod +  

| Significado     | Letra  |
|-----------------|--------|
| usuario propietario | u   |
| grupo|    g | 
| otros|    o   |
| agil| a   |
| igual a   | =  |
| suma  | + |
| resta | - |

* Modo Octal  

| Significado     | Letra  |
|-----------------|--------|
| Read        | 4  |
| Write       | 2  | 
| Execute     | 1  |
| Sin Permiso | 0  |  

La suma de estos nos da lo siguiente, debemos indicar uno de estos números para cada usuario (UGO):  

* 7 (4 + 2 + 1): read, write, and execute (rwx)
* 6 (4 + 2 + 0): read and write (rw-)
* 5 (4 + 0 + 1): read and execute (r-x)
* 4 (4 + 0 + 0): read only (r--)
* 3 (0 + 2 + 1): write and execute (-wx)
* 2 (0 + 2 + 0): write only (-w-)
* 1 (0 + 0 + 1): execute only (--x)
* 0 (0 + 0 + 0): no permissions (---)

grep => sirve para buscar cadenas de texto dentro de archivos
```  
ls | grep ^P
```  
Acá buscó todos los archivos que comienzan con P mayúscula. Si se cambia por s$ => todos los que terminan en s. Sin simbolos busca todas las coincidencias 'grep so'. Si agrega a todo | wc -l => cuenta la cantidad de coincidencias encontradas.  

La diferencia entre pipe y fifo es que el fifo se almacena y el otro no persiste en los archivos de sistema.

## Clase 5 de Mayo
Hoy vimos mediante el comando 
```
ipconfig /all
```
Donde en el mismo se indica datos de conexión. Muestra nuestra Dirección IPv4, Máscara de Subred (Red a la que pertenece la pc, en nuestro caso todas las del lab tienen la misma), aervidores DNS, y puerta de enlace determinada (puerto ip al que se conecta la pc).  
Luego con el comando  
```
ping 'direccion web de lo que quieras'
```
nos mostrará la latencia que existe frente a ese sitio web, TTL es el tiempo que esa ip se guardará en caché para nuevas consultas a la misma.  
### Imagen en usb para instalación de SO
Para instalar un Sistema operativo como Lubuntu, tenemos que preparar una memoria usb con Rufus, al iniciar ese programa seleccionamos la usb, formato FAT (o FAT32), y seleccionamos la imagen iso correspondiente al nuevo SO.
Vamos a "instalarlo" como sistema operativo live, quiere decir que es un sistema que podemos usar sin borrar nada del pc, y es portable mediante la usb a otros pc.    
IMPORTANTE: debemos conservar los datos de conexión de nuestra pc vistos en el ipconfig. IP, Netmask, Port, 
Luego iniciamos la pc con esta memoria y hay que apretar varias veces f8, se nos abrirá el menu de booteo, o directamente se nos puede iniciar la imagen del usb (como le paso a mariano). Luego seleccionar versión de prueba haciendo click en "try".  
Una vez iniciado el sistema y funcionando correctamente, nos dirijimos abajo a la derecha en la barra, y configuramos la conexión de red del pc, para poder acceder a internet. Agregamos una nueva red con los datos que guardamos aparte anteriormente.
Puede pasar que ya exista un perfil anterior de conexión con otros datos incorrectos, en ese caso una vez creado el nuevo, debemos hacer click izquierdo en el logo de conexiones y seleccionar nuestro nuevo perfil. De esta forma accederemos a internet.

## Clase 8 de Mayo

La diferencia entre un hosting y un servidor, es que en el hosting nos permite menos recursos, pero a un precio más económico que un servidor.
Los ínodos son todos los archivos de sistema que contienen información sobre como son almacenado los datos.

> df -T //esto es parar 
> df -h//human readable
> df -ih//la i de inodo + human readable

Tipos de archivo:
- Sis ADM Archivos:

	* Directorios (d)

	* *Ficheros Regulares/Ordinarios  (-)

	* Link  --> Simbólicos / Duros  (L)

	* Pipes --> | / con Nombre FiFos  (P)

	* Ficheros de bloques  (b)

- Sis ADM Dispositivos:

	* Ficheros especiales de caracteres  (c)


Ubuntu como App dentro de windows, es muy útil.  
```
ls -i => podemos ver el número de inodo de un archivo.
stat => vemos especificaciones del archivo.
```
[Wikipedia sobre Inodos](https://es.wikipedia.org/wiki/Inodo)  

Un link duro no puede tener una dirección de otro sistema de archivos.
´´´
ln targetdirectoquesebusqueEnRutaAbsoluta.
´´´

Un **link duro** es un archivo regular (-), y es el mismo archivo que el orginal, en cambio los **links blandos** aparecen en celeste como los links y son un nuevo archivo.  
Cuando creamos un link duro hacia un fichero por ejemplo, ambos tendrán el mismo número de Inodo.  
Esto se puede ver con 'ls -il'. Entonces, es posible tener muchos nombres de archivos, con el mismo inodo.
Al crear un enlace blando con 'ln -s' no tiene el mismo inodo porque es un archivo nuevo.  
Cuando un archivo es eliminado, su **link duro** contiene aún su información, en cambio en los enlaces blandos no se pueden acceder por que el archivo base ya no existe. Una vez eliminados tanto el archivo como sus enlaces, en ese momento el inodo ya se elimina completamente.