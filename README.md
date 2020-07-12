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
Der Code wurde insofern geändert, dass die Tabelle mit der drawTables()-Funktion einmal gezeichnet wird und bei jedem Update/Filtern durch createProtTables() und createPSMTables() jeweils die Zeilenanzahl geändert und die Tabelle gefüllt wird.
<br>
![LauraTables](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/LauracreateTables.png)
<br>
Außerdem wurden die Header jetzt richtig gesetzt und befinden sich nicht mehr in der ersten Zeile der Tabellen.
Die erste Spalte, die nur 'PRT' oder 'PSM' enthalten hat, wurde ebenfalls gelöscht.
Der Output unseres Widgets sieht jetzt so aus:
<br>
![OutputTables](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/OutputTablesLaura.png)
<br>
Wir haben den Code nach dem NumPy docstring Standard kommentiert.
<br>
Unter Type Hinting versteht man die direkte Anmerkung der Typen der Eingabe- und Ausgabe-Parameter einer Funktion in deren Definition. <br>
Bsp.: <br>
 def add(a: int, b: int) -> int: <br>
   return a + b; <br>
Es ist sinnvoll dies anzuwenden, da man so bei einer unbekannten Funktion sofort weiss, welche Parameter diese annimmt und was sie ausgibt, ohne in den Kommentaren / im docstring nachlesen zu müssen, da es für diese verschiedene Normen gibt und es dadurch nicht immer sofort ersichtlich ist.

# Woche 7:Laufzeit: <br>
Es wurde getestet wie die Laufzeit bei kleineren Dateien aussieht und auch bei Dateien mit über 1000 Zeilen lief alles sofort und ohne jegliche Laufzeit Probleme. 
Die mzTab file die wir aber bekommen haben hat über 300 Tausend relevante Zeilen für das Programm was zu der hohen Laufzeit führt. Eine Lösung für das Problem ist uns nicht ersichtlich, da unser Filter lediglich eine Schleife benötigt und wir nicht wissen, wie man diesen noch verschnellern sollte. Um das Einlesen zu verschnellern wäre die einzige mir ersichtliche Lösung eine Datenstruktur zu verwenden, welche es uns ermöglicht ganze Zeilen auf einmal in die Tabellen einzufügen und nicht über jede einzelne Kachel iterieren zu müssen, hierfür fehlte uns jedoch die Zeit und das nötige Wissen. <br>

<br> Unser bisheriges Laufzeitproblem lässt sich auf das Befüllen der vollständigen PSM-Tabelle zurückführen, was sowohl beim Start der Anwendung, als auch beim Aufheben eines Filters passiert. Gefilterte Teilmengen stellen dagegen kein wirkliches Problem dar. Der vorgeschlagene Ansatz Dictionaries zum Vorsortieren zu verwenden optimiert daher leider nur einen Teil des Programms, der bereits mit akzeptabler Geschwindigkeit läuft. <br>
<br> Ein weiterer Ansatz war es, die Tabelle nicht neu aufzufüllen, wenn man das Filtern rückgängig machen möchte, sondern stattdessen Zeilen je nach Kontext zu verstecken bzw. wieder sichtbar zu machen. Dadurch wurde jedoch für jeden Befehl durch die gesamte Tabelle iteriert, wodurch dann auch das filtern langsam wurde. <br>
<br> Dieser Ansatz führte jedoch zu der jetzt umgesetzten Lösung, ganze Tabellen zu verstecken. Die Anwendung besteht nun aus vier tableWidgets, zwei davon werden genau einmal zu Beginn mit den vollständigen Daten befüllt, die anderen Beiden starten leer und versteckt. Wenn eine gefilterte Tabelle angezeigt werden soll, wird die zugehörige vollständige Tabelle versteckt, die zu Beginn Leere mit den relevanten Daten aufgefüllt und sichtbar gemacht. Der bisher kritische Vorgang, den Filter wieder rückgängig zu machen, wird nun dadurch erreicht, dass die zu Beginn volle Tabelle einfach wieder sichtbar und die gefilterte Tabelle unsichtbar gemacht wird. <br>
<br> Erreicht wird dies über eine Klickfunktion, eine für jede Tabellenart, die den momentanen Zustand des Programms ermittelt und danach entscheidet, was angezeigt bzw, versteckt wird. <br>

