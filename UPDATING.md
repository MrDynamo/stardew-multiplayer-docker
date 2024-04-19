# Updating Guide

## Bundling new version of game files

1. Download latest Linux installer from GOG
2. Place on WSL instance in ~/ and run: ```cd ~ && ./stardew_valley_1_6_4_24109_6654973489_72741.sh```
3. Move into game directory: ```cd ~/GOG\ Games/Stardew\ Valley/ && tar czf 1.6.4.tar.gz .```

## Upload to fileserver site

1. Place tarball into \docker_store\fileserver\stardew_valley\game folder
2. SSH into Docker Host 01 and set permissions: ```chmod -R /docker_store/fileserver/stardew_valley```

## Update Dockerfile

1. Create a new branch based from ```local-build```
2. Commit a fix by modifying the URLs to point to the updated game/smapi files

## Build new docker image

1. SSH into Docker Host 02 and cd into stardew-multiplayer-docker directory
2. Checkout the branch with the version fix: ```git checkout fix/v1.6.4```
3. Build new image: ```docker-compose build --no-cache```

## Run updated container

1. ```docker-compose up -d```
