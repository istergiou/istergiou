---
tags:
  - wiim
  - radio
  - m3u8
  - reference
aliases:
  - Radio Stream URLs
  - Global Radio Streams
---

# Internet Radio — Global Stream URL Directory

A curated directory of ==direct stream endpoints== for high-quality global internet radio, cross-referenced against multiple sources as of March 2025.

> [!warning] Stream URL stability
> Stream URLs can change without notice. BBC changed its infrastructure in January 2025. When a URL stops working, check the station's official site or the [[#Reference Directories]] at the bottom of this note.

> [!tip] SomaFM URL pattern
> All SomaFM streams follow a consistent pattern:
> `https://ice5.somafm.com/<channel>-<bitrate>-<format>`
> Substitute `ice3` for `ice5` as an alternate server.

> [!note] FLAC stream compatibility
> FLAC streams require a player that supports raw FLAC over HTTP: VLC, foobar2000, Roon, WiiM Ultra, Naim streamers. Most browser-based radio apps cannot decode FLAC.

---

## 1. High-Fidelity / Audiophile Streams

### Radio Paradise (USA — eclectic, ad-free, FLAC lossless)

| Mix | Format | Stream URL |
|-----|--------|-----------|
| Main Mix | FLAC ~1000 kbps / 44.1 kHz | `http://stream.radioparadise.com/flac` |
| Mellow Mix | FLAC ~1000 kbps / 44.1 kHz | `http://stream.radioparadise.com/mellow-flac` |
| Rock Mix | FLAC ~1000 kbps / 44.1 kHz | `http://stream.radioparadise.com/rock-flac` |
| Global/Eclectic Mix | FLAC ~1000 kbps / 44.1 kHz | `http://stream.radioparadise.com/eclectic-flac` |

Official stream links: https://radioparadise.com/listen/stream-links

### Mother Earth Radio (Germany — vinyl/hi-res source material, no ads)

| Channel | Format | Stream URL |
|---------|--------|-----------|
| Main | FLAC 24-bit / 192 kHz | `https://motherearth.streamserver24.com/listen/motherearth/motherearth` |
| Jazz | FLAC 24-bit / 192 kHz | `https://motherearth.streamserver24.com/listen/motherearth_jazz/motherearth.jazz` |
| Klassik | FLAC 24-bit / 192 kHz | `http://motherearth.streamserver24.com:18910/motherearth.klassik` |
| Instrumental | FLAC 24-bit / 192 kHz | `http://motherearth.streamserver24.com:18920/motherearth.instrumental` |

### Naim Radio (UK — FLAC)

| Channel | Format | Stream URL |
|---------|--------|-----------|
| Main | FLAC 16-bit / 44.1 kHz | `https://mscp3.live-streams.nl:8362/flac.flac` |
| Jazz | FLAC 16-bit / 44.1 kHz | `https://mscp3.live-streams.nl:8342/jazz-flac.flac` |
| Classical | FLAC 16-bit / 44.1 kHz | `http://mscp3.live-streams.nl:8250/class-flac.flac` |

### SuperStereo (Chile — FLAC 24-bit/96 kHz)

| Channel | Stream URL |
|---------|-----------|
| SuperStereo 1 | `http://icecast.centaury.cl:7570/SuperStereoHiRes1` |
| SuperStereo 2 | `http://icecast.centaury.cl:7570/SuperStereoHiRes2` |
| SuperStereo 3 | `http://icecast.centaury.cl:7570/SuperStereoHiRes3` |

---

## 2. Jazz Stations

| Station | Country | Format | Stream URL |
|---------|---------|--------|-----------|
| WBGO Jazz 88.3 FM | USA | MP3 128k | `https://ais-sa8.cdnstream1.com/3629_128.mp3` |
| Radio Swiss Jazz | Switzerland | AAC+ 96k | `https://stream.srg-ssr.ch/srgssr/rsj/aac/96` |
| Radio Swiss Jazz | Switzerland | MP3 128k | `https://stream.srg-ssr.ch/srgssr/rsj/mp3/128` |
| TSF Jazz 89.9 FM | France | MP3 128k | `http://broadcast.infomaniak.net/tsfjazz-high.mp3` |
| FIP Jazz | France | AAC HiFi ~192k | `https://icecast.radiofrance.fr/fipjazz-hifi.aac?id=radiofrance` |
| WWOZ 90.7 FM | USA (New Orleans) | MP3 hi | `http://wwoz-sc.streamguys.com/wwoz-hi.mp3` |
| SomaFM: Sonic Universe | USA | AAC 128k | `https://ice5.somafm.com/sonicuniverse-128-aac` |
| SomaFM: Bossa Beyond | USA | AAC 128k | `https://ice5.somafm.com/bossa-128-aac` |
| Naim Radio Jazz | UK | FLAC 16-bit | `https://mscp3.live-streams.nl:8342/jazz-flac.flac` |