Die Uniprot Suche wurde so implementiert, dass beim doppelklicken auf eine Zeile die jeweilige Uniprot Seite für das Protein dieser Zeile geöffnet wird. <br>
![UniprotSuche](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Uniprot%20Suche%202.PNG)
![UniprotSuche](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/Uniprot%20Suche.PNG) <br>

![HideColumnsPRT](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/hidePRTColumns.PNG)
![HideColumnsPRT](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/hidePSMColumns.PNG) <br>
Konstante columns werden nun standardmäßig ausgeblendet. Dies wird einfach dadruch erreicht, dass gecheckt wird ob jedes Element in einer column gleich ist und falls dies der Fall ist, wird die column ausgeblendet. Für das Implementieren eines buttons zum einblenden dieser columns fehlte jedoch die Zeit.<br>
Es wurde ebenfalls versucht, innerhalb der hidePRTColumns bzw hidePSMColumns die Tabelleneinträge von Nummern von Strings zu Nummern als Datentyp zu konvertieren, da hier sowieso noch einmal die Tabellen ganz durchlaufen werden. <br>
![SaveNumbers](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/SaveNumbers.png)<br>
Allerdings haben wir hier eine Fehlermeldung erhalten "TypeError: 'float' object is not subscriptable", die sich auf die Vergleiche der Einträge in den if-Bedingungen bezogen hat. Darum ist dieses Feature momentan nicht im Widget enthalten.<br>
<br>
Unter stacktrace versteht man eine Liste von Frames, die in Python zum "Nachgehen" der Funktionsaufrufe dient. Ein Frame wird hierbei bei jedem Funktionsaufruf erstellt und gelöscht, wenn dieser returned wird.<br>
Der Stack ändert sich also während des Programmausführens, je nach Funktionsaufrufen und - returns.<br>

# Woche 8: <br>
Wir haben die Application GUI_Tabs erstellt und mit QTabWidget 5 Tabs hinzugefügt.<br>
In den dritten Tab haben wir unser mzTabTableWidget geladen, in den vierten Tab haben wir den FastaViewer von Team 1 laden können.<br>
![TabsLaura](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/TabsLaura.png)<br>
Wir waren uns nicht sicher, wo die Dateien Ini-Config und Experimental Design gespeichert sind. Daher sind Tab1 und Tab2 noch leer. <br>
In den 5.Tab haben wir das SpectrumWidget geladen (wir waren uns nicht sicher, ob mit 'Spectrum Viewer' der SpecViewer oder das SpectrumWidget gemeint ist.).<br>
Der Output unserer Application:<br>
![OutputTabs](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/OutputTabs.png)

# Woche 9:
Es wurde ein Button zum manuellen einladen eines files erstellt. <br>
![loadButton](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/loadButton.PNG)<br>
Hierzu wird über einen boolean gecheckt ob bereits ein file gealden ist, falls das der Fall ist müssen die Tabellen und Listen die dahinter stecken erst gecleared werden.<br>
![fileAlreadyLoaded](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/fileAlreadyLoaded.PNG)<br>
Danach (oder falls noch kein file geladen ist), werden die Tabllen befüllt und eingeblendet (einfache Auslagerung der Funktionen aus der init in die neue loadFile Funktion).<br>
![loadFile](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/loadFile.PNG)<br>

Es wurden außerdem die Spaltenbreiten der PRT-/PSM-Tabellen in der mzTabTableWidget automatisch angepasst mit resizeToContents(), sodass nun der vollständige Spalteninhalt angezeigt wird.<br>
![mzTabColumnsLaura](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/mzTabColumnsLaura.png)<br>

Das Hinzufügen des SpecViewers in Tab5 hat nun auch funktioniert. Der ursprüngliche Fehler lag in dem Aufruf der Main Klasse des SpecViewers, die denselben Namen wie eine andere Klasse hatte (App).<br>
![SpecViewerLaura](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/SpecViewerTabsLaura.png)<br>

# Woche 10:
OpenMS wurde installiert.<br>
Der XML-Viewer und das Experimental Design von Team 2 wurden der GUI_Tabs hinzugefügt, sodass nun jeder Tab ein Widget enthält.<br>
![GUITabsW10](https://raw.githubusercontent.com/Fabian1567/Teamprojekt-SS20-Laura-Yannik-Fabian/master/LauraW10.png)<br>
Es wurde außerdem ein Config-Button erstellt, der über den Tabs zu sehen ist.<br>






