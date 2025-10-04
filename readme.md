# SCUM Dedicated Server on Docker

This project allows you to easily run a dedicated SCUM game server using Docker.

## Quick Start

1.  **Get Files:**
    ```bash
    git clone https://github.com/jasonlcsdev/scum-server-docker.git
    cd scum-server-docker
    ```
2.  **Start Server:**
    ```bash
    docker compose up -d --build
    ```
    (The game will be downloaded and installed on first startup.)

3.  **To update the Server:**
    ```bash
    docker compose up -d --build --force-recreate
    ```
    (The game will be downloaded and updated on first startup.)

4.  **If the "downloading" process keeps looping:**
    It could be due to your permission settings, in which case you need to change the SCUM directory permission to UID:GID 1000:1000
    root@server:~/scum-server-docker# 
    ```bash
    chown -R 1000:1000 SCUM/
    ```
    (The game will be downloaded and updated on .)

5.  **Game Settings directory:**
    All .ini files are in the /scum-server-docker/SCUM/SCUM/Saved/Config/WindowsServer directory:
    | Filename               | Description                                 |
    | :--------------------- | :------------------------------------------ |
    | `AdminUsers.ini`       | SteamID64 number of the user, per line      |
    | `GameUserSettings.ini` | Universal Game Settings for your users      |
    | `ServerSettings.ini`   | [Main game settings for the server, see link](https://docs.google.com/spreadsheets/d/1w_JyXbtXcwhoYMrB_OAuLLJldR1Tu3Pq8GZGRjej0J8/edit?gid=612109557#gid=612109557) |

## Configuration

### Environment Variables

Set these in `compose.yml` under `environment`:

| Variable           | Description                      |
| :----------------- | :------------------------------- |
| `SCUM_PORT`        | Main server port (e.g., 7777).   |
| `SCUM_MAX_PLAYERS` | Max players (128 max).    |
| `SCUM_NO_BATTLEYE` | `"true"` to disable BattlEye.    |
| `STEAM_APP_ID`     | SCUM Steam App ID (3792580).     |

## Ports

Ensure these ports are open in your firewall and mapped in `docker-compose.yml`:

* `7777-7779/udp`, `7777/tcp`: Default SCUM Game Ports
* `27015-27016/udp`: Steam Query Ports

## Troubleshooting

* If the server won't start, check logs: `docker compose logs SCUM`.

## Resources

* For more detailed server setup information, refer to the [SCUM Dedicated server setup guide](https://scum.fandom.com/wiki/Scum_Dedicated_server_setup).
