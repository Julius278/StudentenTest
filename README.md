# Inhaltsverzeichnis
* [ Git ](#git)
* [ Project ](#project)
    * [ Getting Started ](#gettingstarted)
        * [ Vorbereitungen ](#vorbereitungen)
        * [ SSH Keys ](#ssh)
    * [ Hands on](#handson)
        * [ Git Repo erstellen ](#repo)
        * [ Vorhandene Daten hochladen ](#hochladen)
        * [ Projektmanipulation ](#manipulation)
            * [ Hinzufügen von Daten ](#hinzufuegen)
            * [ Abändern von Daten ](#aendern)
            * [ Löschen von Daten ](#loeschen)
        * [ Pull ](#pull)
        * [ Gitignore ](#gitignore)
        * [ Reset ](#reset)
* [ Git GUI ](#gitgui)
* [ Cheat Sheet ](#cheatsheet)
* [ Aufgaben ](#aufgaben)


<a name="git"></a>
# Git  
Git ist eine freie Software zur verteilten Versionsverwaltung von Dateien, die durch Linus Torvalds initiiert wurde.  


<a name="project"></a>
# Projekt
In diesem GitLab Projekt geht es um die grundlegenden Funktionsweisen von GitLab.  
Die Architektur und Funktionsweise im Hintergrund von Git ist uns erstmal egal und nicht Bestandteil, es geht nur um die Anwendung.


<a name="gettingstarted"></a>
## Getting Started

<a name="vorbereitungen"></a>
### Vorbereitungen
* Wir benötigen die [Git Software](https://git-scm.com/download/win), worin die Git GUI und Git Bash enthalten sind
* Ein Ordner mit Dateien, z.B. Programmcode

<a name="ssh"></a>
### SSH Key
Zur Authentifierung des Rechners bei GitLab benötigt einen Schlüssel

```
ssh-keygen -t ed25519 -C "email@example.com"
```

auf bzw. in Benutzer/.ssh/ liegt der öffentliche Schlüssel
dieser muss in Git eingetragen werden, um den Laptop zu authentifizieren
    Settings > SSH Keys > Key reinkopieren > Add Key

<a name="handson"></a>
## Hands On

<a name="repo"></a>
### Git Repo erstellen

Zunächst erstellen wir uns ein neues Projekt in unserer Git Umgebung.  
Hierbei können wir wählen, ob dies privat oder internal sein soll. Public ist (derzeit?) gesperrt durch die Konfiguration der Firma. 

![new Project](/img/newProject.PNG)

Angelegt wird ein leeres Projekt, welches wir nun nutzen können, um dort alles Mögliche zu testen.

<a name="hochladen"></a>
### Vorhandene Daten hochladen

Wir stellen uns zunächst vor, wir haben bereits einen Ordner mit Daten, die wir sichern möchten.  
Dieser Ordner kann nun aus verschiedensten Daten bestehen. Beispielsweise kann er Programmcode oder Dokumente enthalten, die mit mehreren Nutzern bearbeitet werden sollen.  

Hier die nötigen Zeilen zum initialen Upload der Daten mit Git Bash (Kommandozeile):

```
cd existing_folder
git init
git remote add origin git@git.altemista.cloud:Julius.Lauterbach/studententest.git
git add .
git commit -m "Initial commit"
git push -u origin master		
```

In Git ist nun der Projekt Ordner verfügbar, dies kann aussehen wie dieses Projekt (siehe oben). 
Die aktuell angezeigte Beschreibung steht in der README.md, welche automatisch als Beschreibung eines Projektes angenommen wir.

<a name="manipulation"></a>
### Projektmanipulation
In diesem Absatz geht es um die grundlegenden Möglichkeiten der Manipulation von verschiedenen  Daten innerhalb unseres Projektes.

<a name="hinzufuegen"></a>
#### Hinzufügen von Daten
Fügen wir eine neue Datei unserem Projektordner hinzu, muss diese i.d.R. auch dem Git-Projekt zur Verfügung stehen. 
In diesem Beispiel wird eine einfache Textdatei erstellt mit dem Namen "Hallo.txt", der Inhalt besteht aus "Hello World!". 
Mit  
```
git status		
```
könenn wir nun den aktuellen Status sehen, dort wird unsere neue Datei angezeigt.  
Anschließend möchten wir alle Dateien für den nächsten Commit hinzufügen.
```
git add .		
```
Wir können theoretisch noch mehr Dateien hinzufügen oder ändern und dem Commit hinzufügen.  
Anschließend wird der Commit getätigt, welcher eine neue "Version" des Projektes bestimmt.
Mit dem Push wird dies auch an Git übertragen.
```
git commit -m "Upload Kommentar"
git push
```
Die Schritte sind hier auch nochmal in der Kommandozeile zu sehen.  
![newTxt](/img/newTxt.PNG)

<a name="aendern"></a>
#### Abändern von Daten
Ändern wir nun die Datei ab, wird dies ebenfalls im Git Status angezeigt.  

![editTxt](/img/editTxt.PNG)  

In diesem Fall ist die Datei bekannt und sie wird nur als `modified` angezeigt. 
Da niemand sie sonst bearbeitet hat, können wir sie mit den o.g. Kommandos hochladen/updaten.

```
git add .
git commit -m "Upload Kommentar"
git push
```  

Die editierte Version der Datei ist nun sowohl lokal als auch in Git auf dem selben Stand.

<a name="loeschen"></a>
#### Löschen von Daten

Löschen wir eine Datei, weil wir sie nicht mehr benötigen, soll sie natürlich auch aus dem Git Repository verschwinden.  
Um dies zu erreichen, müssen wir diesen "delete" an Git weitergeben.  

Zunächst schauen wir nach, was die Kommandozeile zu der Löschung sagt:

![statusLoeschen](/img/statusLoeschen.PNG)  

Im Gegensatz zu Hinzufügen oder Ändern von Daten steht hier nur "deleted". Das lokale Repository merkt also, dass die Datei gelöscht wurde und in Git noch verfügbar ist.
Um diese nun auch im Git Repository zu löschen, nehmen wir die uns bereits bekannten Kommandozeilen Operationen.  

![loeschenPush](/img/loeschenPush.PNG)  

**ACHTUNG !!!**  
Wer nun aufmerksam den Screenshot durchgelesen hat, sieht hier, dass dort noch eine weitere Datei hinzugefügt wurde.  
Nutzt man ohne genauer hinzuschauen den Befehl `git add .`, dann werden alle Änderungen dem neuen Commit hinzugefügt.  
In diesem Fall habe ich den `git status` Screenshot direkt mit hochgeladen. Das ist im Normalfall nicht schlimm, man sollte jedoch genauer aufpassen.  

Wie im folgenden Beispiel zu sehen, man kann auch einzelne Dateien hinzufügen und somit dieses Problem umgehen.  

![gitAdd](/img/gitAdd.PNG)


<a name="pull"></a>
### Pull
Arbeitet man zusammen, kommt es immer wieder vor, dass man lokal nicht die selbe Version des Projekts besitzt wie im Git Repository. 
So kann einer der zuvor beschriebenen Fälle aufgekommen sein und beispielsweise hat jemand eine Datei bearbeitet, die lokal noch nicht bearbeitet ist.  

![behindMaster](/img/behindMaster.PNG)  

Mit einem Pull `git pull` können Änderungen des Projekts zur lokalen Bearbeitung eingeholt werden.  

![gitPull](/img/gitPull.PNG)  

Wie hier zu sehen ist, sind an der Datei README.md Änderungen vorgenommen worden, hierbei wurden einige Dinge ergänzt und etwas gelöscht oder geändert.
Genaue Änderungen lassen sich hier nur schwer einsehen. Möchte man dies genauer tun, kann man bsplw. die Git GUI verwenden. 
Einige Entwicklungsumgebungen bieten hier auch die Visualisierun von Changes an.

<a name="gitignore"></a>
### Gitignore
Gitignore ist eine Art der Textdatei mit der Dateiendung .gitignore, sie trägt keinen Dateinamen lediglich die Dateiendung.  
Erstellt kann sie werden, indem man eine leere Textdatei folgendermaßen speichert.  

![gitignoreSpeichern](/img/gitignoreSpeichern.PNG)  

neue Textdatei > speichern unter ".gitignore"  

Diese Datei wird trotz anderer Dateiendung als Textdokument gesehen und kann mit normalen Editoren bearbeitet werden. 
Fügt man beispielsweise "*.txt" ein, bewirkt man, dass alle Textdateien vom Upload bzw. Commit ausgeschlossen werden.  

Auch der Auschluss genauer Dateibezeichnungen ist möglich. 
Steht in der .gitignore-Datei lediglich `Hallo.txt`, wird nur die "Hallo.txt" ausgeschlossen, eine "Hello.txt" wird comitted.  

Ausschließbar sind auch ganze Ordner oder ein bestimmter Dateityp innerhalb eines Ordners.
Für genauere Beschreibungen verweise ich hier auf eine gute [Infoseite](https://www.atlassian.com/git/tutorials/saving-changes/gitignore).  

<a name="reset"></a>
### Reset


<a name="gitgui"></a>
# Git GUI
Die Git GUI visualisiert die Inhalte, die zuvor durch die Git Bash (Kommandozeile) durchgeführt wurden.  

Hiermit müssen die Kommandos nicht mehr eingetippt werden und können über die Oberfläche einfach und unkompliziert ausgewählt werden. 
Ein Beispiel der Dateiänderung und Ansicht der Änderungen sieht in der Git GUI folgendermaßen aus:  

![gitguiBeispiel](/img/gitguiBeispiel.PNG)  

Im Gegensatz zur Kommandozeile wird die Änderung hier sichtbar und kann eventuell noch widerrufen werden.  

Diese grafische Erweiterung bieten auch manche Entwicklungsumgebungen wie beispielsweise Visual Studio Code:
![vscgit](/img/vscgit.PNG)

<a name="cheatsheet"></a>
# Cheat Sheet
Wer noch weitere Befehle braucht oder einen schnellen Überblick über Befehle, 
kann diesen [Link](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf) nutzen.

<a name="aufgaben"></a>
# Aufgaben

1.  Erstelle ein neues Git Projekt
2.  Lade deinen Programmcode in das Repository
3.  Erstelle eine neue Textdatei, welche du aus deinem lokalen Repository in das Git Repository pushst
4.  Ändere eine oder mehrere Datei(en) ab, hierbei ist es egal, ob es sich um Programmcode oder die zuvor erstellte Aufgabe handelt. Comitte und pushe die Änderung.
5.  Lösche eine Datei aus deinem lokalen Repository. Nimm am besten hierzu die in Aufgabe 3 erstellte Textdatei, um Programmcode nicht zu zerstören.
6.  Erstelle eine .gitignore Datei und teste die Funktionalität mit mindestens 2 auszuschließenden Dateien oder Dateitypen.