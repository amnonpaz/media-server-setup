# Media Server Setup
This setup uses docker containers run by systemd services to automatically start up Jellyfin media server and transmission torrnet client with web interface.<br>
This is a setup for a RPi running Raspbian (Debian), but will work on any other platform.<br>
## Requirements
Required for this setup is docker and docker-compose. Also, the system must use systemd services manager (default in Ubuntu and Debian).
## Setting up
1. Change the name of the folder `user` under `home` to the real user name
2. Edit home/<user>/transmission/docker-compose.yml:
   Set `PUID` and `PGUID` to the real user and group IDs. Can be retreived by `uid -u` and `uid -g` respectively
   Set `USER` and `PASS`. These are the webl ogin credentials to your transmission server.
   Set the source folder for `/download` volume: Replace `/media/data` with your download destination
3. Edit home/<user>/jellyfin/docker-compose.yml:
   Set `PUID` and `PGUID`
   Set the source folder for `/media` volume
4. Edit the services file under `etc/systemd/system/`:
   Set the correct user folder
5. Copy the files to place:
   ```
   sudo cp -r etc/ /
   cp -r home/<user> /home/<user>/
   ```
6. Reload systemd daemon and enable services:
   ```
   sudo systemctl daemon-reload
   sudo systemctl enable transmission
   sudo systemctl enable jellyfin
   ```
7. Start services:
   ```
   sudo systemctl start transmission
   sudo systemctl start jellyfin
   ```
