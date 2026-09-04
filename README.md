# CityStrides Leaderboard Tracker

This project tracks the top 50 runners on CityStrides and generates a static HTML leaderboard with weekly changes.

## Setup

1.  Ensure you have `uv` installed.
2.  Install dependencies:
    ```bash
    uv sync
    ```

## Usage

Run the update script to fetch the latest data and generate the website:

```bash
uv run update_leaderboard.py
```

This will:
1.  Read `leaderboard_data.json` (if it exists) to get the previous week's stats.
2.  Fetch the current top 50 runners from CityStrides.
3.  Calculate the change in rank and streets run.
4.  Save the new data to `leaderboard_data.json`.
5.  Generate `index.html`.

The generated site also has a **Map** tab. Its image is kept between normal
updates. Add `--map` when you want to refresh it from Conor's public
CityStrides map. The capture uses your default Firefox profile, which must be
signed into CityStrides as Conor:

```bash
uv run update_leaderboard.py --map
```

Use `--no-serve` if the script should exit after updating the files:

```bash
uv run update_leaderboard.py --map --no-serve
```

If the signed-in profile is not Firefox's default, set
`CITYSTRIDES_FIREFOX_PROFILE` to its directory before running the command.

## Automation

To run this weekly (e.g., every Sunday at 8 PM), add a cron job:

```bash
0 20 * * 0 cd /path/to/citystride_ranking && uv run update_leaderboard.py
```
