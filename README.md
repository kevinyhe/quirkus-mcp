# quirkus-mcp

MCP server for U of T Quercus and ACORN. Read-only. Stdio.

It's the MCP half of [Quirkus](https://github.com/kevinyhe/quirkus) as its own binary. It has no login of its
own: it reads the desktop app's saved sign-in and cache. So install Quirkus and sign in once first.
Timetable and academic history come from whatever the app last synced from ACORN.

Unofficial. Not affiliated with U of T or Instructure.

## build

Needs Rust.

```sh
git clone https://github.com/kevinyhe/quirkus-mcp
cd quirkus-mcp
cargo build --release
```

Binary is `target/release/quirkus-mcp`. Or `cargo install --path .` to put it on your PATH.

## setup

Claude Code:

```sh
claude mcp add --scope user quirkus -- /path/to/quirkus-mcp
```

Claude Desktop (`claude_desktop_config.json`), or anything else that takes this format:

```json
{ "mcpServers": { "quirkus": { "command": "/path/to/quirkus-mcp" } } }
```

If tools say "Not signed in", open the Quirkus app and sign in again.

## tools

`list_courses` `upcoming_deadlines` `course_assignments` `get_assignment` `grades` `announcements`
`course_modules` `read_page` `read_file` `search` `inbox` `timetable` `academic_history`

Courses are matched by code (`CSC263`), id, or part of the name. `read_file` returns text for PDFs and
text/code files.

## env

Only for testing.

- `QUERCUS_BASE_URL` talk to something other than `https://q.utoronto.ca`
- `QUERCUS_PROFILE_DIR` use `<dir>/{cache,config,data}` instead of the app's folders

## test

```sh
cargo test
```

## notes

- Only sends GETs. Can't submit or change anything.
- Talks to `q.utoronto.ca` and nothing else. ACORN data is read from disk.
- Whatever a tool returns goes to your AI provider.

MIT
