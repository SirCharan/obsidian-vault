---
title: OSINT Data Sources
date: 2026-04-07
tags:
  - stocky-terminal
  - osint
  - geopolitics
  - conflict
  - disaster
  - acled
  - nasa
status: published
category: data-sources
---

# OSINT Data Sources

Stocky Terminal's OSINT layer aggregates 8+ open-source intelligence data sources covering armed conflicts, natural disasters, internet outages, and transportation tracking. All data is visualized on the [[Map System]] with 27+ layers.

> [!info] Why OSINT in a Financial Terminal?
> Geopolitical events move markets. A chokepoint blockade affects crude oil prices. An earthquake near a semiconductor fab disrupts chip stocks. Internet outages signal instability. OSINT data provides early warning signals that traditional financial terminals miss.

## Data Source Details

### ACLED (Armed Conflict Location & Event Data)

| Field | Value |
|---|---|
| **URL** | acleddata.com |
| **Data** | Armed conflicts, protests, riots, violence against civilians |
| **Coverage** | Global, updated weekly |
| **Format** | CSV/JSON API |
| **Map Layer** | Red markers with severity-based sizing |
| **Market Impact** | Supply chain disruptions, commodity price spikes, regional instability |

Sample events tracked:
- Military operations (Ukraine-Russia, Israel-Palestine, Myanmar, Sudan)
- Protests (large-scale, market-moving)
- Strategic violence (targeting infrastructure, government facilities)

### USGS (United States Geological Survey)

| Field | Value |
|---|---|
| **URL** | earthquake.usgs.gov |
| **Data** | Earthquakes magnitude 5.0+ |
| **Coverage** | Global, real-time |
| **Format** | GeoJSON API |
| **Map Layer** | Concentric circles, size = magnitude |
| **Market Impact** | Insurance stocks, infrastructure companies, supply chain disruption |

> [!tip] Why M5+ Only?
> Earthquakes below M5.0 rarely have market impact. Filtering to M5+ reduces map clutter while ensuring all market-moving seismic events are displayed.

### NASA EONET (Earth Observatory Natural Event Tracker)

| Field | Value |
|---|---|
| **URL** | eonet.gsfc.nasa.gov |
| **Data** | Fires, storms, volcanoes, floods, icebergs |
| **Coverage** | Global, near-real-time |
| **Format** | GeoJSON API |
| **Map Layer** | Category-specific icons with animation |
| **Market Impact** | Agricultural commodities, shipping routes, insurance |

Event categories:
- **Wildfires** — Agricultural commodity impact (sugar, palm oil, wheat)
- **Tropical storms** — Shipping route disruption, energy infrastructure
- **Volcanoes** — Aviation disruption, regional supply chains
- **Floods** — Infrastructure damage, commodity supply

### NASA FIRMS (Fire Information for Resource Management System)

| Field | Value |
|---|---|
| **URL** | firms.modaps.eosdis.nasa.gov |
| **Data** | Satellite-detected active fires |
| **Coverage** | Global, updated every 3 hours |
| **Format** | CSV/JSON |
| **Map Layer** | Orange heat dots |
| **Market Impact** | Agricultural impact, air quality (India-specific during stubble burning season) |

### GDACS (Global Disaster Alerting Coordination System)

| Field | Value |
|---|---|
| **URL** | gdacs.org |
| **Data** | Disaster alerts (earthquakes, floods, cyclones, droughts) |
| **Coverage** | Global |
| **Format** | RSS/GeoJSON |
| **Map Layer** | Alert-level colored markers (Green/Orange/Red) |
| **Market Impact** | Humanitarian response, insurance, infrastructure |

Alert levels:
- **Green** — Low impact, monitoring
- **Orange** — Moderate impact, regional concern
- **Red** — High impact, potential market-moving event

### Cloudflare Radar (Internet Outages)

| Field | Value |
|---|---|
| **URL** | radar.cloudflare.com |
| **Data** | Internet traffic anomalies and outages by country |
| **Coverage** | Global |
| **Format** | API |
| **Map Layer** | Country-level shading (darker = more disruption) |
| **Market Impact** | Tech sector impact, government censorship signals, infrastructure instability |

> [!warning] Outage ≠ Censorship
> Internet outages can be caused by infrastructure failure, natural disasters, or government censorship. Stocky does not distinguish the cause — it displays the data and lets users interpret. However, patterns (e.g., outages coinciding with protests) are noted in AI analysis.

### OpenSky Network (Flight Tracking)

| Field | Value |
|---|---|
| **URL** | opensky-network.org |
| **Data** | Live aircraft positions (ADS-B) |
| **Coverage** | Global, real-time |
| **Format** | REST API |
| **Map Layer** | Aircraft icons with heading arrows |
| **Market Impact** | Aviation sector, military movements, VIP travel |

### Vessel Tracking (AIS)

| Field | Value |
|---|---|
| **URL** | Various AIS providers |
| **Data** | Ship positions, types, routes |
| **Coverage** | Global maritime |
| **Format** | API |
| **Map Layer** | Ship icons on major shipping routes |
| **Market Impact** | Crude oil shipping, chokepoint monitoring (Hormuz, Suez, Malacca) |

## Data Refresh Rates

| Source | Refresh | Latency |
|---|---|---|
| ACLED | Daily | ~24h |
| USGS | Real-time | Minutes |
| NASA EONET | 6-12 hours | Hours |
| NASA FIRMS | 3 hours | Hours |
| GDACS | Near-real-time | Hours |
| Cloudflare Radar | Hourly | Minutes |
| OpenSky | 10 seconds | Real-time |
| Vessel AIS | 1-5 minutes | Minutes |

## Related Notes

- [[Map System]]
- [[Country Dossier]]
- [[Signal Generation & Aggregation]]
- [[News & Intelligence Sources]]
- [[Data Pipeline Architecture]]
