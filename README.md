# 🛰️ Satellite Intelligence Center

A futuristic, browser-based **Satellite Intelligence Center (S.I.C.)** designed as a high-tech global monitoring dashboard.

The interface combines an interactive satellite map, world-affairs intelligence feed, breaking-news ticker, UTC clock, system-status indicators, and live RSS-based news retrieval into a single immersive command-center style interface.

![Satellite Intelligence Center](https://img.shields.io/badge/Status-Operational-00f0d4?style=for-the-badge)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-199900?style=for-the-badge)

---

## 🌍 Overview

**Satellite Intelligence Center (S.I.C.)** is a front-end intelligence-style dashboard inspired by modern satellite operations and geopolitical monitoring interfaces.

The application provides:

- 🛰️ Interactive global satellite map
- 🌍 World affairs / intelligence feed
- 🔴 Breaking-news ticker
- 🕐 Live UTC clock and date
- 📡 System and satellite status indicators
- 📍 Real-time map coordinates
- 📰 RSS-based world news retrieval
- 🔄 Automatic news refresh
- 📱 Responsive interface for desktop, tablet, and mobile
- ⌨️ Keyboard shortcuts for quick controls
- ✨ Animated HUD-inspired visual interface

The application is designed to provide an immersive **command-center experience directly in the browser**.

---

## ✨ Features

### 🗺️ Interactive Satellite Map

The dashboard uses **Leaflet.js** to provide an interactive world map.

Features include:

- Global map view
- Satellite imagery
- Zoom controls
- Dynamic latitude/longitude display
- Animated targeting crosshair
- Radar-style scanning rings
- Responsive map resizing

Satellite imagery is provided through an Esri World Imagery tile layer.

---

### 🌐 World Affairs Feed

The right-side intelligence panel displays global news and geopolitical updates.

Each intelligence item contains:

- Headline
- Source
- Timestamp
- Severity classification

News items are categorized as:

- 🔴 **HIGH**
- 🟠 **MEDIUM**
- 🔵 **LOW**

High-priority events are automatically displayed first.

---

### 📰 Live News Integration

The application attempts to retrieve current world news through RSS feeds.

Currently configured sources include:

- BBC World News
- Al Jazeera

RSS data is retrieved through a proxy and parsed directly in the browser.

If live news cannot be retrieved, the system automatically falls back to a predefined intelligence dataset so that the dashboard remains operational.

---

### 🔴 Breaking News Ticker

A continuously scrolling breaking-news ticker appears at the bottom of the interface.

The ticker:

- Displays recent intelligence updates
- Shows severity indicators
- Displays timestamps
- Displays news sources
- Continuously scrolls horizontally
- Pauses when hovered

---

### 🕐 UTC Monitoring

The header contains a live UTC clock and date display.

The clock updates every second and provides a consistent global time reference.

---

### 📡 System Status

The interface includes operational status indicators such as:

```text
SYSTEM ONLINE
SATELLITE: 🔗 LOCKED
SIGNAL: 98%
```

The status indicator includes animated visual feedback to reinforce the monitoring-console aesthetic.

---

### ⌨️ Keyboard Controls

| Key | Action |
|-----|--------|
| `R` | Refresh intelligence/news feed |
| `F` | Reset map to global view |

---

## 🎨 Interface Design

The UI is designed around a futuristic **satellite command-center / intelligence operations** aesthetic.

### Design characteristics

- Dark tactical interface
- Cyan/teal HUD accents
- Glowing borders
- Animated radar rings
- Monospace intelligence typography
- Grid overlay
- Glassmorphism-inspired panels
- Real-time status indicators
- Responsive layout

### Fonts

The interface uses:

- **Orbitron** — display/interface headings
- **Share Tech Mono** — technical data
- **Inter** — general interface text

---

## 🧰 Technologies Used

### Frontend

- HTML5
- CSS3
- JavaScript (Vanilla JS)

### Mapping

- [Leaflet.js](https://leafletjs.com/)

### Map Data

- Esri World Imagery
- Carto map labels

### News

- RSS feeds
- Fetch API
- DOMParser
- AllOrigins proxy

### External Resources

The project loads Leaflet and Google Fonts through external CDNs.

---

## 📁 Project Structure

The current project can run as a lightweight single-page application:

```text
satellite-intelligence-center/
│
├── index.html
└── README.md
```

The main application contains the HTML structure, CSS styling, and JavaScript functionality in a single file.

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/satellite-intelligence-center.git
```

### 2. Enter the project directory

```bash
cd satellite-intelligence-center
```

### 3. Open the application

You can simply open:

```text
index.html
```

in a modern web browser.

For the best experience, however, run it through a local development server.

### Using VS Code Live Server

If you have the **Live Server** extension installed:

1. Open the project in VS Code.
2. Right-click `index.html`.
3. Select **Open with Live Server**.

---

## ⚠️ Important Notes

This project is a **front-end visualization and simulation dashboard**.

The satellite map does **not** represent a real military or intelligence satellite-control system.

The displayed system-status indicators are visual UI elements.

News severity levels are also application-level classifications and should not be interpreted as official intelligence assessments.

---

## 📡 News Feed & Fallback System

The application uses two layers of news data.

### Primary

Live RSS feeds are requested and parsed when available.

### Fallback

If the live feed fails, the application uses predefined fallback headlines.

This ensures that the interface does not remain empty when an external RSS service is unavailable.

---

## 🔄 Automatic Updates

The intelligence feed automatically attempts to refresh every:

```text
60 seconds
```

Users can also manually trigger a refresh using:

```text
R
```

---

## 📱 Responsive Design

The interface adapts to different screen sizes.

### Desktop

The dashboard uses a two-panel layout:

```text
┌─────────────────────────────────────────────────────┐
│                    S.I.C. HEADER                    │
├───────────────────────────────────┬─────────────────┤
│                                   │                 │
│          SATELLITE MAP            │ WORLD AFFAIRS   │
│                                   │                 │
│                                   │                 │
├───────────────────────────────────┴─────────────────┤
│                  BREAKING TICKER                    │
└─────────────────────────────────────────────────────┘
```

### Mobile

The map and intelligence feed stack vertically to provide a usable mobile layout.

---

## 🛠️ Future Improvements

Potential future development directions include:

- [ ] Real satellite tracking
- [ ] Satellite orbital visualization
- [ ] ISS tracking
- [ ] Multiple map layers
- [ ] Weather satellite data
- [ ] Earthquake monitoring
- [ ] Flight tracking
- [ ] Maritime vessel tracking
- [ ] Geopolitical event visualization
- [ ] News filtering by region
- [ ] News filtering by severity
- [ ] Search functionality
- [ ] Interactive intelligence markers
- [ ] Backend API
- [ ] Database integration
- [ ] User authentication
- [ ] Custom dashboard layouts
- [ ] WebSocket-based live updates
- [ ] Historical event timeline
- [ ] Dark/light interface modes

---

## 🔐 Disclaimer

This project is intended for **educational, experimental, and visualization purposes**.

It does not provide classified intelligence, military satellite control, or access to restricted satellite systems.

External map and news services are subject to their respective providers' availability, terms, and usage policies.

---

## 👨‍💻 Author

**Your Name**

Built as an experimental **geospatial intelligence dashboard / satellite monitoring interface** using modern browser technologies.

---

## ⭐ Support

If you find this project interesting, consider giving the repository a ⭐ on GitHub.

---

## 📄 License

Add your preferred open-source license to this repository.

For example:

```text
MIT License
```