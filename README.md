# Counter-Strike: Global Offensive Dedicated Practice Server
This is a collection of addons, maps, scripts, and configuration files used for my personal CSGO surf server. If you're looking for my CSS guide, [it can be found here](https://github.com/evelyndrake/css-surf-practice-server).

![](https://i.imgur.com/bpTn31a.png)

The server contains the following, already configured for your convenience:
- [SurfTimer](https://github.com/surftimer/SurfTimer) and [predefined zones](https://github.com/Sayt123/SurfZones)
- [Metamod and Sourcemod](https://www.sourcemod.net/)
- A variety of other SourceMod plugins, including
    - MomSurfFix
    - NoLobbyReservation (required to join CSGO servers after CS2)
    - Trails
    - Knife, glove, and weapon skin customization
    - Model selection
    - Night vision
    - Realbhop
- Some preinstalled maps
## Installation Guide
### Setting up the server
- This guide assumes you're hosting this from a Windows machine.
- On Steam, right click on Counter-Strike 2, go to Properties -> Betas and switch the Beta Participation dropdown to `csgo_legacy`.
- Download [SteamCMD](https://steamcdn-a.akamaihd.net/client/installer/steamcmd.zip).
- Note that the folder containing the SteamCMD executable will be the folder in which your server is stored. This will take ~20GB if I recall correctly.
- Run SteamCMD.
- In the command prompt, login anonymously: `login anonymous`.
- Install the CS:GO dedicated server: `app_update 740 validate`.
- Exit SteamCMD.
- Navigate to the folder containing your dedicated server, containing the folders: `bin`, `csgo`, and `platform`.
- From this repository, remove the `start.bat` file located inside `!PUT THIS NEXT TO CSGO FOLDER NOT IN IT` and place it next to the `csgo` directory in your dedicated server (the file will exist alongside the 3 folders I just mentioned).
- Copy the rest of the files from this repository and merge them with your dedicated server's, replacing files when prompted.
- [Download my premade surf map pack](https://drive.google.com/file/d/1e96J0UEXmt8D-dD4p3Af9d5tgRO9N75T/view?usp=sharing), and extract it into your server's `csgo/maps` folder
- For some reason, I've been experiencing issues unless you also copy the maps folder from the server's `csgo` folder into your own client-side `Counter-Strike Global Offensive/csgo` folder (In Steam, right click CSGO -> Manage -> Browse local files to access this folder). Setting up FastDL will probably fix this.
- In your dedicated server, navigate to `csgo/addons/sourcemod/configs` and open the file `admins_simple.ini`.
- Use [steamidfinder.com](https://www.steamidfinder.com/) to find your Steam ID, for example, mine is `STEAM_0:0:47800602`.
- Replace this Steam ID in the configuration file with your own.
- To adjust the server's configuration, modify files in `csgo/addons/sourcemod/configs` and `csgo/cfg`, as well as `start.bat` and `csgo/cfg/server.cfg`.
### Setting up the database
- This part was the most confusing for me, but you got this ♥
- Start by installing the Windows version of [MariaDB](https://mariadb.org/download/?t=mariadb).
- The installer should prompt you to create a database--call it `surftimer` and make the password for the `root` user `admin` (You can make it whatever you want, but then you'll have to change the password in `csgo/addons/sourcemod/configs`).
- Search for MariaDB in the Windows start menu and open `Command Prompt (MariaDB)`.
- Run `mysql -u root -p surftimer < "YOUR_SERVER_DIRECTORY/csgo/scripts/mysql-files/fresh_install.sql"`, and enter your password (`admin` by default) when prompted.
- Run the same command two more times, replacing `fresh_install.sql` with `ck_zones.sql` and `ck_maptier.sql`.
- Your database should now be set up!
### Starting the server
- Run `start.bat` to start your local server.
- Open your Counter Strike: Global Offensive client before starting the server, otherwise it will say you already have the game open.
- Run `gamemenucommand openserverbrowser` in your client's console and go to the Local Games tab, where your server will appear.
- Join and have fun! Consider binding keys to `"say !COMMAND"`, where `COMMAND` could be `ws`, `gloves`, `knives`, `models`, `maps`, `surftimer` (to configure the timer settings), and `trails`.
- I'd recommend binding mouse3 to `sm_restart`, allowing you to restart your run whenever you'd like.
- Have fun!
### Installing new maps
- To add your own maps, install them from the steam workshop.
- Go to your client's `csgo/maps/workshop` folder and search for `.bsp`, which should reveal a list of all the workshop maps you've downloaded.
- Copy these into your server's `csgo/maps` folder.
- Edit `csgo/mapcycle.txt`, adding the names of each map you've installed (without `.bsp` at the end).
- Restart your server if it's already running.
- Finally, use the chat command `!maps` to select a map.
- Also, keep in mind that not all of the maps will have zones, which might break `sm_restart`.