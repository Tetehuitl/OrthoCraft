---
title: Minecraft docker-compose
description: 
published: true
date: 2022-02-23T13:18:35.941Z
tags: 
editor: markdown
dateCreated: 2022-02-23T13:18:33.908Z
---

Typical docker setup:
```
version: "3"

services:
  mc:
    image: itzg/minecraft-server
    ports:
      - 25565:25565
      - 25516:25516/udp
    environment:
      TYPE: "PURPUR"
      SPIGET_RESOURCES: "8631,6245,28140,68271,87610"
      EULA: "TRUE"
      MEMORY: "1G"
      VERSION: "1.17.1"
      ENABLE_RCON: "true"
      RCON_PORT: "25575"
      RCON_PASSWORD: "minecraft"
      SERVER_PORT: "25565"
      ONLINE_MODE: "false"
      SERVER_NAME: "lobby"
      #ENABLE_ROLLING_LOGS: "true"
      MOTD: "Orthocraft lobby server."
      VIEW_DISTANCE: "15"
      SIMULATION_DISTANCE: "8"
      MAX_PLAYERS: "10"
      DIFFICULTY: "peaceful"
      GAMEMODE: "survival"
      FORCE_GAMEMODE: "false"
      SPAWN_ANIMALS: "false"
      SPAWN_MONSTERS: "false"
      SPAWN_NPCS: "false"
      #RESOURCE_PACK: "https://github.com/anaxios/MC-resource-pack/raw/main/Vanilla_Additions_2.1.zip=1"
      PVP: "false"
      #LEVEL_TYPE: "flat"
      BROADCAST_CONSOLE_TO_OPS: "true"
      ALLOW_FLIGHT: "true"
      LEVEL: "world"
      SPAWN_PROTECTION: "0"
      OPS: "SOPHRONIOS"
      OVERRIDE_SERVER_PROPERTIES: "true"
      ENABLE_WHITELIST: "false"
      ENFORCE_WHITELIST: "false"
      WHITELIST: "SOPHRONIOS"
      USE_AIKAR_FLAGS: "true"
      EXEC_DIRECTLY: "true"
      ENABLE_AUTOPAUSE: "false"
      AUTOPAUSE_TIMEOUT_EST: "300"
      AUTOPAUSE_TIMEOUT_KN: "120"
      AUTOPAUSE_TIMEOUT_INIT: "600"
      AUTOPAUSE_PERIOD: "10"
      AUTOPAUSE_KNOCK_INTERFACE: "eth0"
      MAX_TICK_TIME: "-1"
    tty: true
    stdin_open: true
    restart: unless-stopped
    volumes:
      # attach a directory relative to the directory containing this compose file
      - /MC-SERVER-DRIVE/LOBBY-SERVER/data:/data
```