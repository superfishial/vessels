# Components

## Jellyfin

https://watch.super.fish

### Setting up Authentication



## Jellyseerr

https://request.watch.super.fish

## Doplarr



## Sonarr

https://sonarr.watch.super.fish

## Radarr

https://radarr.watch.super.fish

## Bazarr

https://bazarr.watch.super.fish

Enable Basic Authentication under Settings -> General and set a username and password
Go to Settings -> Sonarr and add the API key from Settings -> General in https://sonarr.watch.super.fish
Go to Settings -> Radarr and add the API key from Settings -> General in https://radarr.watch.super.fish
Go to Settings -> Providers and add your providers (i.e. OpenSubtitles, YIFY Subtitles, Gestdown)

## Jackett

## QBittorrent/Flood

Set the "Port used for incoming connections" to a random value and enable "Use UPnP / NAT-PMP port forwarding from my router" under the Connection tab. NOTE Not sure if this actually helps

Bazarr:

For sonarr and radarr qbittorrent, set save path to /downloads and incomplete to /downloads/temp

Exec into `kubectl exec -it sonarr-0 -- /bin/bash` both sonarr and radarr and run the following to create the media folders

```
mkdir /downloads/media
chmod a+rw /downloads/media
```

And set the `autoProcess.ini` files for transcoding

```bash
cat <<EOF >/usr/local/sma/config/autoProcess.ini
Put the contents of autoProcess.ini from the sonarr and radarr directories here
EOF
```

Go to the `Media Management` tab and add `/downloads/media` as a root folder

## Prefer H265

For Sonarr, create a release profile called "H265" and add "x265" "h265" "hevc" as preferred terms. Set the score to anything above 0

For Radarr, create a Custom Fromat called "H265" and add a condition using the preset under "Release Title" called "x265". Go to the Profiles tab and add the custom format with a score above 0 for all the profiles.

# Cheat sheet

Port forward for most of the services

```
Sonarr: kubectl port-forward service/sonarr 8989:80
Sonarr QBittorrent: kubectl port-forward service/sonarr-qbittorrent 8080:80
Radarr: kubectl port-forward service/radarr 7878:80
Radarr QBittorrent: kubectl port-forward service/radarr-qbittorrent 8080:80
Jackett: kubectl port-forward service/jackett 9117:80
```
