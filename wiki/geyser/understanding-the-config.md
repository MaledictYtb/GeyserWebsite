---
title: Understanding the Config
description: This page covers basic information about the Geyser config and the function of each option.
---

This page covers basic information about the Geyser config and what each option does. Though they are explained in the configuration itself, this explains what each option does in more detail.

## Bedrock Section {#bedrock-section}
The options for Geyser on the Bedrock-facing end. Mostly contains options for how Bedrock edition will see the server.

**`address`**: The address of Geyser on the Bedrock end. In most all scenarios, this should not need to be changed, unless you want to limit what IPs can connect to your server. Leave it at 0.0.0.0 (default), unless otherwise instructed in the setup guide.

**`port`**: The port Geyser will run on. By default, it is 19132 in Bedrock. If you are using a server hosting provider, you may not have this port available to you - in which case, read the setup guide to proceed.

**`clone-remote-port`**: Some hosting services change your Java port everytime you start the server and require the same port to be used for Bedrock/UDP connections. This option makes the Bedrock port the same as the Java port every time you start the server. This option does not do anything on the Standalone version of Geyser.

**`motd1`**: The first line of the MOTD for Geyser.

**`motd2`**: The second line of the MOTD for Geyser. **Please keep in mind, this option will only work if Geyser is shown in the Friends tab!**

**`server-name`**: The world name that is shown in the top-right area of the pause menu and the settings menu.

**`compression-level`**: An number value that represents how much to compress outgoing traffic. Can be any number from -1 to 9; any other value will be replaced with the nearest acceptable value. The higher the number, the more CPU processing that is used but with less bandwidth used. Default is 6.

**`enable-proxy-protocol`**:  Whether to enable PROXY protocol or not for clients. You DO NOT WANT this feature unless you run UDP reverse proxy in front of your Geyser instance. You do NOT need this for BungeeCord (and forks), Velocity, or Waterfall.

**`proxy-protocol-whitelisted-ips`**: Disabled by default, and only enable this if you use "enable-proxy-protocol". A list of allowed PROXY protocol speaking proxy IP addresses/subnets. Should really only be used when you are not able to use a proper firewall (usually true with shared hosting providers etc.). Keeping this list empty means there is no IP address whitelist. IP addresses, subnets, and links to plain text files containing either are supported.

## Remote Section {#remote-section}
Options for the remote (Java) server.

**`address`**: The address of the Minecraft: Java Edition server you want to join. By default, this value is `auto`. By keeping it as `auto`, the address, port, and Floodgate support will be automatically configured. In standalone, keeping this as `auto` sets the remote address to 127.0.0.1.

**`port`**: The port of the Minecraft: Java Edition server you specified in the `address` section. For plugin versions, if address has been set to "auto", the port will also follow the server's listening port.

**`auth-type`**: The authentication type of the Minecraft: Java Edition server. Valid options are `online`, `offline`, and `floodgate`. 

**Please keep in mind, what you specify in the Geyser `auth-type` option MUST be the same as what the remote server has (with the exception of Geyser being in online mode and remote being in offline mode). You simply cannot join an online mode server without a genuine account. If you want to allow Minecraft: Bedrock Edition accounts to join without a Minecraft: Java Edition account, see the [Floodgate](/wiki/floodgate/) wiki page.**