---

## 3. Classical Music Stations

| Station | Country | Format | Stream URL |
|---------|---------|--------|-----------|
| Radio Swiss Classic | Switzerland | AAC+ 96k | `https://stream.srg-ssr.ch/srgssr/rsc_de/aac/96` |
| Radio Swiss Classic | Switzerland | MP3 128k | `https://stream.srg-ssr.ch/srgssr/rsc_de/mp3/128` |
| France Musique — Main | France | AAC HiFi ~192k | `https://icecast.radiofrance.fr/francemusique-hifi.aac?id=radiofrance` |
| France Musique — Baroque | France | AAC HiFi | `https://icecast.radiofrance.fr/francemusiquebaroque-hifi.aac?id=radiofrance` |
| France Musique — Classique Plus | France | AAC HiFi | `https://icecast.radiofrance.fr/francemusiqueclassiqueplus-hifi.aac?id=radiofrance` |
| WQXR 105.9 FM | USA (NYC) | MP3 128k | `https://stream.wqxr.org/wqxr` |
| WQXR — Operavore | USA | MP3 128k | `https://opera-stream.wqxr.org/operavore` |
| WQXR — New Sounds (Q2) | USA | MP3 128k | `https://q2stream.wqxr.org/q2` |
| BR-Klassik | Germany | MP3 high | `https://dispatcher.rndfnk.com/br/brklassik/live/mp3/high` |
| BBC Radio 3 | UK (intl) | AAC 320k HLS | `https://lsn.lv/bbcradio.m3u8?station=bbc_radio_three&bitrate=320000` |
| RNZ Concert | New Zealand | MP3 64k | `http://radionz-ice.streamguys.com/concert.mp3` |

---

## 4. Ambient / Electronic / Chill Stations

### SomaFM Ambient & Electronic

URL pattern: `https://ice5.somafm.com/<slug>-128-aac` (alternate server: `ice3`)

| Channel | Slug | Genre |
|---------|------|-------|
| Groove Salad | `groovesalad` | Ambient/downtempo |
| Drone Zone | `dronezone` | Atmospheric/space ambient |
| Deep Space One | `deepspaceone` | Space/IDM |
| Synphaera Radio | `synphaera` | New age/ambient |
| Lush | `lush` | Chill/ambient vocal |
| The Trip | `thetrip` | Psychedelic/trance |
| cliqhop idm | `cliqhop` | IDM/electronica |
| Beat Blender | `beatblender` | Deep house/lounge |
| Space Station Soma | `spacestation` | Electronic/ambient |

### Radio France Electronic (AAC HiFi ~192k)

| Station | Stream URL |
|---------|-----------|
| FIP Electro | `https://icecast.radiofrance.fr/fipelectro-hifi.aac?id=radiofrance` |
| FIP Groove | `https://icecast.radiofrance.fr/fipgroove-hifi.aac?id=radiofrance` |
| FIP Hip-Hop | `https://icecast.radiofrance.fr/fiphiphop-hifi.aac?id=radiofrance` |
| FIP Métal | `https://icecast.radiofrance.fr/fipmetal-hifi.aac?id=radiofrance` |

---

## 5. World Music / Eclectic Stations

