# PRACTICA 6  : Buses de comunicación II (SPI)

## A:  LECTURA/ESCRITURA DE MEMORIA SD

### Código

```cpp
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>

File myFile;

void setup(){

Serial.begin(9600);
Serial.print("Iniciando SD ...");

SPI.begin(18,19,23,4);

if(! SD.begin(4)){
  Serial.println("No se pudo inicializar");
  return;
}
  
Serial.println("inicializacion exitosa");

// Escribimos en el fichero
myFile = SD.open("/archivo.txt",FILE_WRITE); 
myFile.println("Escritura en SD correcta.");
myFile.close();

myFile=SD.open("/archivo.txt"); //Abrimos, mostramos y leemos
  if (myFile) {
    Serial.println("archivo.txt:");
    while (myFile.available()) {
      Serial.write(myFile.read());
    }
    myFile.close(); 
  }
  
  else {
    Serial.println("Error al abrir el archivo");
  }
}

void loop(){}
```

### Funcionamiento del programa

En primer lugar, haremos uso de tres librerias en las que destacamos la librería SPI y SD. También tendremos que declarar una variable de tipo File a la que llamaremos "myFile".

```cpp
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>

File myFile;
```

A continuación definimos nuestra función Setup, en primer lugar iniciaremos los pines de entrada, a continuación comprobaremos que la tarjeta microSD esta conectada de forma correcta. Si es así, se procedera con la escritura. En caso de que no se haya conectado de forma correcta nos avisará mostrandonos un mensaje.

Si la conexión se ha realizado de manera correcta, procederemos a la escritura. Para ello el programa va a abrir el fichero llamado "archivo.txt" y en caso de que no exista la sentencia "FILE_WRITE" creará el fichero y procederá a abrirlo. Entonces escribiremos en el fichero y posteriormente si todo ha salido correctamente el contenido del fichero se imprimirá por el puerto série. 

```cpp
void setup(){

Serial.begin(9600);
Serial.print("Iniciando SD ...");

SPI.begin(18,19,23,4);

if(! SD.begin(4)){
  Serial.println("No se pudo inicializar");
  return;
}
  
Serial.println("inicializacion exitosa");

// Escribimos en el fichero
myFile = SD.open("/archivo.txt",FILE_WRITE); 
myFile.println("Escritura en SD correcta.");
myFile.close();

myFile=SD.open("/archivo.txt"); //Abrimos, mostramos y leemos
  if (myFile) {
    Serial.println("archivo.txt:");
    while (myFile.available()) {
      Serial.write(myFile.read());
    }
    myFile.close(); 
  }
  
  else {
    Serial.println("Error al abrir el archivo");
  }
}
```

### Salida por Terminal 

```cpp
Iniciando SD ...sd init ok
inicializacion exitosa
Escritura en SD correcta.
```
