# Plex Media Setup

https://trash-guides.info/

### Indexers

Prowler:  TPB, TheRARBG, YTS

Jackett: Unused, couldn’t uninstall

### Downloader

qbittorrent

### Sonarr

[http://192.168.2.54:8989/](http://192.168.2.54:8989/)

### Radarr

[http://192.168.2.54:7878/](http://192.168.2.54:7878/)

### Plex

[http://192.168.2.54:32400](http://192.168.2.54:32400/web/index.html#!/)

### Overseerr

[http://localhost:5055/](http://localhost:5055/)  (Only from media computer)

- Setup Docker Script
    
    ```jsx
    docker run -d `
      --name overseerr `
      -e TZ="America/Toronto" `
      -p 5055:5055 `
      -v C:\DockerData\Overseerr:/config `
      --restart unless-stopped `
      lscr.io/linuxserver/overseerr:latest
    ```
    
    ```jsx
    docker stop overseerr
    docker start overseerr
    ```
    
- Temporarily using dev build for watchlist sync
    
    ```jsx
    docker run -d `
      --name overseerr `
      -e TZ="America/Toronto" `
      -p 5055:5055 `
      -v C:\DockerData\Overseerr:/config `
      --restart unless-stopped `
      lscr.io/linuxserver/overseerr:develop
    ```