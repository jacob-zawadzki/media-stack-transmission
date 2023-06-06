# media-stack

A stack of self-hosted media managers and streamer along with VPN. 

## Requirements

- Docker version 23.0.5 and above
- Docker compose version v2.17.3 and above
- It may also work on some of lower versions, but its not tested.

## Install media stack

`stack-1` This stack contains Jellyfin, Radarr, Sonarr, Jackett and Transmission.


```
docker network create mynetwork

# Install Jellyfin, Radarr, Sonarr, Jackett and Transmission stack
docker compose --profile stack-1 up -d

# Install Plex, Radarr, Sonarr, Jackett and Transmission stack
docker-compose --profile stack-2 up -d
```

## Configure Transmission

```
docker exec -it transmission bash # Get inside transmission container

mkdir /downloads/movies /downloads/tvshows
chown 1000:1000 /downloads/movies /downloads/tvshows
```

## Add indexer to Jackett

- Open Jackett UI at http://localhost:9117
- Add indexer
- Search for torrent indexer (e.g. the pirates bay, YTS)
- Add selected

## Configure Radarr

- Open Radarr at http://localhost:7878
- Settings --> Media Management --> Check mark "Movies deleted from disk are automatically unmonitored in Radarr" under File management section --> Save
- Settings --> Indexers --> Add --> Torznab --> Follow steps from Jackett to add indexer
- Settings --> Download clients --> Transmission --> Add Host (transmission) and port (9091) --> Username and password if added --> Test --> Save **Note: If VPN is enabled, then transmission / qbittorrent is reachable on vpn's service name**
- Settings --> General --> Enable advance setting --> Select Authentication and add username and password

## Add a movie

- Movies --> Search for a movie --> Add Root folder (/downloads/movies) --> Quality profile --> Add movie
- Go to transmission (http://localhost:9091) and see if movie is getting downloaded.

## Configure Jellyfin

- Open Jellyfin at http://localhost:8096
- Configure as it asks for first time.
- Add media library folder and choose /data/movies/

## Configure Jackett

- Add admin password

