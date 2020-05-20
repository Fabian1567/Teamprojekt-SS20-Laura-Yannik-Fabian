# Woche 2:
Das Erstellen einer Fork hat ohne Probleme geklappt. <br>
Das Ausführen der graphischen Komponenten hat unter Windows (bei Fabian & Laura) nicht funktioniert, da es zu Problemen mit pyopenms kam (siehe Screenshots). <br>
Nur das Ausführen der Dateien annotateSpectrum.py, convertToMGF.py, filter.py und PhosphoScoring.py hat funktioniert.<br>

Fehlermeldung Fabian: <br>
![Fehlermeldung1](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Fehlermeldung.PNG.jpg) <br>

Fehlermeldung Laura: <br>
![Fehlermeldung2](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/FehlerGUIMapWidget.png) <br>

Bei Yannik, der Elementary verwendet, hat das Ausführen der Dateien funktioniert.<br>
Yannik: <br>
![Erfolg1](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/pyopenmsSuccess.png) 
<br>

Der flake8 Test konnte nach kurzer Recherche hinzugefügt werden und läuft so wie er sollte.


# Woche 3:
Der fix/style branch wurde problemlos erstellt und mithilfe von black, autopep8, Jetbrains PyCharm und Handarbeit fast vollständig flake8 kompatibel gemacht.
Folgende Probleme traten dabei auf:
*  autopep8 setzte, gemäß E402, modul level imports an den Anfang der File. Die in manchen Files verwendete line "sys.path.include()" verlangt aber diesen import unter sich, weshalb E402 nicht erfüllt werden kann und deaktiviert werden sollte. (Begründung unbekannt, herausgefunden per trial&error)
*  Sowohl W503 als auch W504, die sich auf die Position von Zeilenumbrüchen bei Binäroperatoren beziehen, sind standardmäßig aktiv und schließen damit praktisch Zeilenumbrüche bei Binäroperationen aus. Eins davon sollte deaktiviert werden. 
*  Die maximale Zeilenlänge von 79 bezieht sich auch auf Kommentare, alle gefundenen Tools ignorieren diese allerdings. Der Großteil der Handarbeit stammte daher. 
*  Je ein Vorkommen von F821 und E741 konnte ohne weiteres Wissen über die Funktion des Programms nicht korrigiert werden.

Insgesamt hätte es Zeit gespart sich vorher zu überlegen, ob anders mit Kommentaren umgegangen werden kann und wie das Zusammenspiel von W503 und W504 gelöst werden soll, da sonst fast alles von den erwähnten Tools abgedeckt wurde. 
