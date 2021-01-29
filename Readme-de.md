# Motivation

Für unser Open-Source Führungsinformationssystem ODIN soll Kartenmaterial auch offline zur Verfügung stehen. Diese Anforderung erscheint nur logisch wenn man bedenkt, dass sowohl zivile wie auch militärische Einsatzkräfte in hohem Ausmaß unabhängig von vorhandener bzw. funktionierender Infrastruktur operieren müssen. Offline Fähigkeit bedeutet in diesem Zusammenhang, dass der Einsatz ohne eine Verbindung zum Internet durchgeführt werden kann.

# Methode

Unser Ansatz ist grundsätzlich "user first". D.h., die Anwendung so zu gestalten, dass selbst ungeübte Personen rasch Erfolge erzielen und die Bedienung der Anwendung dem eigentlichen Ziel nicht "im Weg" ist.

Das soll auch bei diesem Tutorial im Vordergrund stahen, wiewohl die gewählte Methode für das Bereistellen des Kartenmaterials zwar einfach ist, aber gerade für nicht versierte Benutzer auf den ersten Blick abschreckend erscheint.

# Kartenmaterial
Unser FüIS ODIN kann Kartenmaterial einbinden, das typischerweise von einem Kartenprovider bereitgestellt wird. Typische Vertreter von öffentlich zugänglichen Kartenprovidern sind z.B. OpenStreetMap oder basemap.at. Letztere werden wir beispielhaft in diesem Tutorial nutzen, da die notwendigen Daten von basemap.at bereits für den Download bereitgestellt werden.

Das Kartenmaterial wird in der Form von quadratischen Kacheln (Tiles) bereitgestellt, d.h. das sichtbare Kartenbild setzt sich aus einer Anzahl von Kacheln zusammen. Die Auswahl der Kacheln hängt von der Zoom-Stufe und vom Kartenausschnitt ab. Um nun die für den aktuell gewählten Kartenausschnitt notwendigen Kacheln zu laden, werden diese vom Kartenprovider angefordert. Die Addressierung der Kacheln erfolgt über das sogenannte x/y/z Schema, wobei die Variable {z}
 für die Zoomstufe und {x}{y} für die Koordinaten der Kachel in dieser Zoomstufe stehen. Werden die Karten über das Internet angeboten, dann konsumiert man die Kacheln beispielhaft über eine URL wie diese: https://{servername}/{kartenname}/{z}/{x}/{y}.png
 
Für die Nutzung von Kartenmaterial ohne Inernetzugang werden die Kacheln in einen Container gepackt. Das ermöglicht die Verteilung und Nutzung durch die Bereitstellung einer einzigen - zugegeben sehr großen - Datei.
 
## Container
Für dieses Tutorial verwenden wir die Offline Container von basemap.at:

* [basemap.at Standard Auflösung, Zoom 0..16 (19 GB!)](https://www.basemap.at/downloads/offline/bmap_standard_mbtiles_L00bisL16.zip)
und/oder
* [basemap.at Orthofoto, Zoom 0..16 (9 GB!)](https://www.basemap.at/downloads/offline/bmap_orthofoto_mbtiles_L00bisL16.zip)
 
 
## Offline Bereitstellung
Wie schon im Punkt Kartenmaterial beschrieben, wird das Kartenmaterial typischerweise über einen Server bereitgestellt und die Kartenkacheln über eine URL geladen. Das werden wir auch in diesem Totorial so machen. Wir stellen einen minimalen Karten-Server zur Verfügung, der vom [US Conservation Biology Institute
](https://github.com/consbio/mbtileserver) als frei verwendbare Open-Source Software bereitgestellt wird.

Dazu benötigen wir [den MBTiles Server]() und entpacken das Archiv (ZIP) an einen beliebigen Ort im Dateisystem. Das Resultat sieht so aus:

```
├── mbtileserver-osx
├── mbtileserver-windows.exe
├── tilesets
     ├── Readme.txt
```

Nun laden wir einen (oder beide) der oben angeführten Container von basemap.at und entpacken die darin enthaltene(n) ```mbtiles``` Dateien in den Ordner ```tilesets```. Wir haben das hier mit dem "Standard" Tile Container gemacht. Möglicherweise kann der verwendete Name von unserem in diesem Beispiel abweichen, jedoch sollte darauf geachtet werden, dass der Dateiname __keine__ Leer- oder Sonderzeichen enthält:

```
├── mbtileserver-osx
├── mbtileserver-windows.exe
├── tilesets
     ├── Readme.txt
     ├── standard16.mbtiles

```


 
 
# Nutzung in ODIN
ODIN verwendet für den Zugriff auf die 
