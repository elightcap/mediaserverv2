# Docker Plex & Usenet Media Server #

docker-based plex & usenet media server using custom subdomains with tls

## Changes from V1
- Break each service into individual docker-compose files.  This might make initial start a bit worse, but makes changes and management more readable.
- Move from Plex to Jellyfin
- Change from traefik to caddyV2.  Caddy's config is just easier to work with to me, and being able to make dynamic changes is pretty neat
- Add ebooks through readarr
- Remove deluge because I dont torrent anymore

## Features
- [Jellyfin](https://hub.docker.com/r/linuxserver/jellyfin) is a Free Software Media System that puts you in control of managing and streaming your media. It is an alternative to the proprietary Emby and Plex, to provide media from a dedicated server to end-user devices via multiple apps.
- [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/) is a usenet downloader, written in C++ and designed with performance in mind to achieve maximum download speed by using very little system resources.
- [Sonarr](https://hub.docker.com/r/linuxserver/sonarr/) (formerly NZBdrone) is a PVR for usenet and bittorrent users. It can monitor multiple RSS feeds for new episodes of your favorite shows and will grab, sort and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available.
- [Radarr](https://hub.docker.com/r/linuxserver/radarr/) is a fork of Sonarr to work with movies à la Couchpotato.
- [Lidarr](https://hub.docker.com/r/linuxserver/lidarr/) is a music collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new tracks from your favorite artists and will grab, sort and rename them.
- [Readarr](https://hub.docker.com/r/linuxserver/readarr/) is a Book Manager and Automation (Sonarr for Ebooks)
- [Prowlarr](https://hub.docker.com/r/linuxserver/prowlarr/) is a indexer manager/proxy built on the popular arr .net/reactjs base stack to integrate with your various PVR apps.
- [tdarr](https://hub.docker.com/r/haveagitgat/tdarr) is a Audio/Video Library Analytics & Transcode/Remux Automation
- [NZBHydra](https://hub.docker.com/r/linuxserver/hydra2/) 2 is a meta search application for NZB indexers, the "spiritual successor" to NZBmegasearcH, and an evolution of the original application NZBHydra . It provides easy access to a number of raw and newznab based indexers.
- [rutorrent](https://hub.docker.com/r/linuxserver/rutorrent/) is a popular rtorrent client with a webui for ease of use.
- [Sabnzbd](https://hub.docker.com/r/linuxserver/sabnzbd) is a Usenet client.
- [Jellyseerr](https://hub.docker.com/r/fallenbagel/jellyseerr) is a free and open source fork of Overseerr for managing requests for your media library.
- [Caddy](https://hub.docker.com/_/caddy/) Caddy 2 is a powerful, enterprise-ready, open source web server with automatic HTTPS written in Go.
- [Watchtower](https://hub.docker.com/r/containrrr/watchtower) is a process for automating Docker container base image updates.
- [Deluge](https://hub.docker.com/r/linuxserver/deluge) is a lightweight, Free Software, cross-platform BitTorrent client.


## Requirements

- dedicated server or PC with plenty of storage
- windows or linux x86/x64 os (not ARM)
- personal top-level domain with configurable sub-domains (eg. plex.mydomain.com)

## ACME & DNS

The following subdomains should point to the public IP of your server:

- `jellyfin.mydomain.com`
- `sabnzbd.mydomain.com`
- `sonarr.mydomain.com`
- `radarr.mydomain.com`
- `hydra.mydomain.com`
- `ombi.mydomain.com`
- `readarr.mydomain.com`

Caddy, Sabnzbd, Tdarr, Prowlar, deluge, and rutorrent do not need entries because they run internally, and theres really no need to have them outside.  Watchtower theres nothing to serve

## Installation

1. install [docker](https://docs.docker.com/install/linux/docker-ce/debian/)

2. install [docker-compose](https://docs.docker.com/compose/install/#install-compose)

3. clone mediaserver repo
```bash
git clone https://github.com/elightcap/mediaserver.git
```

## Configuration

Copy `env.sample` to `.env`and `./caddy/sample/env` to `/caddy.env` and fill all required fields

```bash
cp env.sample .env && cp ./caddy/sample.env ./caddy/.env
```

## Deployment

Pull and deploy containers with docker-compose

```bash
docker-compose -f filename-compose.yml  up -d
```

You'll have to go through and up each compose file, and may need to create the docker network first


## Author

Evan Lightcap

## Acknowledgments

I didn't create any of these docker images myself, so credit goes to the
maintainers, and the original software creators. They are lined in the above Features section

## License

[MIT License](./LICENSE)
