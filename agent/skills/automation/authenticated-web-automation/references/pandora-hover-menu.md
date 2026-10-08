# Pandora Hover-Menu Safety Notes

Use this verified interaction model for Pandora-style playlist mutations:

1. Open the source playlist and hover the target track.
2. Click the track's three-dot action menu once.
3. Hover (do not click) the arrowed `Add to Playlist` item and wait for its submenu.
4. Select `Daily Recommendations` by exact visible label, never by menu position. Recent activity reorders entries, and adjacent `New Playlist` entries are unsafe lookalikes.
5. Verify a success toast or read back the destination playlist title and item count. A closed menu is not evidence of success.

If the available computer-control surface cannot issue a hover-only event, stop before the arrowed item and ask the user to hover it; perform only the final exact-label click.

Use a dedicated personal browser profile for unattended automation, not a work Chrome profile. If Pandora presents a failed CAPTCHA/human-verification challenge, require manual handling; never bypass it.
