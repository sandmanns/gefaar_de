# GEFAAR (deutsche Version)
Ein Generisches Framework für die Analyse von Antimikrobieller Resistenz (aka Erreger- und Resistenzstatistik)

(es handelt sich um eine Erweiterung der Version von GEFAAR, die für das Universitätsklinikum Münster UKM, entwickelt wurde; eine englische Version ist unter sandmanns/gefaar verfügbar)


<p align="center">
    <img height="600" src="https://uni-muenster.sciebo.de/s/vyRZNwZRPDKKxdW/download">
</p>

Sandmann, S., Schaumburg, F. & Varghese, J. GEFAAR: a generic framework for the analysis of antimicrobial resistance providing statistics and cluster analyses. Sci Rep 13, 16922 (2023). https://doi.org/10.1038/s41598-023-44109-3


## Voraussetzungen
Um GEFAAR zu nutzen, benötigen Sie R (Version 4.1.0 oder höher) und R Shiny.

##  Installation
Um GEFAAR zu installieren, laden Sie einfach das Repository herunter. Alle erforderlichen Pakete werden installiert, alle Funktionen werden automatisch mit Hilfe des global.R-Skripts geladen.

## GEFAAR ausführen
GEFAAR ist als R Shiny GUI verfügbar. Um die Software auszuführen: 1) navigieren Sie zu dem Ordner, in dem die folgenden Dateien gespeichert sind: `global.R`, `ui.R`, `server.R`, `www/UKM.png` und `www/white.png. 2) Führen Sie Run App aus.

## Beispielhafte Nutzung von GEFAAR

## Input
m Analysen mit GEFAAR durchzuführen, muss der Input 1) eingelesen und 2) konfiguriert werden.

### Input einlesen

* `File einlesen` Wählen Sie eine tabellarische Datei zum Hochladen aus, die Informationen über antimikrobielle Resistenz enthält.
* `Trennzeichen Input File` Wählen Sie das Feldtrennzeichen aus, das in der Eingabedatei verwendet wird (eine von: Komma, Semikolon, Tabulator).

### Input konfigurieren

* `Wählen Sie die Spalte, die Informationen enthält zu...`
  * `...Spezies Name der Spalte, die Informationen über die analysierten Spezies enthält.
  * `...Klinik/Fachbereich` Name der Spalte, die Informationen über die Klinik/Fachbereich enthält.
  * `...Material` Name der Spalte, die Informationen über das Probenmaterial enthält, in dem die Spezies nachgewiesen wurden.
  * `...Datum` Name der Spalte, die Informationen über das Datum enthält, an dem die Proben entnommen wurden.
    * `-> Datumsformat` In der Eingabedatei verwendetes Datumsformat (eine von: tt.mm.jj, tt.mm.jjjj, mm/tt/jj, mm/tt/jjjj, jj-mm-tt, jjjj-mm-tt)
  * `...1. Isolat` Name der Spalte, die Informationen dazu enthält, ob es sich bei einer Probe um das 1. Isolat handelt (1) oder nicht (0).
  * `...erstes Antibiotikum` Name der Spalte, die Informationen über den ersten getesteten antimikrobiellen Wirkstoff enthält. Es wird angenommen, dass alle nachfolgenden Spalten Informationen über Antibiotika enthalten. Folgende Codierungen der Resistenzinformationen sind erforderlich: 'S' für susceptible, 'I' für susceptible increased exposure, 'R' für resistant, '-' für nicht analysiert (gemäß EUCAST).

      

### Beispiel

Wählen Sie die beispielhafte Input Datei 'Beispiel/Input/Exemplary_input_3years.txt' (für Daten über drei aufeinanderfolgende Jahre) und den Separator `Tab`. Führen Sie `Input einlesen` aus.

