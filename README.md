# PlatformIndicator for Vencord

A modified version of Vencord's built-in **PlatformIndicators** plugin that also shows platform icons in the **friends list**.

The icons sit right after each friend's name and server tag. Each icon is colored by the status the friend has *on that platform*, so a friend who is idle on desktop but online on mobile shows a yellow monitor and a green phone.

## Features

Icons for desktop, mobile, web, console/embedded (game controller) and VR, shown:

| Location | Setting | Default |
| --- | --- | --- |
| Friends list (new) | Show indicators in the friends list | On |
| Member list and DM list | Show indicators in the member list | On |
| User profiles, as badges | Show indicators in user profiles, as badges | On |
| Messages | Show indicators inside messages | On |

The original option to color the mobile avatar indicator with the user's status is still there. All settings need a Discord restart.

## Installation

This is a user plugin, so it needs Vencord [built from source](https://docs.vencord.dev/installing/).

1. Clone this repo into Vencord's `src/userplugins` folder:

   ```bash
   cd Vencord/src/userplugins
   git clone https://github.com/TheUnknownMurda/PlatformIndicator-Vencord platformIndicators
   ```

2. Build Vencord from the Vencord folder:

   ```bash
   pnpm build
   ```

3. If Discord doesn't load Vencord from this folder yet, inject it:

   ```bash
   pnpm inject
   ```

4. Fully quit Discord (from the system tray) and start it again.

The plugin has the same name as the built-in one, so it replaces it and keeps your existing PlatformIndicators settings.

### Updating

```bash
cd Vencord/src/userplugins/platformIndicators
git pull
```

Then run `pnpm build` again and restart Discord.

## How it works

The friends list has no Vencord API for decorations, so the plugin uses two patches:

- The friends list row passes the indicators to Discord's name component (`DiscordTag`).
- `DiscordTag` renders them between the server tag and the username. That username is hidden until hover but still takes up space, so the icons have to come before it to stay next to the name.

Both patches only run when the friends list setting is on. If a Discord update breaks them, the friends list keeps working without the icons.

## Credits

Based on [PlatformIndicators](https://github.com/Vendicated/Vencord/tree/main/src/plugins/platformIndicators) by kemo, sunnie, Nuckyz and V, from [Vencord](https://github.com/Vendicated/Vencord).

## License

GPL-3.0-or-later, like Vencord. See the header in [index.tsx](index.tsx).
