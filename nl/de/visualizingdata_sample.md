---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-20"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerätedaten visualisieren
{: #visualizingdata_data}

Dieses Beispiel hilft Ihnen dabei, Echtzeitdaten und archivierte Daten von registrierten Geräten in Ihrer {{site.data.keyword.iot_full}}-Organisation zu visualisieren.
{:shortdesc}

## Vorbereitende Schritte
{: #byb}

Bevor Sie Ihre Daten visualisieren können, müssen Sie folgende Aktionen ausführen:

- Registrieren Sie Ihre Geräte für Ihre {{site.data.keyword.iot_short_notm}}-Organisation.
- Stellen Sie sicher, dass Ihre Geräte Ereignisse an {{site.data.keyword.iot_short_notm}} senden.
- [Laden Sie das Visualisierungsbeispiel](https://github.com/ibm-watson-iot/rickshaw4iot/archive/master.zip) vom Github-Repository herunter und extrahieren Sie die ZIP-Datei.
- [Installieren Sie das Befehlszeilentool 'cf'](../../starters/install_cli.html) von {{site.data.keyword.Bluemix_notm}}.

## Beispiel in {{site.data.keyword.Bluemix_notm}} ausführen
{: #running_sample}

1. Erstellen Sie in {{site.data.keyword.Bluemix_notm}} eine Anwendung mithilfe des Node.js-SDK. Notieren Sie den Anwendungsnamen und den Hostnamen der Anwendung; diese Informationen sind erforderlich, um die Anwendung in {{site.data.keyword.Bluemix_notm}} hochzuladen.
2. Binden Sie die Node.js-Anwendung in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard an Ihre {{site.data.keyword.iot_short_notm}}-Instanz und führen Sie folgende Schritte aus:

  a. Klicken Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard auf die von Ihnen erstellte Node.js-Anwendung.

  b. Klicken Sie auf **Service oder API binden**, wählen Sie anschließend Ihren {{site.data.keyword.iot_short_notm}}-Service aus und klicken Sie auf **Hinzufügen**.
3. Wechseln Sie mithilfe des Befehlszeilentools 'cf' von Ihrem Verzeichnis zu dem extrahierten Paket mit dem Visualisierungsbeispiel und führen Sie folgenden Befehl aus, um eine Verbindung zu {{site.data.keyword.Bluemix_notm}} herzustellen.
```
cf api https://api.ng.bluemix.net
```
4. Melden Sie sich anschließend mithilfe der folgenden Angaben bei {{site.data.keyword.Bluemix_notm}} an:
```
cf login -u <Ihre_Anmelde-ID_für_Bluemix>
```
Wenn Sie nicht die Standardorganisation und den Standardbereich verwenden, können Sie Folgendes verwenden:
```
cf target -o <Ihre_Bluemix-Organisation> -s dev
```

5. Bearbeiten Sie die Datei `manifest.yml` und aktualisieren Sie den Hostnamen und den Anwendungsnamen mithilfe des folgenden Formats:
```
Anwendungen:
 - Plattenkapazität: 1024M
   Host: <Name_Ihres_Bluemix-Hosts>
   Name: <Name_Ihres_Bluemix-Hosts>
   Befehl: node ap.js
   Pfad:
   Domäne: mybluemix.net
   Instanzen: 1
   Speicher: 128M
```
6. Implementieren Sie Ihr Visualisierungsbeispiel mithilfe des folgenden Befehls:
```
cf push <Name_Ihrer_Anwendung>
```
7. Geben Sie folgende URL in Ihren Browser ein:
```
http://<Name_Ihrer_Anwendung>.mybluemix.net
```

Alle Geräte in Ihrer Organisation sind im Dropdown-Menü des Geräts aufgelistet. Ist ein Gerät ausgewählt, wird die Echtzeitvisualisierung der Daten angezeigt, die dieses Gerät an Ihren {{site.data.keyword.iot_short_notm}}-Service sendet. Zum Anzeigen von archivierten Daten klicken Sie auf die Schaltfläche für die Option für historische Daten.

## Beispiel anpassen
{: #customize_sample}

Die Beispielanwendung ist eine eigenständige Webanwendung, die im Node.js-Framework geschrieben wurde. Mit dem Beispiel werden Ereignisse visualisiert, die von registrierten Geräten in {{site.data.keyword.iot_short_notm}} gesendet wurden. Im Beispiel werden folgende Tools verwendet:

- Express: Node.js-Framework von Webanwendungen
- JQuery: Aufrufe der grafischen Benutzerschnittstelle und Ajax-Aufrufe
- Rickshaw: Tool für die grafische Visualisierung
- Paho: MQTT-Client

Die Beispielanwendung wird durch folgende Verzeichnisse strukturiert:

- Public
- CSS: Stylesheets
- Images
- JS: Hauptdateien für JavaScript-Logik
- Historian: Code für Visualisierung über Archivierungsfunktion
- Realtime: Code für Echtzeitvisualisierung
- Uicontroller.js: Code zum Steuern der Benutzerschnittstelle
- Routen: Weiterleitungslogik und Webanwendung
- Utils: Dienstprogrammfunktionen, die zum Ausführen von HTTP-Aufrufen verwendet werden
- Views: in Jade geschriebene Benutzerschnittstellendateien
- Die Rickshaw-Bibliothek für die Diagrammerstellung wird zum Darstellen des Diagramms für Echtzeit- und archivierte Daten verwendet.

## Anzeige von Echtzeitdaten anpassen
{: #customize_real_time_display}

Das Verzeichnis mit dem grafischen Visualisierungscode für Echtzeitdaten lautet `public/ja/realtime`. Die Logik für die grafische Darstellung kann durch Bearbeiten von `public/js/historian/realtimeGraph.js` angepasst werden.

Die Datei, die auf die Paho-MQTT-Bibliothek verweist, um Gerätetopics zu subskribieren und Geräteereignisse von {{site.data.keyword.iot_short_notm}} zu erhalten, finden Sie an der Position `public/js/historian/realtime.js`.

Geräteereignisse werden an die Datei `realtimeGraph.js` gesendet, um das Diagramm grafisch darzustellen.

Ein detallierteres Entwicklerhandbuch ist über das [Github-Wiki ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/rickshaw4iot/wiki){:new_window} verfügbar.