Wählen Sie die Spalte 'Species' für `...Spezies`, 'Clinic' für `...Klinik/Fachbereich`, 'Material' für `...Material`, 'Date' für `...Datum, 'yyyy-mm-dd' für `-> Datumsformat`, 'Isolate' für `...1. Isolat` und 'Amphotericin.B' für `...erstes Antibiotikum`. Führen Sie `Input konfigurieren` aus.

Alternativ wählen Sie `Demo Daten laden` (Daten über drei aufeinanderfolgende Jahre) und führen Sie `Input einlesen` aus.

Spalten mit Informationen zu Spezies, Klinik/Fachbereich, Material, Datum, Datumsformat, 1. Isolat und erstem Antibiotikum sind standardmäßig bereits korrekt definiert ('Species' für `...Spezies`, 'Clinic' für `...Klinik/Fachbereich`, 'Material' für `...Material`, 'Date' für `...Datum`, 'yyyy-mm-dd' für `-> Datumsformat`, 'Isolat' für `...1. Isolat` und 'Ampicillin' für `...erstes Antibiotikum`). Führen Sie `Input konfigurieren` aus.



## Erregerstatistik

Sobald eine Eingabedatei hochgeladen und konfiguriert wurde, kann die Erregerstatistik bestimmt werden.

### Details

* `Jahr`  Wählen Sie das Jahr, für das die Daten analysiert werden sollen (Standard: letztes verfügbares Jahr).
* `Material` Wählen Sie die Materialien aus, für die die Erregerstatistik bestimmt werden sollen.
* `Klinik/Fachbereich` Wählen Sie die Kliniken/Fachbereiche aus, für die die Erregerstatistik bestimmt werden sollen.
* `Cut-off min. 30 Fälle` Wählen Sie, ob ein Cut-off von mindestens 30 Fällen angewendet werden soll (wie im WHO GLASS Report) (Standard: ja).
* `Ausschließlich 1. Patienten-Isolat analysieren` Wählen Sie, ob ausschließlich das 1. Patienten-Isolat analysiert werden soll (Standard: nein).

Die Eingabeoptionen werden interaktiv aktualisiert, abhängig von der hochgeladenen Eingabedatei (z. B. können nur die Jahre ausgewählt werden, die in der zuvor definierten Datumsspalte verfügbar sind).

### Output

Eine interaktive Version der Erregerstatistik ist im rechten Bereich der Shiny-Oberfläche, Registerkarte `Erregerstatistik, verfügbar. Die Analyse kann als CSV-, Excel- oder PDF-Datei (=Drucken) exportiert werden.


### Beispiel

Wählen Sie: `Jahr` 2022, `Material` Alle, `Klinik/Fachbereich` Alle, `Cut-off min 30 Fälle` Ja, `Ausschließlich 1. Patienten-Isolat analysieren` Ja. Starten Sie die Analyse. Die interaktive Erregerstatistik wird generiert. Exportieren Sie die Ergebnisse als Excel-Datei. Die zu erwartende Ausgabedatei ist in 'Beispiel/Output/Erregerstatistik_2022-12-16.xlsx' verfügbar.


## Resistenzstatistiken

Sobald eine Input Datei hochgeladen und konfiguriert wurde, kann die Resistenzstatistik bestimmt werden.

### Details

* `Jahr`  Wählen Sie das Jahr, für das die Daten analysiert werden sollen (Standard: letztes verfügbares Jahr).
* `Material` Wählen Sie die Materialien aus, für die die Resistenzstatistik bestimmt werden sollen.
* `Klinik/Fachbereich` Wählen Sie die Kliniken/Fachbereiche aus, für die die Resistenzstatistik bestimmt werden sollen.
* `Ausschließlich 1. Patienten-Isolat analysieren` Wählen Sie, ob ausschließlich das 1. Patienten-Isolat analysiert werden soll (Standard: nein).
* `Spezies` Wählen Sie die Spezies aus, für die Resistenzstatistik bestimmt werden soll.

