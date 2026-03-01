<h1 align='center'>
    <img 
        src='/assets/logo.png' 
        height='200' 
        width='200'
        alt='Logo' 
    />
    <br>
    Jelly Torrent Throttle
    <br>
</h1>

<div align='center'>
    <a href='https://github.com/jbakalarski/JellyTorrentThrottle'>
        <img src='https://img.shields.io/github/stars/jbakalarski/JellyTorrentThrottle?style=for-the-badge&color=%23cfb002'/>
    </a>
    <a href='https://hub.docker.com/r/jedrzejme/jelly-torrent-throttle'>
        <img src='https://img.shields.io/docker/pulls/jedrzejme/jelly-torrent-throttle?style=for-the-badge&label=DOCKER%20PULLS'/>
    </a>
    <a href='https://github.com/jbakalarski/JellyTorrentThrottle/tags'>
        <img src='https://img.shields.io/github/v/tag/jbakalarski/JellyTorrentThrottle?sort=date&style=for-the-badge&label=VERSION&color=%23db34eb'/>
    </a>
    <a href='https://github.com/jbakalarski/JellyTorrentThrottle/issues'>
        <img src='https://img.shields.io/github/issues/jbakalarski/JellyTorrentThrottle?style=for-the-badge&color=%23ff6f00'/>
    </a>
    <a href='https://github.com/jbakalarski/JellyTorrentThrottle/pulls'>
        <img src='https://img.shields.io/github/issues-pr/jbakalarski/JellyTorrentThrottle?style=for-the-badge'/>
    </a>
</div>

<br>

**❓ What is this?** Jelly Torrent Throttle is a lightweight Python webhook service that listens to [Jellyfin](https://github.com/jellyfin/jellyfin) playback events and temporarily throttles [qBittorrent](https://github.com/qbittorrent/qBittorrent) global speeds during playback (restoring them on pause/stop).

**❓ How to use it?**
* [**Using docker-compose**](#-using-docker-compose-to-run-jelly-torrent-throttle)
* [**Using Python**](#-using-python-to-run-jelly-torrent-throttle)

**❓ What did I use?**
* [Python](https://www.python.org/)
* [Docker](https://www.docker.com/)
* [Webhooks for Jellyfin](https://github.com/shemanaev/jellyfin-plugin-webhooks)
* [qBittorrent WebUI API](https://github.com/qbittorrent/qBittorrent/wiki/WebUI-API-(qBittorrent-5.0))
* [Coding](https://code.visualstudio.com/)
* [Git management](https://desktop.github.com/)

## ⚠️ Requirements
* [Jellyfin](https://github.com/jellyfin/jellyfin)
* [Webhooks for Jellyfin](https://github.com/shemanaev/jellyfin-plugin-webhooks)
* [qBittorent with WebUI 5.0+](https://github.com/qbittorrent/qBittorrent)
* [Python 3.13+](https://www.python.org/) or [Docker with docker-compose](https://www.docker.com/)

## 🐳 Using docker-compose to run Jelly Torrent Throttle
1) Install Webhooks for Jellyfin:
    * Add [this link](https://raw.githubusercontent.com/shemanaev/jellyfin-plugin-repo/master/manifest.json) to `Repositories` in Jellyfin settings
    * Restart your Jellyfin instance
    * Install plugin called `Webhooks`
    * Restart your Jellyfin instance
2) Copy `docker-compose.yml` file to directory of your choice
3) Edit it according to [environment variables](#%EF%B8%8F-environment-variables)
4) Run container - `docker-compose up -d`
5) Grab the `IP:PORT` of your container
6) Create new webhook in Webhooks for Jellyfin plugin:
    * URL: `http://IP:PORT`
    * Payload format: `Default`
    * Listen to events only for: `All users`
    * Events: `Play`, `Pause`, `Resume`, `Stop`

## 🐍 Using Python to run Jelly Torrent Throttle
1) Install Webhooks for Jellyfin:
    * Add [this link](https://raw.githubusercontent.com/shemanaev/jellyfin-plugin-repo/master/manifest.json) to `Repositories` in Jellyfin settings
    * Restart your Jellyfin instance
    * Install plugin called `Webhooks`
    * Restart your Jellyfin instance
2) Copy `JellyTorrentThrottle.py`, `.env.example` and `requirements.txt` to directory of your choice
3) Change name of `.env.example` to `.env` and edit it according to [environment variables](#%EF%B8%8F-environment-variables)
4) Install requirements - `python -m pip install -r requirements.txt`
5) Run script - `python JellyTorrentThrottle.py`
6) Grab the `IP:PORT`
7) Create new webhook in Webhooks for Jellyfin plugin:
    * URL: `http://IP:PORT`
    * Payload format: `Default`
    * Listen to events only for: `All users`
    * Events: `Play`, `Pause`, `Resume`, `Stop`

## 🛠️ Environment variables
* `WEBHOOK_HOST` - IP address or hostname to bind the webhook listener to (default: `0.0.0.0`)
* `WEBHOOK_PORT` - Port for the webhook listener (default: `18080`)

* `QBITTORRENT_URL` - Base URL of qBittorrent WebUI (e.g. `http://localhost:8080`)
* `QBITTORRENT_USERNAME` - qBittorrent WebUI username
* `QBITTORRENT_PASSWORD` - qBittorrent WebUI password

* `SPEED_MODE` - Throttle mode: `alternative` (use qBittorrent alt-speed limits) or `custom` (use the custom limits below)
* `THROTTLE_DOWNLOAD_LIMIT` - Download limit to apply when throttling (KiB/s, only used with `SPEED_MODE=custom`)
* `THROTTLE_UPLOAD_LIMIT` - Upload limit to apply when throttling (KiB/s, only used with `SPEED_MODE=custom`)

* `LOG_LEVEL` - Logging level (`DEBUG`, `INFO`, `WARNING`, `ERROR`, default: `INFO`)
* `LOG_FILE` - Optional path to a rotating log file (if set, logs will also be written to this file)

## 🚀 Features
* 🎛️ Listens to Jellyfin playback webhooks (Play / Resume / Pause / Stop)
* 🐢 Temporarily throttles qBittorrent global speeds during playback and restores them on pause/stop
* ⚙️ Supports `alternative` (qBittorrent alt-speed) and `custom` throttle modes
* 👥 Safely handles multiple simultaneous playback sessions
* 🌐 Configurable via a `.env` file or via `docker-compose.yml` (qBittorrent credentials, throttle limits, host/port)
* 🩺 Exposes a `/health` endpoint and provides clean console logging
* 🐳 Runnable via Docker Compose or directly with Python
* 🔐 Uses qBittorrent WebUI authentication for API actions; no database required
  
## 💲 Support
<p><a href="https://support.jedrzej.me/" target="_blank"> <img align="left" src="https://raw.githubusercontent.com/jbakalarski/jbakalarski/main/assets/supportme.png" width="172" height="56" alt="jbakalarski" /></a></p>