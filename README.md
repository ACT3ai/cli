# ACT3 CLI (`act3`)

Direct your ACT3 production from the command line — find shots, change your
movie, generate video, and move files between ACT3 and your disk.

This repository ships the **compiled `act3` binary** for each platform. There is
nothing to build and no runtime to install.

## Install

Pick the build for your machine, put it on your `PATH`, and make it executable.

| Platform | Binary |
| -------- | ------ |
| Mac (Apple Silicon — M1, M2, M3, M4) | `bin/Mac-Apple_Silicon/act3` |
| Mac (Intel) | `bin/Mac-Intel_CPU/act3` |
| Linux (x86-64) | `bin/linux-amd64/act3` |
| Linux (ARM64) | `bin/linux-arm64/act3` |
| Windows (x86-64) | `bin/windows-amd64/act3.exe` |
| Windows (ARM64) | `bin/windows-arm64/act3.exe` |

Not sure which Mac you have? Click the Apple menu → About This Mac. If it lists a
**chip** (M1, M2, M3, M4), it is Apple Silicon; if it lists a **processor**
(Intel Core), it is Intel. Every Mac sold since late 2020 is Apple Silicon.

macOS / Linux:

```bash
git clone https://github.com/ACT3ai/cli.git
cd cli
sudo install -m 755 bin/Mac-Apple_Silicon/act3 /usr/local/bin/act3   # your platform here
act3 --help
```

On macOS, Gatekeeper may block the first run of a downloaded binary. Allow it
under **System Settings → Privacy & Security**, or:

```bash
xattr -d com.apple.quarantine /usr/local/bin/act3
```

Windows: copy `act3.exe` into a directory on your `PATH`.

## Sign in

```bash
act3 login          # opens your browser, hands the credential back
act3 status         # which backend, signed in?, reachable?
act3 doctor         # which ACT3 is this, and can every command run there?
act3 logout
```

On a machine with no browser, paste a key instead:

```bash
act3 login --api-key <your-api-key>
```

## How it works

One command does one thing. To act on many shots, use `act3 select` to get the
ids and `act3 batch create` to act on them — or a shell loop.

```
act3 <noun> <verb> [ids] [flags]
```

The nouns, by what they do:

- **Select** — find things (free): `character`, `digital-actor`, `genre`,
  `layer`, `pattern`, `scene`, `select`, `sequence`, `set`, `shot`, `tag`,
  `timeline`
- **Upload** — put your files into ACT3: `asset`, `broll`, `mocap`, `note`,
  `project`, `script`
- **Download** — get files onto your disk: `export`
- **Change** — edit your movie (free): `batch`, `change`, `line`, `lock`,
  `outfit`, `prompt`, `snapshot`, `version`
- **Generate** — make pixels and sound (spends credits): `audit`, `blend`,
  `camera-plan`, `job`, `look`, `plan`, `reframe`
- **Manage** — projects, credits, your team, jobs: `analytics`, `capabilities`,
  `context`, `credits`, `estimate`, `org`, `publish`
- **Local** — this tool: `doctor`, `help`, `login`, `logout`, `status`

## 4D sets

```bash
act3 set list --search courtroom              # find a set's id
act3 set yaml <setId> --out ./courtroom.yaml  # its 4D model, with its revision
act3 set yaml-save <setId> ./courtroom.yaml --base-revision <rev> --confirm
act3 set upload <setId> ./location_scout/ --confirm
act3 set export --format zip --out ./sets_backup
```

Also `create`, `show`, `shots`, `usage`, `url`, `add-node`, `add-picture`,
`import-blend` and `delete`. A command that changes a set shows its plan first
and changes nothing until you add `--confirm`.

Name the set once with `--set <id|name>` (or `ACT3_SET_ID`) and leave `<setId>`
out; every answer says which set ACT3 used and why.

## Learn a command

Every command documents itself, down to each flag's values and an example that
runs:

```bash
act3 <noun> --help          # every verb for that noun
act3 <noun> <verb> --help   # every flag, every value, and an example
```

## Scripting

`--json` prints exactly what ACT3 sent, one line, for `jq`. Other global flags:
`--project-id` (act on one project without moving your cursor), `--api-url`
(point at a different ACT3), `--set` (the 4D set a call means when it names
none), and `--verbose` (the detail behind an error).

## License

UNLICENSED — © ACT3 AI.
