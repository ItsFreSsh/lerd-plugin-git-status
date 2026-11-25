# git-status — a lerd plugin

Shows the git state of your [lerd](https://lerd.sh) sites: branch, ahead/behind the upstream, staged / modified / untracked / conflicted files, stashes and the last commit.

- **Overview card** on each site in the lerd dashboard, with a Refresh button.
- **Console command** `lerd git-status:show` for the current project, a named site, or every site at once.

It is read-only and never runs `git fetch`, so ahead/behind reflects your last fetch.

## Install

From the terminal:

```sh
lerd plugin install https://github.com/ItsFreSsh/lerd-plugin-git-status.git
```

Or from the lerd dashboard: open **Plugins → Install from folder or git** and paste the URL above.

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

## Updating

A plugin installed from git does not update on its own. To get the latest version, remove it (its data is kept) and install it again:

```sh
lerd plugin remove git-status
lerd plugin install https://github.com/ItsFreSsh/lerd-plugin-git-status.git
```

## Development

Install from a local clone; the installed copy does not follow the folder, so reinstall after a change:

```sh
lerd plugin remove git-status && lerd plugin install "$PWD"
```

## License

MIT
