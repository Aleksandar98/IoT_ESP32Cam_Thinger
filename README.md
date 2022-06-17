# IoT_ESP32Cam_Thinger

# Thinger.io i Edge computing sa ESP32 Cam modulom

IoT_ESP32Cam_Thinger aplikacija analizira podatke na Edge-u u vidu lokalne detekcije subjekta preko ESP32 Cam modula kako bi rasteretio cloud.

Pri pokretanju aplikacije startuje se lokalni web server koji dozvoljava kreiranje modela lica za prepoznavanje i konfigurisanje samog ESP32 Cam modula.

Tacnu IP adresu servera mozemo naci u serialnom monitoru na COM portu koji je modul dobio kada smo ga povezali na racunar sa boud rate-om od 115200

```c++
Serial.begin(115200);
```

## Izlaz u serialnom monitoru
![Alt text](https://github.com/Aleksandar98/IoT_ESP32Cam_Thinger/blob/main/images/arduino_serial.png?raw=true "Optional Title")

## Izgled web servera za konfiguraciju
![Alt text](https://github.com/Aleksandar98/IoT_ESP32Cam_Thinger/blob/main/images/esp32cam_config.png?raw=true "Optional Title")

Modlu komunicira sa Thinger.io platformom tako sto se prvobitno na nju povezuje u setup delu programa
```c++
ThingerESP32 thing(USERNAME, DEVICE_ID, DEVICE_CREDENTIAL);

void setup() {
...
thing.add_wifi(SSID, SSID_PASSWORD);
...
}
```

Potom u dvosmernoj komunikaciji sa Thinger.io platformom modlu salje podatke kada je detektovao prethodno registrovano lice i pobudjuje jedan od GPIO dostupnih pinova na modulu kako bi pokrenuo reley i aktivirao elektromagnet za otvaranje vrata

## Read i write komunikacija sa platformom
```c++
...
 thing["otkljucaj"] >> digitalPin(4);
...
 thing["Vrata otkljucana"] << inputValue(openLock);
...
```

## Mapa pinova na ESP32 Cam modulu

![Alt text](https://github.com/Aleksandar98/IoT_ESP32Cam_Thinger/blob/main/images/esp32pins.png?raw=true "Optional Title")

# Thinger.io

Ovako izgleda Devices tab ako se ESP32 povezao sa Thinger.io platformom

![Alt text](https://github.com/Aleksandar98/IoT_ESP32Cam_Thinger/blob/main/images/devices_dashboard.png?raw=true "Optional Title")

U Api tabu u okviru Devices sekcije moguce je slati komande do modula 

![Alt text](https://github.com/Aleksandar98/IoT_ESP32Cam_Thinger/blob/main/images/devices_api.png?raw=true "Optional Title")