Die Eingabeoptionen werden interaktiv aktualisiert, abhängig von der hochgeladenen Eingabedatei (z. B. können nur die Jahre ausgewählt werden, die in der zuvor definierten Datumsspalte verfügbar sind).


### Output

Die Resistenzstatistik besteht aus dem `Datenblatt Antibiotika` und den `Grafiken Antibiotika`. Eine interaktive Version ist im rechten Bereich der Shiny-Oberfläche, Registerkarte `Resistenzstatistik`, verfügbar. Die Analyse kann als xlsx-Datei durch Ausführen von xlsx-Export exportiert werden.


### Beispiel

Wählen Sie: `Jahr` 2022, `Material` Alle, `Klinik/Fachbereich` Alle, `Ausschließlich 1. Patienten-Isolat analysieren` Ja, `Spezies` Alle. Starten Sie die Analyse. Die interaktive Resistenzstatistik wird generiert. Führen Sie `xlsx-Export` aus, um die Ergebnisse als Excel-Datei zu exportieren. Die zu erwartende Ausgabedatei ist in 'Beipsiel/Output/Resistenzstatistik_2024_12-16.xlsx' verfügbar.



## Trend-Analyse

Sobald eine Input Datei hochgeladen und konfiguriert wurde, kann eine Trend-Analyse durchgeführt werden.


### Details

* `Material` Wählen Sie die Materialien aus, für die die Trendanalyse bestimmt werden sollen.
* `Klinik/Fachbereich` Wählen Sie die Kliniken/Fachbereiche aus, für die die Trendanalyse bestimmt werden sollen.
* `Ausschließlich 1. Patienten-Isolat analysieren` Wählen Sie, ob ausschließlich das 1. Patienten-Isolat analysiert werden soll (Standard: nein).
* `Spezies` Wählen Sie die Spezies aus, für die Trendanalyse bestimmt werden soll.
* `Antibiotikum` Wählen Sie die Antibiotika aus, für die die Trendanalyse durchgeführt werden soll.

Die Eingabeoptionen werden interaktiv aktualisiert, abhängig von der hochgeladenen Eingabedatei (z. B. können nur die Materialien ausgewählt werden, die in der zuvor definierten Materialspalte verfügbar sind).


### Output

Eine interaktive Version der Trendanalyse ist im rechten Bereich der Shiny-Oberfläche, Registerkarte `Trend-Analyse`, verfügbar. Die Analyse kann als xlsx-Datei durch Ausführen von `xlsx-Export` exportiert werden.


### Beispiel

Wählen Sie: `Material` Alle, `Klinik/Fachbereich` Klinik 02, `Ausschließlich 1. Patienten-Isolat analysieren` Nein, `Spezies` Escherichia coli, `Antibiotikum` Alle. Starten Sie die Analyse. Die interaktive Trendanalyse wird durchgeführt. Führen Sie `xlsx-Export` aus, um die Ergebnisse als Excel-Datei zu exportieren. Die zu erwartende Ausgabedatei ist in 'Beispiel/Output/Trend_2024-12-16.xlsx' verfügbar.


## Cluster-Analyse

Sobald eine Input Datei hochgeladen und konfiguriert wurde, kann die Cluster-Analyse durchgeführt werden. Es stehen zwei Versionen zur Verfügung: `Interaktiv` und `Export`.


### Details

* `Dateiname des PDF-Exports` Wählen Sie die standardmäßige Benennung (GEFAAR_Resistance-Cluster-Analyse_<Datum>) oder definieren Sie einen individuellen Namen (default: Standard; nur EXPORT).
* `Jahr` Wählen Sie das Jahr, für das die Daten analysiert werden sollen (Standard: letztes verfügbares Jahr).
* `Material` Wählen Sie alle oder ein spezifisches Material aus, für das die Clusteranalysen durchgeführt werden sollen (Standard: alle).
* `Ausschließlich 1. Patienten-Isolat analysieren` Wählen Sie, ob ausschließlich das 1. Patienten-Isolat analysiert werden soll (Standard: nein).
* `Analyse wird unabhängig durchgeführt` Wählen Sie, ob eine Analyse 'pro Spezies' oder 'pro Klinik/Fachbereich' durchgeführt werden soll (Standard: pro Spezies; Optionsfelder für INTERAKTIV, Check Boxes für EXPORT).


