# NIVEL DE AGUA CON LCD
## Practica con un sensor ultrasonico en una placa de desarrollo ESP32 y un LCD de 12C 
Este repositorio muestra como podemos programar una **ESP32** con el sensor **HC-SR04** y mostrar los datos optenidos en un **LCD 12c**.

### Introducción
**Descripción:** 
La **ESP32** la utilizamos en un entorno de adquision de datos, en esta practica ocuparemos un **sensor ultrasonico** para medir la distancia de un tanque de agua, como tambien un **LCD de 12c** para visualizar la distancia y porcentaje del tanque, como uso de **modulos de relevadores** para tener indicadores visuales del nivel del tanque de agua, todo siendo simulado en una pagina llamda **WOKWI**

### Material Necesario
Para realizar esta practica necesitas lo siguiente:
- WOKWI
- Tarjeta ESP32
- Sensor ultrasonico HC-SR04
- modulos de relavadores
- LCD (16x2) 12c

### Requisitos previos:
Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.

### Instrucciones de preparación de entorno:
1.-Abrir la terminal de programación y colocar la siguente programación:
```
// defines pins numbers
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 2;
const int led2 = 5;
const int led3 = 18;
const int led4 = 17;

#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

// defines variables
long duration;
int distance;
int distancia;
int safetyDistance;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
  lcd.init();
  lcd.backlight();
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

// Calculo de la distancia
//distance= duration*0.034/2;
distancia= int(0.01716*duration);

safetyDistance = distancia;
if (safetyDistance>=2 && safetyDistance<=5) //90% TANQUE
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
lcd.clear(); 
  lcd.setCursor(4, 0);
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(1000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("diego bahena");
  lcd.setCursor(6, 1);
  lcd.print("I.E.E");
  delay(1000);

lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distancia)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 90%");
  delay(2000);
}
else if(safetyDistance>=5 && safetyDistance<=10) //75% TANQUE
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
lcd.clear(); 
  lcd.setCursor(4, 0);
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(1000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("diego bahena");
  lcd.setCursor(6, 1);
  lcd.print("I.E.E");
  delay(1000);

lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distancia)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 75%");
  delay(2000);
}
else if(safetyDistance>=10 && safetyDistance<=45) //50% TANQUE
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
lcd.clear(); 
  lcd.setCursor(4, 0);
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(1000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("diego bahena");
  lcd.setCursor(6, 1);
  lcd.print("I.E.E");
  delay(1000);

lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distancia)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 50%");
  delay(2000);
}
else if(safetyDistance>=45 && safetyDistance<=70) //35% TANQUE
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
lcd.clear(); 
  lcd.setCursor(4, 0);
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(1000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("diego bahena");
  lcd.setCursor(6, 1);
  lcd.print("I.E.E");
  delay(1000);

lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distancia)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 35%");
  delay(2000);
}
else  //5% TANQUE O MENOS
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
lcd.clear(); 
  lcd.setCursor(4, 0);
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(1000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("diego bahena");
  lcd.setCursor(6, 1);
  lcd.print("I.E.E");
  delay(1000);

lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(distancia)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 5%");
  delay(2000);
}

// Prints the distance on the Serial Monitor
Serial.print("Distancia: "  );
Serial.println(distancia);
delay (2000); 
}
```

2.- Instalar la libreria de **LiquidCrystal I2C** como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/653d1f67-6d5a-4db8-a26c-4dd5ee6eb3fc)

3.- Hacer la conexion de **HC-SR04** con la **ESP32** y el **LCD 12C** como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/5ac3049f-a220-4dc1-916e-6b2edaf713e2)

### Instrucciónes de operación
- Iniciar simulador.
- Visualizar los datos en el LCD.
- visualizar la secuencia de leds dependiendo del nivel del tanque de agua
- Colocar la distancia dando click al sensor ultrasonico HC-SR04
  
### Resultados
Cuando haya funcionado, verás los valores dentro del LCD como se muestra en las siguentes imagenes.

-Tanque al 90% de nivel de agua.

-led 1 encendido, led 2,3,4 apagados.

![image](https://github.com/user-attachments/assets/c72a3fc9-e181-4dc7-a030-9408ba2af07d)

![image](https://github.com/user-attachments/assets/42044288-3135-428f-8308-309d27574e9d)

![image](https://github.com/user-attachments/assets/863d05fc-9cf4-4b1a-a996-2450e645ae3c)

-Tanque al 75% de nivel de agua.

-led 1 y 2 encendidos, led 3,4 apagados.

![image](https://github.com/user-attachments/assets/9778a9b8-fcfc-4613-8e17-122cfe6629b0)

![image](https://github.com/user-attachments/assets/8aa23a73-9a98-4e80-8211-7f97f4117ffb)

![image](https://github.com/user-attachments/assets/8615c2da-2b53-4be8-8e59-2617f4220da7)

-Tanque al 50% de nivel de agua.

-led 3 encendido, led 1,2,4 apagados.

![image](https://github.com/user-attachments/assets/fd39c50c-470a-4750-afe0-29a4122a3e22)

![image](https://github.com/user-attachments/assets/4c3a00b7-a1bc-4d72-aa5a-62a67538529d)

![image](https://github.com/user-attachments/assets/b158c826-2cad-43a9-bd50-72caba970769)

-Tanque al 35% de nivel de agua.

-led 3 y 4 encendidos, led 1,2 apagados.

![image](https://github.com/user-attachments/assets/2c7df680-caa7-4172-9879-724fe1fcd03a)

![image](https://github.com/user-attachments/assets/951bfaef-c14f-401d-bf60-d214e0e6a0b0)

![image](https://github.com/user-attachments/assets/20202fbd-4d95-4ed8-b341-f94875bf4840)

-Tanque al 5% de nivel de agua.

-led 1,2,3,4 apagados.

![image](https://github.com/user-attachments/assets/de096388-9ecc-413b-9ceb-66d2e33f9a2e)

![image](https://github.com/user-attachments/assets/025f954b-f7bf-4bbc-ab3d-a56da699fc6c)

![image](https://github.com/user-attachments/assets/068bdd8a-5031-4dc9-8d24-c74c2edff5e7)

### Desarrollado por 
Diego David Bahena Galan

[GitHub](https://github.com/DiegoDBG)
