# Practica ESP32 con HC-SR04 Ultrasonic Distance Sensor para saber el nivel de un deposito
Este repositorio muestra como podemos programar una ESP32 con el sensor Ultrasonico de distancia para poder saber el nivel de un deposito de agua, utilizamos leds como indicadores del nivel.

## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```HC-SR04```) Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor HC-SR04 Ultra Distance 
- LEDS como representación de nivel 
- Y muchas ganas de chambear :D


## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:


```
// defines pins numbers
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 23;
const int led2 = 22;
const int led3 = 19;
const int led4 = 18;

// defines variables
long duration;
int distance;
int safetyDistance;


void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance>=2 && safetyDistance<=10)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}
else if(safetyDistance>=10 && safetyDistance<=20) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}
else if(safetyDistance>=20 && safetyDistance<=30) 
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
}
else if(safetyDistance>=30 && safetyDistance<=40) 
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
}
else if (safetyDistance>=40 && safetyDistance<=45) // aqui denotaremos parpadeo en los leds para saber que ya esta lleno el deposito
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  delay(500);
   digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  delay (500);
   digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  delay(500);
   digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  delay (500);
   digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  delay(500);
   digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  delay (500);
   digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  delay(500);
}
else if (safetyDistance > 45 )
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay (1000);
}

```

2. Hacer la conexion de **HC-SR04** con la **ESP32** como se muestra en la siguente imagen.



![](https://github.com/UrielMastache/ESP32-HCSR04/blob/main/Conexion%20sensor.png?raw=true)

3. Hacer la conexion de **LEDS** con la **ESP32** como se muestra en la siguiente imagen.

![](https://github.com/UrielMastache/ESP32-Sensor-Nivel-Con-Leds/blob/main/Conexiones%20leds.png?raw=true)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial y con los leds dinamicos.

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial (parte blanca de abajo, así como también en dependiendo del nivel del sensor prenderan los leds) como se muestra en las siguentes imagenes.

Nivel de 2 a 10 cm
![](https://github.com/UrielMastache/ESP32-Sensor-Nivel-Con-Leds/blob/main/un%20led%20prendido.png?raw=true)

Nivel de 10 a 20 cm

![](https://github.com/UrielMastache/ESP32-Sensor-Nivel-Con-Leds/blob/main/dos%20les%20prendidos.png?raw=true)

Nivel de 20 a 30 cm

![](https://github.com/UrielMastache/ESP32-Sensor-Nivel-Con-Leds/blob/main/tres%20leds%20prendidos.png?raw=true)

Nivel de 30 a 40 cm

![](https://github.com/UrielMastache/ESP32-Sensor-Nivel-Con-Leds/blob/main/leds%20prendidos.png?raw=true)

Nivel de tanque de 40 a 45 cm (Simulando tanque lleno ) *Aquí para denotar la diferencia entre el llenado de 30 a 40 y el llenado total, los leds parpadearan para avisar que el tanque esta en el limite.

Posteriormente llegando al limite o superandolo todo se apaga.

![](https://github.com/UrielMastache/ESP32-Sensor-Nivel-Con-Leds/blob/main/Tanque%20lleno%20apagado%20todo.png?raw=true)


## Comentarios

Recuerda que esto es demostrativo, por ese motivo los valores estan en cm, y son muy cercanos, sin embargo, aplicando esto a un nivel real, se puede modificar a su gusto.


Gracias por ver :D 

Ciao.