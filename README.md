# Trending YouTube Videos - Data Analysis

A data analysis project on the Trending YouTube dataset, covering videos that
trended across 10 countries: Canada (CA), Germany (DE), France (FR), Great
Britain (GB), India (IN), Japan (JP), South Korea (KR), Mexico (MX), Russia
(RU), and the United States (US).

The work is done in a single Jupyter notebook that loads the raw data, runs 15
analysis tasks, and produces a set of charts saved as PNG files.

## Dataset

The dataset is a single zip archive (`trendingYT.zip`) containing, for each
country:

* `{country}videos.csv.zst` - video metadata (title, channel, tags, views,
  likes, dislikes, publish time, trending date, etc.), zstd-compressed.
* `{country}_category_id.json` - mapping of numeric `category_id` values to
  category names and an `assignable` flag.

Some CSV files contain non-UTF-8 characters, so the notebook reads them with
`encoding_errors='replace'`.

## Requirements

* Python 3.x
* pandas
* numpy
* matplotlib
* zstandard

Install the dependencies with:

```
pip install pandas numpy matplotlib zstandard
```

`zstandard` is also installed from inside the notebook in the setup cell.

## How to run

1. Place `trendingYT.zip` somewhere on your machine.
2. Open `youtube_data.ipynb` in Jupyter.
3. Update the `zip_path` variable in the Task 1 cell to point at your copy of
   the zip file.
4. Run all cells from top to bottom.

On the first run the notebook creates an `images` folder next to itself and
writes every chart there as a PNG.

## What the notebook does

The notebook is organised into 15 tasks:

1. Read every country CSV from the zip, add a `country` column, and combine
   them into one dataframe.
2. Extract all videos that have no tags (`[none]`).
3. Compute total views per channel.
4. Move videos with comments disabled, ratings disabled, or removed/errored
   into a separate `excluded` dataframe.
5. Add a `like_ratio` column (likes divided by dislikes).
6. Cluster each video's publish time into 10-minute intervals.
7. Compute the number of videos and average likes/dislikes per interval.
8. Count the number of videos per tag.
9. Find the tags used by the largest number of videos.
10. Compute the average like ratio for each (tag, country) pair.
11. Find the most viewed video per (trending_date, country).
12. Split `trending_date` into separate year, month, and day columns.
13. Find the most viewed video per (month, country).
14. Load all category JSON files into a lookup dictionary.
15. Count videos that fall into non-assignable categories, per country.

## Generated charts

The charts are written to the `images` folder:

| File | Description |
| --- | --- |
| `01_entries_per_country.png` | Number of trending entries per country |
| `02_no_tags_per_country.png` | Videos with no tags per country |
| `03_top_channels_by_views.png` | Top 10 channels by total views |
| `04_exclusion_reasons.png` | Reasons videos were excluded |
| `05_like_ratio_distribution.png` | Distribution of the like ratio |
| `07_videos_by_publish_time.png` | Number of videos by 10-minute publish interval |
| `09_top_tags.png` | Top 10 tags by number of videos |
| `12_entries_per_month.png` | Trending entries per month |
| `14_top_us_categories.png` | Top 10 video categories in the US |
| `15_non_assignable_per_country.png` | Videos in non-assignable categories per country |

## Project structure

```
.
├── youtube_data.ipynb     # main analysis notebook
├── trendingYT.zip         # raw dataset (not included here)
├── images/                # charts saved by the notebook
└── README.md
```
