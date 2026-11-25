# Git status

Adds a **Git status** card to a site's Overview showing, for the site's checkout (or the selected worktree):

- the current branch, or *detached HEAD*
- commits ahead of / behind the upstream branch, or *no upstream*
- staged, modified, untracked and conflicted file counts, or *clean*
- the number of stashes
- the last commit: short hash, subject and how long ago

Click **Refresh** to re-read it.

## Console command

```sh
lerd git-status:show                    # the project you are in
lerd git-status:show project-name           # a site by name
lerd git-status:show --project=project-name # same, as a switch (also -p project-name)
lerd git-status:show --all              # one line per site (also -a)
```

In the `--all` table, changes are abbreviated: `S` staged, `M` modified, `?` untracked, `!` conflicted.

## Turning the card on

Overview cards are off by default. Switch it on per site from the site's header in the dashboard, or in the project folder:

```sh
lerd plugin card git-status on
```

## Notes

- The card and the command are read-only: it never runs `git fetch`, so ahead/behind reflects the last time you fetched.
- The data comes from `GET /api/plugins/git-status/status?site=<site>`, which returns JSON.
