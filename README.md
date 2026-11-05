# Augsburg – Interaktive Tourismuskarte

Eine browserbasierte Karte für Augsburg, die mehrere Audio-Stadtführungen, Points of Interest und Routen auf einer einzigen Leaflet.js-Karte vereint.

**Live:** https://bamisi.github.io/Reiserei/augsburg_map.html

---

## Funktionen

- **8 togglebare Quellen** (Lauschtouren, Wasserdrache Stadt, EPOCI, Brecht-Weg, Fuggerei-Weg, Kostenlose Museen, Essen & Trinken, Google Pins) sowie Unterkunft und Parkplatz als dauerhaft sichtbare Ebenen
- **Custom SVG-Pins** pro Quelle (Kamera, Lautsprecher, Drachenkopf, Buch, Haus, Gabel, Säulengebäude)
- **Audio-Player** direkt im Popup: einzelne Tracks oder mehrteilige Playlist mit Vor/Zurück-Navigation und automatischem Weiterspringen
- **Fußgänger-Routen** zwischen den Stationen einer Tour (via OSRM)
- **App-Store-Links** im Popup für Quellen mit externer App (Lauschtouren, Brecht-Weg)
- **Solo-Toggle**: Klick auf eine Quelle in der Legende blendet alle anderen aus; weiterer Klick fügt hinzu

---

## Technischer Aufbau

| Bereich | Lösung |
|---|---|
| Karte | [Leaflet.js 1.9.4](https://leafletjs.com), OpenStreetMap-Tiles |
| Routing | [OSRM Fußgänger](https://routing.openstreetmap.de/routed-foot/) |
| Audio | HTML5 `<audio>`, MP3s auf GitHub Pages gehostet |
| Text-to-Speech | [TTSMaker](https://ttsmaker.com) (kostenlos, keine Registrierung) |
| Hosting | GitHub Pages |
| Abhängigkeiten | keine Build-Tools, kein Framework – eine einzige `.html`-Datei |

---

## Audio-Dateien

Alle Audio-Guides liegen unter `augsburg_audio/`:

```
augsburg_audio/
├── fuggerei/
│   ├── fuggerei1.1.mp3 … fuggerei1.3.mp3   (Station 1, 3 Teile)
│   ├── fuggerei.zwischen1-2.moritz.1.mp3 … .moritz.6.mp3
│   ├── fuggerei.zwischen1-2.barfussmp3.mp3
│   ├── fuggerei2.mp3 … fuggerei11.3.mp3
│   └── …
└── dom/
    ├── dom1.mp3 … dom8.mp3
    └── …
```

**Namenskonvention:** `<ort><station>.<teil>.mp3`  
Zwischenstopps: `<ort>.zwischen<von>-<bis>.<name>.<teil>.mp3`

---

## Lokale Entwicklung

```bash
cd ~
python3 -m http.server 8080
# Karte öffnen: http://localhost:8080/augsburg_map.html
```

---

## Stationen hinzufügen

Neue Stationen werden im `STATIONS`-Array in `augsburg_map.html` eingetragen:

```javascript
{ name: 'Name des Ortes',
  src: 'fuggerei',           // Quelle (muss in SOURCES definiert sein)
  lat: 48.3691,
  lng: 10.9044,
  order: 5,                  // Reihenfolge für Route (optional)
  audio: 'https://…/datei.mp3',   // oder Array für Playlist
  desc: 'Kurzbeschreibung.' }
```
