# quirkus-mcp

Read only MCP server for U of T Quercus and ACORN

[Quirkus](https://github.com/kevinyhe/quirkus) as its own binary

Does not require you to login, it reads the desktop app's saved sign-in and cache, so install Quirkus and sign in once first before using the mcp. Note that timetable and academic history come from whatever the app last synced from ACORN

Not affiliated with U of T or Instructure!!!

## Build

Needs Rust

```sh
git clone https://github.com/kevinyhe/quirkus-mcp
cd quirkus-mcp
cargo build --release
```

Binary is `target/release/quirkus-mcp`. Or `cargo install --path .` to put it on your PATH

## Setup

Claude Code

```sh
claude mcp add --scope user quirkus -- /path/to/quirkus-mcp
```

Claude Desktop (`claude_desktop_config.json`), or anything else that takes this format

```json
{ "mcpServers": { "quirkus": { "command": "/path/to/quirkus-mcp" } } }
```

If tools say "Not signed in", open the Quirkus app and sign in again.

## Tools

`list_courses` `upcoming_deadlines` `course_assignments` `get_assignment` `grades` `announcements`
`course_modules` `read_page` `read_file` `search` `inbox` `timetable` `academic_history`

Courses are matched by code (`CSC263`), id, or part of the name. `read_file` returns text for PDFs and
text/code files

## env

Only for testing

- `QUERCUS_BASE_URL` talk to something other than `https://q.utoronto.ca`
- `QUERCUS_PROFILE_DIR` use `<dir>/{cache,config,data}` instead of the app's folders

## Testing

```sh
cargo test
```

## Notes

- Whatever a tool returns goes straight to your AI provider

MIT
