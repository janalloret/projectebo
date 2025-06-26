# PROJECTE FINAL PROCESSADORS DIGITALS: CONTROL D’UNA MÀ ROBÒTICA VIA WEB

### Autors
- Jana Lloret Sellabona
- Marta Pitarch Granell

## 1. Introducció
Aquest projecte consisteix a dissenyar i desenvolupar un sistema funcional per controlar una mà robòtica a distància a través d’una pàgina web, utilitzant un navegador i un microcontrolador ESP32.

## 2. Objectius del projecte
- Crear una interfície web intuïtiva i fàcil d'utilitzar per seleccionar el dit i l’angle a moure.
- Controlar diversos servomotors que representen els dits de la mà robòtica.
- Establir comunicació eficient entre el navegador web i el microcontrolador ESP32.
- Integrar diferents components en un sistema robust i coordinat.

## 3. Procés de desenvolupament
### 3.1 Impressió i muntatge de la mà
- Utilització de la mà robòtica del projecte InMoov, amb peces impreses en 3D proporcionades pel professor.
- Desenvolupament d’un sistema propi combinant HTML, Arduino i/o ESP32.

### 3.2 Arquitectura general del sistema

| Component     | Funció principal                                               |
|---------------|--------------------------------------------------------------|
| ESP32         | Microcontrolador que genera una xarxa WiFi i rep ordres.    |
| PCA9685       | Driver I2C per controlar múltiples servomotors amb precisió.|
| Interfície Web| Formulari HTML per enviar ordres des del navegador.          |
| Usuari final  | Interactua amb el sistema mitjançant la pàgina web.         |

## 4. Explicació del codi
### 4.1 Configuració punt d’accés i servidor
```cpp
const char* ap_ssid = "MA_ROBOTICA"; 
const char* ap_password = "12345678"; 
WiFi.softAP(ap_ssid, ap_password);
El microcontrolador crea un punt d'accés per a connexions sense necessitat d'internet.
```
### 4.2 Interfície web

Permet:

Seleccionar el dit a moure.
Indicar l’angle entre 0° i 180°.
Enviar la petició GET al servidor.
```cpp
<form action="/mou" method="GET"> 
  <label for="servo">Selecciona un dit:</label> 
  <select id="servo" name="servo">...</select> 
  <label for="angle">Angle (0-180):</label> 
  <input type="number" id="angle" name="angle" min="0" max="180"> 
  <input type="submit" value="Moure"> 
</form>
```
### 4.3 Control dels servos amb PCA9685

```cpp
uint16_t angleAServoPWM(uint8_t angle) {
    return map(angle, 0, 180, 50, 400); 
}
```

Conversió de l'angle a valor PWM per controlar els servos.
### 4.4 Diagrama de blocs

![image](https://github.com/user-attachments/assets/ce3692f7-4633-4911-80d1-100031433a34)

### 4.5 Diagrama de flux del sistema
![image](https://github.com/user-attachments/assets/25f5aa1d-3eb7-48fa-a92e-5ccd0a24a07b)

#### 1. Inicialització:
   
    S'inicia la comunicació serial.
    Es configura el bus I2C pels controladors PCA9685.
    Es crea un punt d'accés WiFi.
    S'inicia el servidor web asíncron.

#### 2. Rutes web:
   
    /: Mostra un formulari HTML per seleccionar dit i angle.
    /mou: Processa la petició per moure el servo.
#### 3. Loop principal:
    Buit, ja que el servidor gestiona les peticions de manera asíncrona.
   
#### Flux de dades:

Client Web → Sol·licita formulari → Servidor → Retorna HTML.
Client Web → Envia dades (servo, angle) → Servidor → Mou servo → Confirma acció.
## 5. Conclusions

El projecte ha permès comprendre:

Comunicació entre microcontrolador i interfície web.
Ús de controladors com el PCA9685 per controlar servos.
Futures millores podrien incloure:

Controlar múltiples dits alhora.
Afegir sensors de pressió als dits.
Si necessites més informació o ajustos en el format Markdown, estaré encantat d'ajudar-te! També pots visualitzar el contingut pujat del document en la pàgina detallada.


Si tens més preguntes o necessites ajustar el format Ma
