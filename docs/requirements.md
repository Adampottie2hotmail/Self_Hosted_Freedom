# Requirements

## Hardware Requirements
1. RAM: 4gb (minimum but 8gb would be better)
    - Look at how many services you are going to run (up to 10 on 4gb). 
      - Unless running MC Server, then 8gb would be needed
    - If you can afford to upgrade an old laptop to 8gb RAM, then do it. You will be grateful in the future

2. Storage: 256gb SSD (boot), 500gb / 1TB HDD (storage)
    - Storage depends on your needs. If you are going to be running a Media Server (TV Shows, Movies, Music, etc) go for the 1TB. Otherwise 500gb will be good for now
3. CPU: No real requirements. Must be made after 2010
    - Can be any architecture (ARM (x32 / x64), AMD (x64), Intel (x64)


## Software Requirements
1. Windows
    - Windows 10 / 11
      - Lower versions will not work due to Docker Desktop requirements and Jellyfin / Plex requires newer .NET packages
      - Make sure to check if the OS is up to date (Settings -> Windows Updates -> Check for updates)
2. Linux
    - Ubuntu / Debian
      - Ubuntu 22.04 LTS or higher (LTS - Long Term Support. Using LTS releases are recommended as it reduces the amount of times you have to upgrade)
      - Update all repositories (apps, etc)
Terminal -> 'sudo apt update && sudo apt upgrade' -> Enter user password
