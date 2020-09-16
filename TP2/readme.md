# Compte rendu TP2

 - Elève 1: Jérémy LAURENT
 - Elève 2: Louis MORANDET (Absent)
 - Elève 3: Yoann DREVET (Remplaçant)
 - binôme: N°18, puce 825

## Exercice 1: Feu de circulation
> Pour cet exercice, vous allez programmer le comportement d’un feu de
> circulation. En utilisant des temporisateurs comme la fonction
> microbit.sleep(n) si vous êtes sur Python ou sleep(ms) en C, le but de
> cet exercice sera de simuler le changement de l’état d’allumages des
> LEDs. Pensez bien à garder l’état d’allumage, vous pouvez utiliser la
> structure switch/case.

code python:

    from microbit import *
	while True:
	    pin0.write_digital(1)
	    pin1.write_digital(0)
	    pin2.write_digital(0)
	    sleep(2000)
	    pin0.write_digital(0)
	    pin1.write_digital(0)
	    pin2.write_digital(1)
	    sleep(800)
	    pin0.write_digital(0)
	    pin1.write_digital(1)
	    pin2.write_digital(0)
	    sleep(2000)

![enter image description here](https://raw.githubusercontent.com/JeremyL71/IoT_cpe/master/TP2/exo1.jpg)

code C++ (utiliser Mbade)

    #include "MicroBit.h"

	MicroBit uBit;

	int main() {
	  MicroBitPin FeuRouge = uBit.io.P0;
	  MicroBitPin FeuOrange = uBit.io.P1;
	  MicroBitPin FeuVert = uBit.io.P2;
	  // Initialise the micro:bit runtime.
	  uBit.init();
	  while (1) {
	    FeuVert.setDigitalValue(1);
	    uBit.sleep(3000);
	    FeuVert.setDigitalValue(0);
	    FeuOrange.setDigitalValue(1);
	    uBit.sleep(1000);
	    FeuOrange.setDigitalValue(0);
	    FeuRouge.setDigitalValue(1);
	    uBit.sleep(3000);
	    FeuRouge.setDigitalValue(0);
	  }

	  // If main exits, there may still be other fibers running or registered event handlers etc.
	  // Simply release this fiber, which will mean we enter the scheduler. Worse case, we then
	  // sit in the idle task forever, in a power efficient sleep.
	  release_fiber();
	}

## Exercice 2: LED RGB Neopixel

> Pour cet exercice vous allez récupérer le matériel demandé dans la Figure 4. À partir des exemples présents sur internet, créez le support d’une led RGB de type Neopixel (voir https://www.adafruit.com/product/1312) dans votre nouvelle application, ce type de LED permet de connecter plusieurs LEDs en chaîne. La LED doît être connectée de cette façon : 
> 
> — Pin + à la sortie +3.3V du micro-contrôleur 
> 
> — Pin G à la sortie GND du micro-contrôleur 
> 
> — Pin I à une sortie GPIO, dans le code donné ça sera le GPIO0_19. 
> 
Pour connecter plusieurs LEDs en chaîne vous devez connecter le pin O de la première LED au pin I de la LED suivante et les pins + et G entre les deux LEDs.
> 
> Plusieurs exemples de code pour gérer ce type de LED existent sur internet, prenez le temps de bien comprendre les codes et les tester avec une LED. Modifiez ce code pour itérer entre les couleurs bleu, blanc, rouge à une durée de 250ms. Puis si vous avez le temps, ajoutez une deuxième/troisième LED selon la disponibilité de matériel et tester avec plusieurs LEDs

code python:
 
    from microbit
	import *
	import neopixel

	np = neopixel.NeoPixel(pin0, 2)
	rouge = (255, 0, 0)
	blanc = (255, 255, 255)
	bleu = (0, 0, 255)

	while True:
	  np[0] = bleu
	np[1] = bleu
	np.show()
	sleep(250)
	np[0] = blanc
	np[1] = blanc
	np.show()
	sleep(250)
	np[0] = rouge
	np[1] = rouge
	np.show()
	sleep(250)

![enter image description here](https://raw.githubusercontent.com/JeremyL71/IoT_cpe/master/TP2/exo2.png)

## Exercice 3: Capteurs météo

> Pour cet exercice vous allez récupérer le matériel demandé dans la Figure 5. Cette puce regroupe plusieurs capteurs environnementaux que vous allez devoir interroger pour obtenir leurs valeurs. 
> Ces valeurs seront affichées sur la matrice LED de votre micro :bit.. Le module sensors a une interface I2C pour pouvoir accéder à ses données, la distribution des pins est présenté dans la figure 5. 
> 
> Ce module intègre les capteurs suivants avec ces fonctionnalités : 
> 
> — TSL2561 : Lumière visible et infra-rouge 
> 
> — VEML6070 : Lumière UVA 
> 
> — BME280 : Température, Humidité, Pression
> 

Code python (bloc):

    BME280.power_on()
	def on_forever():
	basic.show_string("" + str(BME280.temperature(BME280_T.T_C)) + " C " + str(BME280.pressure(BME280_P.PA)) + " Pa " + str(BME280.humidity()) + "%")
	basic.forever(on_forever)

## Exercice 4. Écran mono-couleur

> Pour cet exercice vous allez récupérer le matériel demandé dans la Figure 6. Dans cette exercice le but est de pouvoir afficher sur l’écran la valeur de la température obtenue à partir du capteur intégré au module micro :bit ainsi que les noms des intégrants de votre groupe de travail. 
> Avant d’afficher directement les informations, assurez vous de comprendre comment afficher des informations sur cet écran. 
> Pour l’accès à l’écran nous allons utiliser l’interface I2C pour pouvoir envoyer les informations à afficher, on positionne les données en indiquant la ligne à utiliser, la distribution des pins est présenté dans la figure 7. 
> Pour finir, affichez aussi la température obtenue à partir du capteur sensors pour la comparer à celle intégrée au micro-contrôleur.

Ma réponse


## Exercice 5: Écran mono-couleur

Vérification des devices présents:

    from microbit
	import *

	i2c.init()
	devices = i2c.scan()

	print(len(devices)) # Combien de périphériques’

	for device in devices:
	  print(hex(device))
	  
![enter image description here](https://raw.githubusercontent.com/JeremyL71/IoT_cpe/master/TP2/exo5.jpg)