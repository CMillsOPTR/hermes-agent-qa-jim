# Persistent Playlist Workflow Notes

Use this reference for recurring media-library playlist tasks where the user wants daily refreshes without library clutter.

## User preference pattern

- Create or identify one persistent destination playlist, such as `Daily Recommendations`.
- Modify that same playlist on future runs; do not create date-named or daily duplicate playlists unless explicitly requested.
- Prefer recently created/recently played playlists and the user's thumbs-up/favorites collection as sources.
- If multiple listening phases are requested, use one ordered playlist unless the user explicitly asks for separate playlists.

## Mutation verification

1. Confirm the destination title and current item count from fresh live state.
2. Perform the smallest supported add/remove/reorder operation.
3. Read back the destination title and item count.
4. If search/add controls fail to render or the count is unchanged, report the task as incomplete. Never fill the playlist with guessed tracks or claim success.

## Recurring fallback

When unattended authenticated mutation cannot be proven, schedule a reminder-assisted workflow instead. The reminder should tell the user to open and authenticate the service; it must not claim the account was modified. A later interactive run must verify the actual playlist mutation.