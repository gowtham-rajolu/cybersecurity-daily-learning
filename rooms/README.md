# Room-by-room daily notes

Keep each TryHackMe room's notes separate so progress, commands, observations, and lessons do not get mixed together.

## Folder and file naming

Use this structure:

```text
rooms/
  RootMe/
    2026-11-23.md
    2026-11-24.md
  Anonymous/
    2026-11-19.md
  <RoomName>/
    YYYY-MM-DD.md
```

- Create one dated Markdown file for each room worked on each day.
- If multiple rooms are practised on the same day, create a separate file inside each room's folder.
- If the same room is practised on another day, create another dated file in that room's folder.
- Record only commands actually run, outputs actually observed, and progress actually achieved.
- Clearly mark unfinished tasks; never claim a shell, flag, or room completion unless verified.
- Keep general daily summaries separate from room-specific technical notes.

## Suggested note sections

1. Room and date
2. Goal for the session
3. Target environment (avoid publishing credentials or sensitive information)
4. Enumeration and observations
5. Commands run and what they mean
6. Findings and lessons learned
7. Current progress / next steps
8. References
