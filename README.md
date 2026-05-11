# pair-extraordinaire

A small automation tool that generates co-authored pull requests to help earn the GitHub **Pair Extraordinaire** achievement.

## What it does

The script repeatedly:

1. Creates a feature branch
2. Appends a row to [`sessions.md`](./sessions.md)
3. Commits it with a `Co-authored-by:` trailer so both parties receive credit
4. Opens a pull request and immediately merges it

Each merged PR with a valid co-author trailer counts toward the badge.  
**Both** the commit author and the co-author receive credit — so running this with the default settings earns the badge for you and for [@Tivo0921](https://github.com/Tivo0921) at the same time.

## Prerequisites

| Tool | Purpose |
|------|---------|
| `git` | version control |
| [`gh`](https://cli.github.com/) | GitHub CLI — create & merge PRs |
| `bash` 4+ | script runtime |

Authenticate the GitHub CLI before running:

```sh
gh auth login
```

## Usage

```sh
# fork or clone the repo and enter it
git clone https://github.com/Tivo0921/pair-extraordinaire
cd pair-extraordinaire

# make the script executable
chmod +x pair.sh

# run with default settings (48 PRs, co-author: Tivo0921)
./pair.sh

# run a different number of PRs
./pair.sh 10
```

### Environment variables

| Variable | Default | Description |
|----------|---------|-------------|
| `COAUTHOR_NAME` | `Tivo0921` | GitHub username of the co-author |
| `COAUTHOR_EMAIL` | `shun020921@icloud.com` | Email of the co-author |
| `AUTHOR_EMAIL` | *(GitHub noreply)* | Your commit author email. Set to your real email if you want it linked to your GitHub account. |
| `SLEEP_SEC` | `2` | Seconds to sleep between PRs (avoid rate limits) |

Example — override the co-author:

```sh
COAUTHOR_NAME=octocat COAUTHOR_EMAIL=octocat@github.com ./pair.sh 5
```

Example — set your own email as author:

```sh
AUTHOR_EMAIL=you@example.com ./pair.sh 48
```

## How GitHub counts the badge

GitHub awards **Pair Extraordinaire** when you co-author commits that land in merged pull requests.  
Both the commit author and every `Co-authored-by:` party receive credit.

Badge tiers (as of 2025):

| Tier | PRs required |
|------|-------------|
| Bronze | 1 |
| Silver | 10 |
| Gold | 24 |

Running `./pair.sh 48` comfortably exceeds the gold tier and leaves room for future tier changes.

## Session log

Merged sessions are tracked in [`sessions.md`](./sessions.md).

## License

[MIT](LICENSE)
