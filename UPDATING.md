# Updating Guide

## Bundling new version of game files

1. Download latest Linux installer from [GOG](https://www.gog.com/en/account) on Windows
2. Place on WSL instance in ~/ and run: ```cd ~ && ./stardew_valley_1_6_4_24109_6654973489_72741.sh```
3. Move into game directory: ```cd ~/GOG\ Games/Stardew\ Valley/ && tar czf game.tar.gz .```
4. Place tarball into ```/docker_store/fileserver/stardew_valley/game/<version>/``` folder by copying from WSL to share in Windows

## Bundling new version of smapi files

1. Download latest SMAPI version from [Nexus](https://www.nexusmods.com/stardewvalley/mods/2400) on Windows
2. Rename the zip file to ```smapi.zip``` and place into ```/docker_store/fileserver/stardew_valley/smapi/<version>/``` folder

## Set permissions on fileserver

SSH into Docker Host 02 and set permissions: ```sudo chmod -R 0777 /docker_store/fileserver/stardew_valley```

## Update Dockerfile

1. Create a new branch based from ```local-build```
2. Commit a fix by modifying the URLs to point to the updated versions game/smapi files

## Backup instance and build new image

1. SSH into Docker Host 01 and cd into ```stardew-multiplayer-docker``` directory
2. Backup the current environment: ```tar czf ../stardew_backups/[version].tar.gz .```
3. Fetch origin changes: ```git fetch```
4. Checkout the branch with the version fix: ```git checkout fix/v1.6.4-4.0.7```
5. Build new image: ```docker-compose build --no-cache```

## Run updated container

```docker-compose up -d```
