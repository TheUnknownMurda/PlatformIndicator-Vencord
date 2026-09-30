# PlatformIndicator for Vencord

A modified version of Vencord's built-in **PlatformIndicators** plugin that also shows platform icons in the **friends list**.

The icons sit right after each friend's name and server tag. Each icon is colored by the status the friend has *on that platform*, so a friend who is idle on desktop but online on mobile shows a yellow monitor and a green phone.

| Platform | Online | Idle | Do Not Disturb |
| :-- | :-: | :-: | :-: |
| Desktop | <img src="assets/desktop-online.svg" width="40" alt="Desktop, online"> | <img src="assets/desktop-idle.svg" width="40" alt="Desktop, idle"> | <img src="assets/desktop-dnd.svg" width="40" alt="Desktop, do not disturb"> |
| Mobile | <img src="assets/mobile-online.svg" width="40" alt="Mobile, online"> | <img src="assets/mobile-idle.svg" width="40" alt="Mobile, idle"> | <img src="assets/mobile-dnd.svg" width="40" alt="Mobile, do not disturb"> |
| Web | <img src="assets/web-online.svg" width="40" alt="Web, online"> | <img src="assets/web-idle.svg" width="40" alt="Web, idle"> | <img src="assets/web-dnd.svg" width="40" alt="Web, do not disturb"> |
| Embedded (console or game) | <img src="assets/embedded-online.svg" width="40" alt="Embedded, online"> | <img src="assets/embedded-idle.svg" width="40" alt="Embedded, idle"> | <img src="assets/embedded-dnd.svg" width="40" alt="Embedded, do not disturb"> |
| VR | <img src="assets/vr-online.svg" width="40" alt="VR, online"> | <img src="assets/vr-idle.svg" width="40" alt="VR, idle"> | <img src="assets/vr-dnd.svg" width="40" alt="VR, do not disturb"> |

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

Friends list support by [TheUnknownMurda](https://github.com/TheUnknownMurda).

## License

GPL-3.0-or-later, like Vencord. See [LICENSE](LICENSE).