| Station | Country | Genre | Format | Stream URL |
|---------|---------|-------|--------|-----------|
| FIP — Main | France | Eclectic/world (no ads) | AAC HiFi | `https://icecast.radiofrance.fr/fip-hifi.aac?id=radiofrance` |
| FIP Monde | France | World music | AAC HiFi | `https://icecast.radiofrance.fr/fipworld-hifi.aac?id=radiofrance` |
| FIP Reggae | France | Reggae | AAC HiFi | `https://icecast.radiofrance.fr/fipreggae-hifi.aac?id=radiofrance` |
| FIP Rock | France | Rock | AAC HiFi | `https://icecast.radiofrance.fr/fiprock-hifi.aac?id=radiofrance` |
| FIP Pop | France | Pop | AAC HiFi | `https://icecast.radiofrance.fr/fippop-hifi.aac?id=radiofrance` |
| FIP Nouveautés | France | New releases | AAC HiFi | `https://icecast.radiofrance.fr/fipnouveautes-hifi.aac?id=radiofrance` |
| Radio Paradise — Eclectic | USA | Eclectic/world | FLAC lossless | `http://stream.radioparadise.com/eclectic-flac` |
| Worldwide FM | UK | Underground global | MP3 | `http://worldwidefm.out.airtime.pro:8000/worldwidefm_a` |
| SomaFM: Suburbs of Goa | USA | Indian/world | AAC 128k | `https://ice5.somafm.com/suburbsofgoa-128-aac` |
| SomaFM: ThistleRadio | USA | Celtic/folk | AAC 128k | `https://ice5.somafm.com/thistle-128-aac` |

---

## 6. Public Broadcasters

### BBC (United Kingdom)

