# RebuffedItemLevel

Shows average equipped item level and GearScore in your character frame, when inspecting another player, and next to the name in player tooltips. No setup is needed after installation.

## Display

In your character frame, the values appear below the title selector. When inspecting a player, they appear below the character description. A player tooltip might show `[iLvl 232.5 | GS 5000]`.

- `...`: Data is still loading.
- `?`: No data is available, or the player cannot currently be inspected.
- `*`: The cached value for another player is more than ten minutes old.

For other players, the server must first provide equipment data. Stay nearby and briefly hover over the player. Automatic inspections do not start in combat. An open inspect window takes priority.

## Calculation

Item level is averaged across 17 equipment slots, including the ranged weapon or relic. Shirts and tabards are excluded. Empty slots count as zero. A two-handed weapon counts for both weapon slots when the off hand is empty.

GearScore uses the classic [GearScoreLite formula and slot weights](https://github.com/Arcitec/GearScoreLite_Reborn), without penalties for missing enchants. Hunter weapons, Titan's Grip and heirlooms receive their specific adjustments. Other GearScore versions may return different values. A separate GearScore addon is not required.

## Inspections and caching

Other players are automatically inspected at most once per hover. Results remain current for ten minutes and are reused during that period. Automatic inspections are spaced at least two seconds apart. An unanswered request times out after five seconds; move your mouse away and back to try again.

Your own equipment is recalculated in response to relevant game events. Missing item data is retried for a limited time. Other players' data is only cached for the current session.

RebuffedRaidMarket can read your GearScore through `RebuffedItemLevel_GetPlayerGearScore()`. This returns the cached value without starting another equipment scan.

## Versions and update notices

Stable versions are published as GitHub Releases using `major.minor.patch` tags. The first number changes for incompatible changes, the second for new features, and the third for fixes. See [Releases](https://github.com/Derfavo/RebuffedItemLevel/releases) for downloads and release notes.

Update detection runs entirely inside WoW, using the same approach as DBM: addon messages exchange installed versions with other users in your party, raid and guild. Checks start automatically at login and when group or guild membership changes. Messages are hidden addon traffic, not ordinary chat. Replies are delayed and throttled to avoid repeated traffic during raid invites.

A newer version must be reported by two different players before the addon warns you. Future release dates are rejected. Confirmed versions are saved, so the notice can also appear at later logins. Each addon warns at most once per newer version per session. `/rebuffedupdates` shows your installed versions and any confirmed updates.

This does not contact GitHub or check a central server. If nobody you meet has a newer copy, the addon cannot know that a new release exists. No Windows task, external checker or automatic installation is used. DBM itself is not required.

To update, download the latest release's source ZIP, close WoW, extract it and copy the `RebuffedItemLevel` folder into `Interface/AddOns/`, replacing the previous folder. Do not copy the outer repository folder. Your settings in WTF remain untouched.