#### Pro Spezies
* `Alle Spezies analysieren? (min. 30 Fälle)` Wählen Sie, ob alle oder eine ausgewählte Gruppe von Spezies analysiert werden soll. Wenn 'Nein' gewählt wird, werden alle verfügbaren Spezies automatisch angezeigt und eine individuelle Auswahl kann getroffen werden (Standard: ja).

* `Darstellung Heatmap` Wählen Sie durchzuführende Analysen anhand von Heatmaps aus.
  * Daten geordnet nach 1) Klinik/Fachbereich, 2) Resistenz
  * Daten geordnet nach 1) Klinik/Fachbereich, 2) Datum
  * Hierarchische Clusteranalyse
* `Darstellung UMAP` Wählen Sie durchzuführende Analysen anhand von UMAP aus.
  * Diagramm mit farbigen Kliniken/Fachbereichen
  * Diagramm mit farbigen Clustern
     * Zusätzliche Heatmap: Daten nach UMAP-Clustern angeordnet
     * Zusätzliche Heatmap: Daten nach Kliniken/Fachbereichen angeordnet

    
#### Pro Klinik/Fachbereich
* `Alle Kliniken/Fachbereiche analysieren? (min. 30 Fälle)` Wählen Sie, ob alle oder eine ausgewählte Gruppe von Kliniken/Fachbereichen analysiert werden soll. Wenn 'Nein' gewählt wird, werden alle verfügbaren Kliniken/Fachbereiche automatisch angezeigt und eine individuelle Auswahl kann getroffen werden (Standard: ja).

* `Darstellung Heatmap` Wählen Sie durchzuführende Analysen anhand von Heatmaps aus.
  * Daten geordnet nach Spezies
  * Hierarchische Clusteranalyse

Die Eingabeoptionen werden interaktiv aktualisiert, abhängig von der hochgeladenen Eingabedatei (z. B. können nur die Jahre ausgewählt werden, die in der zuvor definierten Datumsspalte verfügbar sind).


### Output

Eine interaktive Version der Cluster-Analysen ist im rechten Bereich der Shiny-Oberfläche, Registerkarte `Cluster-Analysen`, verfügbar. Die Analyse kann als PDF-Datei exportiert werden, indem zur Exportversion der Cluster-Analysen gewechselt wird.


### Beispiel

Wählen Sie die Version `Export`. Behalten Sie die Standardparameter bei (`Dateiname` Standard, `Jahr` 2021, `Material` Alle, `Ausschließlich 1. Patienten-Isolat analysieren` Nein). Wählen Sie 'pro Spezies' und 'pro Klinik/Fachbereich' und haken Sie alle möglichen Analyseoptionen an. Führen Sie Download aus. Ein PDF-Bericht, der alle Resistenzclusteranalysen enthält, wird automatisch generiert. Die zu erwartende Ausgabedatei ist in 'Beispiel/Output/Cluster-Analyse_2024-12-16.pdf' verfügbar.

Alternativ wählen Sie die Version `Interaktiv`. Behalten Sie die Standardparameter bei. Wählen Sie entweder 'pro Spezies' oder 'pro Klinik/Fachbereich' und haken Sie alle möglichen Analyseoptionen an. Starten Sie die Analyse.



## Fehler melden / Features anfordern

Sollten Sie Fehler bei der Nutzung von GEFAAR feststellen oder sich usätzliche Funktionen wünschen, zögern Sie nicht, ein Issue zu öffnen oder Sarah Sandmann (sarah.sandmann@uni-muenster.de) zu kontaktieren.