> [!warning] Geo-restriction & January 2025 URL changes
> The `lsn.lv` proxy URLs work internationally at ==320 kbps AAC==. Native `a.files.bbci.co.uk` HLS URLs are UK-only. Check [GarfNet's BBC HLS table](https://garfnet.org.uk/cms/tables/radio-frequencies/internet-radio-player/bbc-national-and-local-radio-hls-streams/) when URLs break.

| Station | Stream URL (international, 320k) |
|---------|----------------------------------|
| BBC Radio 1 | `https://lsn.lv/bbcradio.m3u8?station=bbc_radio_one&bitrate=320000` |
| BBC Radio 2 | `https://lsn.lv/bbcradio.m3u8?station=bbc_radio_two&bitrate=320000` |
| BBC Radio 3 | `https://lsn.lv/bbcradio.m3u8?station=bbc_radio_three&bitrate=320000` |
| BBC Radio 4 FM | `https://lsn.lv/bbcradio.m3u8?station=bbc_radio_fourfm&bitrate=320000` |
| BBC Radio 6 Music | `https://lsn.lv/bbcradio.m3u8?station=bbc_6music&bitrate=320000` |
| BBC World Service | `https://stream.live.vc.bbcmedia.co.uk/bbc_world_service` |

### Radio France (France)

| Station | Description | Stream URL |
|---------|-------------|-----------|
| France Inter | General/culture/news | `https://icecast.radiofrance.fr/franceinter-hifi.aac?id=radiofrance` |
| France Culture | Arts/philosophy | `https://icecast.radiofrance.fr/franceculture-hifi.aac?id=radiofrance` |
| France Musique | Classical/jazz | `https://icecast.radiofrance.fr/francemusique-hifi.aac?id=radiofrance` |
| FIP | Eclectic/ad-free | `https://icecast.radiofrance.fr/fip-hifi.aac?id=radiofrance` |

### Deutschlandradio (Germany)

| Station | Stream URL |
|---------|-----------|
| Deutschlandfunk (DLF) | `https://st01.sslstream.dlf.de/dlf/01/128/mp3/stream.mp3` |
| Deutschlandfunk Kultur | `https://st02.sslstream.dlf.de/dlf/02/128/mp3/stream.mp3` |
| BR-Klassik | `https://dispatcher.rndfnk.com/br/brklassik/live/mp3/high` |

### NPR / US Public Radio

| Station | Location | Stream URL |
|---------|----------|-----------|
| WNYC FM 93.9 | New York, NY | `https://fm939.wnyc.org/wnycfm` |
| WQXR 105.9 FM | New York, NY | `https://stream.wqxr.org/wqxr` |
| KEXP 90.3 FM | Seattle, WA | `https://kexp-mp3-128.streamguys1.com/kexp128.mp3` |
| WFMU | Jersey City, NJ | `http://stream0.wfmu.org/freeform-high.aac` |
| WWOZ 90.7 FM | New Orleans, LA | `http://wwoz-sc.streamguys.com/wwoz-hi.mp3` |
| WBGO Jazz 88.3 FM | Newark, NJ | `https://ais-sa8.cdnstream1.com/3629_128.mp3` |

### RNZ (Radio New Zealand)

| Station | Stream URL |
|---------|-----------|
| RNZ National | `http://radionz-ice.streamguys.com/national.mp3` |
| RNZ Concert | `http://radionz-ice.streamguys.com/concert.mp3` |

---

## 7. Indie / Alternative / Freeform

| Station | Country | Genre | Stream URL |
|---------|---------|-------|-----------|
| KEXP 90.3 FM | USA (Seattle) | Indie/alt/eclectic | `https://kexp-mp3-128.streamguys1.com/kexp128.mp3` |
| WFMU | USA | Freeform/experimental | `http://stream0.wfmu.org/freeform-high.aac` |
| BBC Radio 6 Music | UK | Alt/indie/eclectic | `https://lsn.lv/bbcradio.m3u8?station=bbc_6music&bitrate=320000` |
| Worldwide FM | UK | Underground global | `http://worldwidefm.out.airtime.pro:8000/worldwidefm_a` |
| SomaFM: Indie Pop Rocks! | USA | Indie pop | `https://ice5.somafm.com/indiepop-128-aac` |
| SomaFM: Secret Agent | USA | Spy jazz/cocktail | `https://ice5.somafm.com/secretagent-128-aac` |
| SomaFM: Underground 80s | USA | 80s alternative | `https://ice5.somafm.com/u80s-128-aac` |
| SomaFM: Seven Inch Soul | USA | Soul/funk/R&B | `https://ice5.somafm.com/7soul-128-aac` |

---

## FIP Radio — All Channels (AAC HiFi ~192k)

URL pattern: `https://icecast.radiofrance.fr/fip<variant>-hifi.aac?id=radiofrance`

| Channel | Stream URL |
|---------|-----------|
| FIP (main) | `https://icecast.radiofrance.fr/fip-hifi.aac?id=radiofrance` |
| FIP Rock | `https://icecast.radiofrance.fr/fiprock-hifi.aac?id=radiofrance` |
| FIP Jazz | `https://icecast.radiofrance.fr/fipjazz-hifi.aac?id=radiofrance` |
| FIP Groove | `https://icecast.radiofrance.fr/fipgroove-hifi.aac?id=radiofrance` |
| FIP Electro | `https://icecast.radiofrance.fr/fipelectro-hifi.aac?id=radiofrance` |
| FIP Hip-Hop | `https://icecast.radiofrance.fr/fiphiphop-hifi.aac?id=radiofrance` |
| FIP Reggae | `https://icecast.radiofrance.fr/fipreggae-hifi.aac?id=radiofrance` |
| FIP Métal | `https://icecast.radiofrance.fr/fipmetal-hifi.aac?id=radiofrance` |
| FIP Pop | `https://icecast.radiofrance.fr/fippop-hifi.aac?id=radiofrance` |
| FIP Monde | `https://icecast.radiofrance.fr/fipworld-hifi.aac?id=radiofrance` |
| FIP Nouveautés | `https://icecast.radiofrance.fr/fipnouveautes-hifi.aac?id=radiofrance` |
| FIP Sacrés Français | `https://icecast.radiofrance.fr/fipsacrefrancais-hifi.aac?id=radiofrance` |

---

## Reference Directories

- [SomaFM — Direct Stream Links](https://somafm.com/listen/)
- [Radio Paradise — Stream Links](https://radioparadise.com/listen/stream-links)
- [GarfNet — BBC HLS Streams (updated Jan 2025)](https://garfnet.org.uk/cms/tables/radio-frequencies/internet-radio-player/bbc-national-and-local-radio-hls-streams/)
- [Radio France icecast URLs — JV-conseil GitHub Gist](https://gist.github.com/JV-conseil/7063daeadf0041cb845d0ec22f8c418f)
- [Roon Internet Radio URL Swap Meet](https://community.roonlabs.com/t/internet-radio-url-swap-meet/8666)
- [HiRes Audio Online — Hi-Res Internet Radio](https://www.hiresaudio.online/hires-internet-radio/)
- [Radio Swiss Jazz — Internet Reception](https://www.radioswissjazz.ch/en/reception/internet)
- [Radio Swiss Classic — Internet Reception](https://www.radioswissclassic.ch/en/reception/internet)
- [KEXP Streaming URLs](https://www.kexp.org/streaming-urls/)
- [WNYC Other Formats](https://www.wnyc.org/audio/other-formats/)
- [radio-browser.info — Community URL Database](https://www.radio-browser.info/)
