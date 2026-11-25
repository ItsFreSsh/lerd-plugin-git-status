# git-status — a lerd plugin

Shows the git state of your [lerd](https://lerd.sh) sites: branch, ahead/behind the upstream, staged / modified / untracked / conflicted files, stashes and the last commit.

- **Overview card** on each site in the lerd dashboard, with a Refresh button.
- **Console command** `lerd git-status:show` for the current project, a named site, or every site at once.

It is read-only and never runs `git fetch`, so ahead/behind reflects your last fetch.

## Install

```sh
git clone <this repository> git-status
lerd plugin install "$PWD/git-status"
```

Then switch the card on per site, from the site's header in the dashboard or in the project folder:

```sh
lerd plugin card git-status on
```

## Usage

```sh
lerd git-status:show                    # the project you are in
lerd git-status:show my-site            # a site by name
lerd git-status:show --project=my-site  # same, as a switch (also -p)
lerd git-status:show --all              # one line per site (also -a)
```

```
SITE         BRANCH       SYNC         CHANGES
my-site      development  in sync      1M 4?
other-site   main         ↑2           clean
```

`S` staged, `M` modified, `?` untracked, `!` conflicted.

## Requirements

lerd 1.39 or newer, on Linux or macOS, with `git`, `curl`, `jq` and `column` on the PATH.

## How it works

| File | Role |
| --- | --- |
| `plugin.yaml` | Declares the command, the API endpoint and the Overview card |
| `bin/gitstate` | Reads `git status --porcelain=v2` for a folder and prints JSON |
| `bin/status` | API endpoint `GET /api/plugins/git-status/status?site=<site>` |
| `bin/show` | The console command |
| `ui/card.html` | The Overview card |

## Development

The installed copy does not follow this folder. After a change:

```sh
lerd plugin remove git-status && lerd plugin install "$PWD"
```

## License

MIT
