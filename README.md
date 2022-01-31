# Docker Plex & Usenet Media Server #

docker-based plex & usenet media server using custom subdomains with tls

## Changes from V1
- Break each service into individual docker-compose files.  This might make initial start a bit worse, but makes changes and management more readable.
- Change from traefik to caddyV2.  Caddy's config is just easier to work with to me, and being able to make dynamic changes is pretty neat
- More Services: Tautulli(Plex dashboard), Readarr(ebooks), Ubooquity(OPDS), and Watchtower(autoupdate containers)
- Remove deluge because I dont torrent anymore

## Features
- [Plex](https://hub.docker.com/r/plexinc/pms-docker) organizes video, music and photos from personal media libraries and streams them to smart TVs, streaming boxes and mobile devices. This container is packaged as a standalone Plex Media Server.
- [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/) is a usenet downloader, written in C++ and designed with performance in mind to achieve maximum download speed by using very little system resources.
- [Sonarr](https://hub.docker.com/r/linuxserver/sonarr/) (formerly NZBdrone) is a PVR for usenet and bittorrent users. It can monitor multiple RSS feeds for new episodes of your favorite shows and will grab, sort and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available.
- [Radarr](https://hub.docker.com/r/linuxserver/radarr/) A fork of Sonarr to work with movies à la Couchpotato.
- [NZBHydra](https://hub.docker.com/r/linuxserver/hydra2/) 2 is a meta search application for NZB indexers, the "spiritual successor" to NZBmegasearcH, and an evolution of the original application NZBHydra . It provides easy access to a number of raw and newznab based indexers.
- [Caddy](https://hub.docker.com/_/caddy/) Caddy 2 is a powerful, enterprise-ready, open source web server with automatic HTTPS written in Go.
- [Ombi](https://hub.docker.com/r/linuxserver/ombi/) UI to allow users to request new shows/movies
- [Readarr](https://hub.docker.com/r/linuxserver/readarr) Book Manager and Automation (Sonarr for Ebooks)
- [Ubooquity](https://hub.docker.com/r/linuxserver/ubooquity) is a free, lightweight and easy-to-use home server for your comics and ebooks. Use it to access your files from anywhere, with a tablet, an e-reader, a phone or a computer.
- [Tautulli](https://hub.docker.com/r/tautulli/tautulli) is a 3rd party application that you can run alongside your Plex Media Server to monitor activity and track various statistics.
- [Watchtower](https://hub.docker.com/r/containrrr/watchtower) is A process for automating Docker container base image updates. 

## Requirements

- dedicated server or PC with plenty of storage
- windows or linux x86/x64 os (not ARM)
- personal top-level domain with configurable sub-domains (eg. plex.mydomain.com)

## ACME & DNS

The following subdomains should point to the public IP of your server:

- `plex.mydomain.com`
- `nzbget.mydomain.com`
- `sonarr.mydomain.com`
- `radarr.mydomain.com`
- `hydra.mydomain.com`
- `ombi.mydomain.com`
- `readarr.mydomain.com`
- `calibre.mydomain.com` (i know its ubooquity, but i had started with calibre and its easier to spell)

Tautulli and Caddy do not need entries because they run internally, and theres really no need to have them outside.  Watchtower theres nothing to serve

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
docker-compose pull
docker-compose -f filename-compose.yml  up -d
```

You'll have to go through and up each compose file, and may need to create the docker network first


## Author

Evan Lightcap

## Acknowledgments

I didn't create any of these docker images myself, so credit goes to the
maintainers, and the original software creators.

- [plex.tv](https://plex.tv/)
- [linuxserver.io](https://linuxserver.io/)
- [containrrr](https://containrrr.dev)
- [tautulli](https://tautulli.com)
- [Caddy](https://caddyserver.com/v2)

## License

[MIT License](./LICENSE)
