# Bio_Ton

Interaktive Karte zur Visualisierung von Bio_O_Ton Habitat-Eignungsflächen auf OpenStreetMap.

## 🗺️ Karte ansehen

**[https://fkistner85.github.io/Bio_Ton/](https://fkistner85.github.io/Bio_Ton/)**

Die Karte zeigt 64.321 Habitat-Flächen als GeoJSON-Overlay auf OpenStreetMap. Die aktuelle Kartenansicht (Position und Zoom) wird im URL-Hash gespeichert und kann direkt als Link geteilt werden.

## 📦 Daten

- **GeoJSON**: `docs/bio_ton_data.geojson` — 64.321 Polygon-Features mit Habitat-ID und Flächenangabe
- **Tile URL**: `https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png`
- **GeoJSON URL**: `https://fkistner85.github.io/Bio_Ton/bio_ton_data.geojson`

## 🔗 Integration

Für die Integration der Daten in uMap, Leaflet oder andere Kartenanwendungen siehe die [Integrations-Seite](https://fkistner85.github.io/Bio_Ton/integration.html).

### Leaflet.js Beispiel

```javascript
var map = L.map('map', { preferCanvas: true }).setView([49.5, 7.5], 9);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
}).addTo(map);

fetch('https://fkistner85.github.io/Bio_Ton/bio_ton_data.geojson')
    .then(r => r.json())
    .then(data => {
        L.geoJSON(data, {
            style: { fillColor: '#2ecc71', fillOpacity: 0.4, color: '#27ae60', weight: 1 }
        }).addTo(map);
    });
```

## 📁 Struktur

```
Bio_Ton/
├── docs/
│   ├── index.html              # Karten-Viewer
│   ├── integration.html        # Integrations-Anleitung
│   ├── bio_ton_data.geojson    # Habitat-Daten (64.321 Features)
│   └── tiles/                  # Tile-Verzeichnis
└── README.md
```

## 📄 Lizenz

Bitte stellen Sie sicher, dass Ihre Tiles den Lizenzbedingungen der Quelldaten entsprechen. Bei OpenStreetMap-Daten: `© OpenStreetMap contributors`.