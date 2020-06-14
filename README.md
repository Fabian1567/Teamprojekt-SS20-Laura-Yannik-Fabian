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
Dem Tutorial ein package zu erstellen wurde gefolgt und es hat auch alles ohne Probleme funktioniert.
Das package kann unter https://pypi.org/project/pyopenms-extra-Fabian-Yannik-Laura/0.0.1/ gefunden werden.
![Install Package](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Package.PNG)


Der fix/style branch wurde problemlos erstellt und mithilfe von black, autopep8, Jetbrains PyCharm und Handarbeit fast vollständig flake8 kompatibel gemacht.
Folgende Probleme traten dabei auf:
*  autopep8 setzte, gemäß E402, modul level imports an den Anfang der File. Die in manchen Files verwendete Line "sys.path.include()" verlangt aber diesen Import unter sich, weshalb E402 nicht erfüllt werden kann und deaktiviert werden sollte. (Begründung unbekannt, herausgefunden per trial&error)
*  Sowohl W503 als auch W504, die sich auf die Position von Zeilenumbrüchen bei Binäroperatoren beziehen, sind standardmäßig aktiv und schließen damit praktisch Zeilenumbrüche bei Binäroperationen aus. Eins davon sollte deaktiviert werden. 
*  Die maximale Zeilenlänge von 79 bezieht sich auch auf Kommentare, alle gefundenen Tools ignorieren diese allerdings. Der Großteil der Handarbeit stammte daher. 
*  Je ein Vorkommen von F821 und E741 konnte ohne weiteres Wissen über die Funktion des Programms nicht korrigiert werden.

Insgesamt hätte es Zeit gespart sich vorher zu überlegen, ob anders mit Kommentaren umgegangen werden kann und wie das Zusammenspiel von W503 und W504 gelöst werden soll, da sonst fast alles von den erwähnten Tools abgedeckt wurde. 

IDViewer.py: <br>
Die Fehlermeldung beim Ausführen von IDViewer.py auf Windows:<br>
![Fehlermeldung IDViewer.py](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Windows-Fehler-IDViewer.png) <br>
Fabian: <br>
Unter Windows hat das Ausführen der IDViewer.py nicht funktioniert, da es nicht das erste Problem war was nur unter Windows auftritt, wurde eine Virtual Machine mit Ubuntu aufgesetzt.
Unter Ubuntu ließ sich, nach beheben eines kleinen Problems, die IDViewer.py ausführen, jedoch werden die TIC Werte nicht angezeigt und im Terminal sthet No TIC values in spectrum.
![IDViewer.py Fabian](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Idviewer.PNG)
Folgender Output wird im Terminal geprintet:
![Output IDViewer.py](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Output%20IDViewer.PNG)
Das Einfügen einer zweiten identischen Tabelle hat über einen zweiten Aufruf des ScanTableWidget in der ControllerWidget.py funktioniert, jedoch erst nachdem nach etlichen fehlversuchen bemerkt wurde, dass auch ein neuer Eintrag in der widget_height liste hinzugefügt werden muss.<br>
Die Änderungen hierfür wurden zunächst auf dem Fabian Branch gespeichert
![SecondScanTableWidget](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Second%20ScanTableWidget.PNG)

# Woche 4 & 5:
Es wurde ein Widget erstellt, dass eine mzTab-Datei  einliest und zur Visualisierung der Datei zwei Tabellen erstellt, die die Proteine und PSMs aus der Datei auflisten.<br>
Der Parser wurde hierbei wie folgt programmiert und filtert zum Einen die Header beider Tabellen, zum Anderen die Proteine mit 'PRT' und die PSMs mit 'PSM' am Anfang heraus, wobei bei den Proteinen zwischen 'single_protein' und 'indistinguishable_protein_group' in der letzten Spalte unterschieden wird. <br>
![ParserFabi](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/ParserFabian.png)<br>
<br>
Die Tabellen wurden mit QTableWidget erstellt und wurden wegen der Spaltenlänge untereinander angeordnet.<br>
Hierbei wurden zwei Funktionen (createProtTable und createPSMTable) erstellt, die jeweils die Tabellen zeichnen und nacheinander die Zeilen der mzTab-Datei einlesen, die durch den Parser übermittelt wurden.<br>
(TableWidget1 -> Proteine, TableWidget2 -> PSMs)<br>
<b>
![TablesLaura](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/TablesMzTab.png)<br>
 <br>
Der Output der Datei sah danach so aus:<br>
 <br>
![OutputTables](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/OutputMzTab.png)<br>
<br>
 Dann folgte das Verlinken beider Tabellen.<br>
 Hier haben wir dafür zwei Funktionen zum Filtern der Tabellen erstellt, um dafür zu sorgen, dass beim Anklicken eines Proteins nur die PSMs, auf die das Protein verweist, angezeigt werden und anders herum, dass beim Anklicken eines PSMs die dazugehörigen Proteine angezeigt werden.<br>
Es wird dafür jeweils der Inhalt in der Spalte accession miteinander verglichen.<br>
![VerlinkenYannik](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/VerlinkenTabellen.png)<br>
 <br>
Output nach Verlinken der Tabellen: <br>
Beim Auswählen eines Proteins:
 <br>
![VerlProt](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/VerlinktePRT.png)<br>
 <br>
Beim Auswählen eines PSMs:
 <br>
![VerlPSM](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/VerlinktePSM.png)<br>
 
# Woche 6:
Unter Type Hinting versteht man die direkte anmerkung der Typen der ein und ausgabe Parameter einer Funktion in deren Definition.
Bsp.: <br>
 def add(a: int, b: int) -> int: <br>
   return a + b; <br>
Es ist sinnvoll dies anzuwenden, da man so bei einer unbekannten Funktion nsofort weiss welche Parameter diese annimt und was sie ausgibt ohne in den Kommentaren / im docstring nachlesen zu müssen, da es für diese verschiedene Normen gibt und es dadurch nicht immer sofort ersichtlich ist.






