# CNNs Convolutional Neural Networks

## Test datenset: 
    MNIST (Modified National Institute of Standards and Technology)

## Feature:
Beschreibt die Eigenschaften von Eingabedaten, z.B:
1. Pixelwerte in einenm Bild
2. Zanhlenwerte wie Umsatz, Alter, Anzahl,...
3. Bestimmte Buchstaben in einem Dokument
4. ...
    
Die anzahl an möglichen Features ist dabei nicht limitiert
    
![features](./images/features.png)

## 1. Filtern:
1. Ausrichten der Features auf den Bildausschnitt.
2. Multiplikation eines jeden Bildpixel mit dem zugehörigen Feature-Pixel
3. Addition der Produkte.
4. Teilen durch die Gesamtzahl der Pixel des Features.
![filter](./images/filtern1.png)
![filter](./images/filtern2.png)
![filter](./images/filtern3.png)
![filter](./images/filtern4.png)

## 2. Convolution
Pürfen auf alle möglichen Übereinstimmungen
![convolution](./images/convolution.png)
![convolution](./images/convolution2.png)
![convolution](./images/convolution3.png)

- Feature + convolution => feature-map

### Convolution layer
Ein Bild wird zu einem Stapel gefilterter Bilder
![convolution4](./images/convolution4.png)
![convolution5](./images/convolution5.png)

## 3. Pooling
Verkleinern des Bildstapels
1. Wählen einer Fenstergröße (normaleweise 2x2px oder 3x3px)
2. Wählen einer Schnittweite (typisch: 2px)
3. Mit dem Fenster über die gefilterten Bilder "gehen"
4. Aus jedem Fenster den Maximalwert nehmen

![pooling1](./images/pooling1.png)
![pooling2](./images/pooling2.png)

### Stapel von Bilder werden verkleinert
Wir behalten bestimmte Merkmale, auch wenn das Bild nicht perfekt ist
![pooling3](./images/pooling3.png)

## 4. Normalisierung (Umstritten)
1. Reduktion von Rechnemaufwand durch Modifikation einzelner Werte.
2. Negative Zahlen werden auf Null (0) gesetzt.
### Rectified Linear Units (Relu's)
![relu1](./images/relu1.png)
![relu2](./images/relu2.png)
![relu3](./images/relu3.png)

## Layer werden in Schichten (Stacks) angeordnet
Das Ergebnus einer Schicht wird zur Eingangsinformation (Input) der nächsten Schicht
![stacks](./images/stacks.png)
## Erzeugung tiefer Schichten (Deep Stacking)
Ebenen können einige (oder auch viele) Male wiederholt werden
![deep-stacking](./images/deep-stacking.png)

=> Frage: wie kommmen wir zu Ergebniss ?

## Fully connected Layer
Jeder Wert ist stimmberechtigt in Bezug auf das Ergebnis
![fully-connected-layer](./images/fully-connected-layer.png)
Zukünftige Werte stimmen für X oder O ab
![Ergebnis](./images/fully-connected-layer2.png)
Eine Liste von Features wird zu einer Liste von Stimmen
![Ergebnis](./images/fully-connected-layer3.png)
Diese können auch gestapelt werden
![fully-connected-layer4](./images/fully-connected-layer4.png)
Ein Satz von Pixel wird zu einem Satz von Stimmen
![fully-connected-layer5](./images/fully-connected-layer5.png)

## Beispiel code:
### input-layer: 
(None, 244, 244, 3) => Eingabeformat 244x244 Px, RGB: 3
### block1-conv1 (Conv2D): 
(None, 224, 224, 64) => Features: 64

in der ausgabe sehen wir:
1. Bildgrösser werden verkleinert
2. Anzahl der Features zunehmmen
=> immer mehr details 
   
###Interessant:
Total params: 138,357,544

# Woher kommen all die magischen Zahlen ?
- Features in convolutional layers
- Voting weights in fully connected layers
## Backprogagation
Fehler = richtige Anwort - aktuelle Antwort
![backpropagation](./images/backpropagation.png)
### Gradientenabstieg (Grdient descent)
Für jedes Features-Pixel und jde Gewichtung (weight) passen wir das Gewicht ein wenig nach oben und unten an und sehen, 
wie der Fehler sich ändern
![Gradientenabstieg](./images/gradient-descend.png)
![Gradientenabstieg](./images/gradient-descend1.png)

### Slope
![Slope](./images/slope.png)
### Fehlerfunktion
Den Slope direkt berechnen
![Fehlerfunktion](./images/error-cal.png)
### Lernrate
#### Klein
Lernrate ist zu klein und benötigt zu viel Rechnenleistung
![Kleine Lernrate](./images/learning-rate-small.png)
#### Gross
Lernrate ist zu gross und verhält sich unvorhersehbar
![Grosse Learnrate](./images/learning-rate-large.png)
#### Optimal
Erreicht schnell niedrige Fehlerwerte
![Optimale Lernrate](./images/learning-rate-optimal.png)
#### Learnrate vs Performance
Erreicht schnell niedrige Fehlerwerte
![Optimale Lernrate](./images/learning-rate-vs-performance.png)
#### Falsches Minima vs globale Minima
![Optimale Lernrate](./images/locale-min-vs-global-min.png)
## Hyperparameter
### Convolution
- Anzahl der Features
- Größe der Features
### Pooling
- Fenstergröße
- Fensterschnitt
### Fully Connected
- Anzahl der Neuronen
## Architektur
- Wie viele von jeden Layer ?
    * in welcher Reihensfolge ?
## Nicht nur Bilder
- Alle 2D- (oder 3D-) Daten
- Dinge, die näher beieinander liegen, sind enger miteinander verbunden als Dinge, die weit weg sind
### Bilder
![Bilder](./images/pictures.png)
### Sound
![Bilder](./images/sound.png)
### Text
![Bilder](./images/text.png)

## Limitierungen
- ConvNets erfassen nur locale "räumliche" Muster in Daten
- Wenn die Daten nicht wie ein Bild aussehen können, sind ConvNets weniger nützlich
  ![customer data](./images/customer-data.png)
## CNN Daumenregel
Wenn die Daten genauso nutzlich sind, nachdem wir eine Ihrer Spalten miteinander vertauscht haben, dann können wir
Convolutional Neural Networks nicht verwenden
CNN sind hervorragend darin, Muster zu finden und damit Bilder zu klassifizieren.