**`use-proxy-protocol`**: Whether to enable PROXY/HAProxy protocol or not while connecting to the server. This is useful only when:
- Your server supports PROXY protocol (it probably doesn't)
- You run Velocity or BungeeCord with its respective option enabled.
- IF YOU DON'T KNOW WHAT THIS IS, DON'T TOUCH IT!

**`forward-hostname`**: Forwards the hostname/IP address that the Bedrock client used to connect over to the Java server. This is designed to be used for forced hosts on proxies.

## General Options {#general-options}
General Geyser options that are mostly specific to Geyser itself.

**`floodgate-key-file`**:  Floodgate uses encryption to ensure use from authorised sources. This should point to the public key generated by Floodgate (BungeeCord, Spigot or Velocity). You can ignore this when not using Floodgate. If you're using a plugin version of Floodgate on the same server, the key will automatically be picked up from Floodgate.The key file path for Floodgate. Requires that you have [Floodgate](/wiki/floodgate/) installed and the `auth-type` set to `floodgate`. 

**`saved-user-logins`**: For online mode authentication type only. 
Stores a list of Bedrock players that should have their Java Edition account saved after login.
This saves a token that can be reused to authenticate the player later. This does not save emails or passwords,
but you should still be cautious when adding to this list and giving others access to this Geyser instance's files.
Removing a name from this list will delete its cached login information on the next Geyser startup.
The file that tokens will be saved in is in the same folder as this config, named `saved-refresh-tokens.json`.

Format:

```yml
saved-user-logins:
  - jeb_
  - Dinnerbone
```

**`command-suggestions`**: Bedrock clients freeze or crash when opening up the command prompt for the first time with a large amount of command suggestions. This config option disables command suggestions being sent to prevent any freezing. **Since 1.16.100:** command freezing and crashing has been largely reduced; you may no longer need this option disabled.

**`passthrough-motd`**: If the MOTD should be relayed from the remote server. Causes the `motd1` and `motd2` options in the bedrock section to no longer have a use.

**`passthrough-protocol-name`**: Relay the protocol name (e.g. BungeeCord [X.X], Paper 1.X) - this is only really useful when using a custom protocol name! This will also show up on sites like MCSrvStatus. \<mcsrvstat.us\>

**`passthrough-player-count`**: If the current and max player counts should be relayed from the remote server.

**`legacy-ping-passthrough`**: If enabled, manually pings the server by impersonating a Minecraft client instead of using the server's API. **This option should *only* be enabled if your MOTD or player count is not accurate,** as it can cause errors especially on BungeeCord. This option does nothing on Geyser Standalone.

**`ping-passthrough-interval`**: How often the fake Minecraft client should attempt to ping the remote server to update information, in seconds (a setting of 1 will ping the server every second; a setting of 3 will ping the server every three seconds). Only relevant for standalone and legacy ping passthrough. Increase the number if you're getting timeout or BrokenPipe exceptions.

**`forward-player-ping`**: Whether to forward player ping to the server. While enabling this will allow Bedrock players to have more accurate ping, it may also cause players to time out more easily.

**`max-players`**: The maximum amount of players shown when pinging the server. This does not actually cap how many players can join the Geyser instance at this time. The number will visually increase when pinging if the amount of players is greater, as Bedrock clients will not even attempt to join a full server.

**`debug-mode`**: If debug messages should be printed in console. Useful if you run into an error and need more context. Yes, this will cause more messages, warnings or even errors in console - some packets aren't translated.

**`allow-third-party-capes`**: If third party (Optifine, 5zig, LabyMod, etc.) capes should be displayed to the bedrock player.

**`allow-third-party-ears`**: If third party Deadmau5-style ears should be enabled. Currently only supports MinecraftCapes.

**`show-cooldown`**: Bedrock Edition currently does not have Java Edition 1.9+ combat mechanics. In order to get around this, Geyser sends a fake cooldown by sending a title message. This cooldown should not show if 1.8 combat mechanics are in use. The options available for this setting are `false` (no cooldown is sent), `title`/`true` (a cooldown indication is shown in the title), or `actionbar` (a cooldown indication is shown in the action bar). All other options default to `false`.

**`show-coordinates`**: Bedrock Edition has an option to show coordinates in the top-left part of your screen. This setting enables or disables this.

**`disable-bedrock-scaffolding`**: Whether Bedrock players are blocked from performing their scaffolding-style bridging.

**`emote-offhand-workaround`**: Since Java Edition 1.9, clients have had the ability to switch the item in their mainhand and offhand with a keybind. Bedrock Edition does not have this ability, so this config option makes up for it, If set, when a Bedrock player performs any emote, it will swap the offhand and mainhand items, just like the Java Edition keybind. There are three options this can be set to:
- `disabled` - the default/fallback, which doesn't apply this workaround
- `no-emotes` - emotes will NOT be sent to other Bedrock clients and offhand will be swapped. This effectively disables all emotes from being seen.
- `emotes-and-offhand` - emotes will be sent to Bedrock clients and offhand will be swapped

**`default-locale`**: The default locale to send to players if their locale could not be found. This option is disabled by default - to enable it, remove the "#" in front of the option.

**`cache-images`**: Specify how many days images will be cached to disk to save downloading them from the internet. A value of 0 is disabled. (Default: 0)

**`allow-custom-skulls`**: Allows custom skulls to be displayed when placed. Keeping them enabled may cause a performance decrease on older/weaker devices.

**`max-visible-custom-skulls`**: The maximum number of custom skulls to be displayed per player. Increasing this may decrease performance on weaker devices. Setting this to -1 will cause all custom skulls to be displayed regardless of distance or number.

**`custom-skull-render-distance`**: A number value specifying the radius in blocks around the player in which custom skulls are displayed. 32 by default.

**`add-non-bedrock-items`**: Whether to add (at this time, only) the furnace minecart as a separate item in the game, which normally does not exist in Bedrock Edition. This should only need to be disabled if using a proxy that does not use the "transfer packet" style of server switching. If this is disabled, furnace minecart items will be mapped to hopper minecart items. This option requires a restart of Geyser in order to change its setting.

**`above-bedrock-nether-building`**: Bedrock prevents building and displaying blocks above Y127 in the Nether - enabling this config option works around that by changing the Nether dimension ID to the End ID. The main downside to this is that the sky will resemble that of the End sky in the Nether, but ultimately it's the only way for this feature to work.

**`force-resource-packs`**: Force clients to load all resource packs if there are any. If set to false, it allows the user to disconnect from the server if they don't want to download the resource packs.

**`xbox-achievements-enabled`**: Allows Xbox achievements to be unlocked. **This disables certain commands so the Bedrock client can't "cheat" to get them; this cannot be worked around if you want to enable this**. Commands such as /gamemode and /give will not work from Bedrock with this enabled.

**`log-player-ip-addresses`**: Whether player IP addresses will be logged by the server.

**`notify-on-new-bedrock-update`**: Whether to alert the console and operators that a new Geyser version is available that supports a Bedrock version that this Geyser version does not support. It's recommended to keep this option enabled, as many Bedrock platforms auto-update.

**`unusable-space-block`**: Which item to use to mark unavailable slots in a Bedrock player inventory. Examples of this are the 2x2 crafting grid while in creative, or custom inventory menus with sizes different from the usual 3x9. A barrier block is the default item (minecraft:barrier is therefore the default value). Takes any Minecraft Bedrock identifier, e.g. `minecraft:apple`. To set this to a custom item, you will need to add the `geyser_custom:` namespace.

## Metrics {#metrics}

bStats is a stat tracker that is entirely anonymous and tracks only basic information about Geyser, such as how many people are online, how many servers are using Geyser, what OS is being used, etc. You can learn more about bStats [here](https://bstats.org/). To see Geyser Stats, see [here](https://bstats.org/plugin/server-implementation/GeyserMC/).

**`enabled`**: If metrics are enabled

**`uuid`**: UUID of the server, don't change this!

## Advanced Options {#advanced-options}

**`scoreboard-packet-threshold`**: Geyser updates the Scoreboard after every Scoreboard packet, but when Geyser tries to handle a lot of scoreboard packets per second can cause serious lag. This option allows you to specify after how many Scoreboard packets per seconds the Scoreboard updates will be then limited to four updates per second.

**`enable-proxy-connections`**: Allow connections from ProxyPass and Waterdog. See https://www.spigotmc.org/wiki/firewall-guide/ for assistance - use UDP instead of TCP. **This option does not need to be enabled in instances like BungeeCord or Velocity**.

**`mtu`**: https://en.wikipedia.org/wiki/Maximum_transmission_unit - The internet supports a maximum MTU of 1492 but could cause issues with packet fragmentation. 1400 is the default.

**`use-direct-connection`**: Whether to connect directly into the Java server without creating a TCP connection. This should only be disabled if a plugin that interfaces with packets or the network does not work correctly with Geyser. If enabled on plugin versions, the remote address and port sections are ignored. If disabled on plugin versions, expect performance decrease and latency increase.

Default Geyser Config: [config.yml](https://github.com/GeyserMC/Geyser/blob/master/core/src/main/resources/config.yml)