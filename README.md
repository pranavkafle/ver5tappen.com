# 🏎️ Ver5tappen.com - F1 Championship Simulator

<div align="center">

![F1](https://img.shields.io/badge/F1-2025_Season-E10600?style=for-the-badge&logo=f1&logoColor=white)
![API](https://img.shields.io/badge/API-jolpica--f1-00D9FF?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-Automated-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)

**Interactive Formula 1 championship standings calculator with real-time API data**

[🐛 Report Bug](../../issues) | [✨ Request Feature](../../issues) | [🍴 Fork This Repo](../../fork)

</div>

---

## 📋 Overview

Ver5tappen.com is a lightweight, single-page F1 fantasy standings calculator that lets you explore "what if" scenarios for the Formula 1 World Drivers' Championship. Drag, drop, and experiment with race outcomes to see how the championship battle unfolds!

### ✨ Key Features

- 🔴 **Live API Integration** - Real-time data from [jolpica-f1 API](https://api.jolpi.ca/ergast/f1/)
- 🤖 **Automated Updates** - GitHub Actions fetches latest standings every 15 minutes during race weekends
- 🎯 **Interactive Drag & Drop** - Reorder drivers and mark DNFs to simulate race outcomes
- 📊 **Dynamic Standings** - Instant championship calculations as you make changes
- 🔗 **Shareable Links** - URL hash state lets you share scenarios with friends
- 🏁 **Past Race Protection** - Historical results are read-only and preserved
- 📱 **Fully Responsive** - Works perfectly on desktop, tablet, and mobile
- ⚡ **Zero Build Tools** - Pure HTML, Tailwind CSS, and vanilla JavaScript

---

## 🎮 Demo

### How to Use

1. **Select Key Drivers** - Choose your favorite drivers to highlight in the standings
2. **Drag & Drop** - Reorder drivers in upcoming race sessions
3. **Mark DNFs** - Drag drivers to the DNF zone to simulate retirements
4. **Toggle Past Races** - Show/hide completed races for a cleaner view
5. **Watch Standings Update** - See championship points recalculate in real-time
6. **Share Your Scenario** - Copy the URL to share your predictions

---

## 🚀 Getting Started

### Quick Start

**Option 1: Fork & Deploy**
1. Fork this repository
2. Enable GitHub Pages in Settings → Pages → Source: `main` branch, `/ (root)`
3. Your site will be live at `https://[your-username].github.io/ver5tappen.com/`
4. GitHub Actions will automatically update F1 data

**Option 2: Run Locally**

```bash
# Clone your fork
git clone https://github.com/[your-username]/ver5tappen.com.git
cd ver5tappen.com

# Open in browser (no build required!)
open index.html

# OR serve with a simple HTTP server
python3 -m http.server 8000
# Then visit http://localhost:8000/
```

No dependencies, no npm install, no webpack - just open and run! 🎉

---

## 📊 Data Sources

### API Integration

All race data is fetched from the **[jolpica-f1 API](https://api.jolpi.ca/ergast/f1/)** (successor to Ergast API):

- 📅 **Race Calendar** - All 2025 F1 races with dates, times, and circuit info
- 🏆 **Driver Standings** - Current championship points and positions
- 🏁 **Race Results** - Historical results for completed sessions
- 🎯 **Sprint Results** - Sprint race outcomes

### Automated Updates

GitHub Actions workflow runs on a smart schedule:
- ⏱️ **Every 15 minutes** during race weekends (Friday-Sunday)
- 📆 **Daily** on non-race days (Monday-Thursday)
- 🎯 **Race window detection**: Updates 1 hour before to 5 hours after each session

See [`.github/workflows/update-standings.yml`](.github/workflows/update-standings.yml) for details.

---

## 🎨 Features in Detail

### Interactive Race Simulation
- **Drag & Drop Interface** - Intuitive reordering of race results
- **DNF Management** - Drag drivers to/from DNF zone
- **Bulk Actions** - "Max P1 for all" applies to all future races
- **Reset to Defaults** - Quickly restore API data

### Smart Race Management
- **Future vs Past** - Only future races are editable
- **Visual Indicators** - Past races show badges and reduced opacity
- **Date-Aware Logic** - Uses precise UTC datetime from API
- **Historical Accuracy** - Past results locked to prevent accidental changes

### Championship Calculations
- **Real-Time Updates** - Instant standings recalculation
- **Accurate Points** - Uses official F1 point system
- **Tiebreakers** - Considers race wins, podiums, and best finishes
- **Key Driver Tracking** - Highlight your favorite drivers

### State Management
- **URL Hash State** - All preferences saved in URL
- **Shareable Links** - Send your scenarios to friends
- **Persistent Settings** - Show/hide past races preference saved
- **JSON Export** - Copy session data for external use

---

## 🛠️ Technical Stack

| Technology | Purpose |
|------------|---------|
| **HTML5** | Semantic structure |
| **Tailwind CSS** | Utility-first styling (CDN) |
| **Vanilla JavaScript** | No frameworks, pure ES6+ |
| **jolpica-f1 API** | Real-time F1 data |
| **GitHub Actions** | Automated data updates |
| **GitHub Pages** | Free hosting |

### Browser Support
- ✅ Chrome/Edge 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

---

## 📁 Project Structure

```
ver5tappen.com/
├── .github/
│   └── workflows/
│       └── update-standings.yml    # Automated data fetching
├── data/
│   ├── races-2025.json            # Full F1 calendar
│   ├── driver-standings-2025.json # Current standings
│   ├── race-results-2025.json     # Historical results
│   └── sprint-results-2025.json   # Sprint results
├── docs/
│   └── API.md                     # API documentation
├── public/
│   └── index.html                 # Application (legacy location)
├── index.html                     # Main application (root)
├── README.md
├── LICENSE
└── wrangler.jsonc                 # Cloudflare config (optional)
```

---

## 🔧 Configuration

### Updating Data Sources

Data files are automatically updated by GitHub Actions, but you can manually update them:

```bash
# Fetch latest race calendar
curl "https://api.jolpi.ca/ergast/f1/2025.json" > data/races-2025.json

# Fetch current standings
curl "https://api.jolpi.ca/ergast/f1/current/driverstandings.json" > data/driver-standings-2025.json

# Fetch race results
curl "https://api.jolpi.ca/ergast/f1/2025/results.json?limit=100" > data/race-results-2025.json

# Fetch sprint results
curl "https://api.jolpi.ca/ergast/f1/2025/sprint.json?limit=100" > data/sprint-results-2025.json
```

### Customizing the App

- **Team Colors**: Edit the `teamPalette` object in `index.html`
- **Point System**: Modify `SESSION_POINTS` array for different scoring
- **Default Drivers**: Auto-selected from top 3 in standings

### GitHub Actions Setup

After forking, GitHub Actions should work automatically. If not:
1. Go to your repo → Settings → Actions → General
2. Enable "Read and write permissions" for workflows
3. Manually trigger the workflow to test

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Reporting Issues
- 🐛 Found a bug? [Open an issue](../../issues)
- 💡 Have an idea? [Start a discussion](../../discussions)

### Pull Requests
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request to the original repository

#### PR Guidelines
- ✅ Clear description of changes and motivation
- ✅ Manual testing steps performed
- ✅ Screenshots/recordings for UI changes
- ✅ Keep changes focused and minimal

---

## 📝 API Documentation

See [docs/API.md](docs/API.md) for comprehensive API endpoint documentation.

### Quick Reference

```bash
# Race calendar
GET https://api.jolpi.ca/ergast/f1/2025.json

# Driver standings
GET https://api.jolpi.ca/ergast/f1/current/driverstandings.json

# Race results
GET https://api.jolpi.ca/ergast/f1/2025/results.json?limit=100

# Sprint results
GET https://api.jolpi.ca/ergast/f1/2025/sprint.json?limit=100
```

---

## 🎯 Roadmap

- [ ] Constructor's Championship simulation
- [ ] Multi-season support (2024, 2023, etc.)
- [ ] Historical comparison mode
- [ ] Mobile app (PWA)
- [ ] Dark mode toggle
- [ ] More advanced tiebreaker scenarios
- [ ] Export to PDF/image
- [ ] Custom point systems

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **[jolpica-f1 API](https://github.com/jolpica/jolpica-f1)** - For providing free, open-source F1 data
- **[Ergast API](http://ergast.com/mrd/)** - The original F1 data source
- **[Tailwind CSS](https://tailwindcss.com/)** - For the beautiful utility-first CSS
- **[lazharichir](https://github.com/lazharichir/ver5stappen.com)** - Original ver5stappen.com concept

---

## 🌟 Show Your Support

If you found this project useful:
- ⭐ Star this repository
- 🍴 Fork it and make it your own
- 🐦 Share it on social media
- 🤝 Contribute improvements

---

<div align="center">

**Made with ❤️ for F1 fans worldwide**

[Report Bug](../../issues) · [Request Feature](../../issues) · [Fork This Repo](../../fork)

</div>
