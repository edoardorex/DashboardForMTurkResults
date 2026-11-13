# MTurk Results Dashboard

A PHP and Chart.js dashboard for exploring image/video quality-study results.
It reads the MySQL schema produced by
[ImageAndVideoQualityAmazonMTurk](https://github.com/edoardorex/ImageAndVideoQualityAmazonMTurk).

The dashboard visualizes existing records; it does not create HITs or replace
the collection scripts.

## Available views

| View | Purpose |
| --- | --- |
| File history | Ratings for an individual image or video |
| Worker history | Ratings submitted by a selected worker |
| Radar comparison | Comparison of two workers' ratings |
| Rating distribution | Quality-rating distribution for one file |
| Submission counts | Workers ranked by completed submissions |
| Scatter plot | Submission volume versus mean rating |
| Demographic consistency | Differences in age/sex entries across submissions |
| Sex distribution | Demographic grouping of responses |
| Screen resolution | Distribution of reported screen sizes |
| Age distribution | Distribution of reported ages |
| Modular dashboard | Three selected charts shown together |

Consistency checks are exploratory signals, not evidence of worker dishonesty.
Do not interpret small samples or demographic groupings as causal findings.

## Local development setup

1. Install a compatible PHP runtime with the **mysqli** extension and MySQL.
2. Prepare a development copy of the `dbmysql` database containing `immquality`
   and `vidquality`.
3. Update the database connection settings in the PHP pages and widgets.
   Credentials are configured in source, not through a centralized environment
   configuration in the original project; keep real secrets out of version control.
4. Serve the repository through PHP rather than opening files directly.

A loopback-only development server can be started from the repository root:

```sh
php -S 127.0.0.1:8080
```

Open `http://127.0.0.1:8080/index.php` and select a chart.
The pages use [Chart.js](https://www.chartjs.org/) for browser-side rendering.
Do not publicly expose participant data or the unreviewed prototype.

## Repository guide

- [index.php](index.php): dashboard entry page.
- [chartFile.php](chartFile.php), [chartWorker.php](chartWorker.php):
  individual histories.
- [radar.php](radar.php), [cake.php](cake.php), [scatter.php](scatter.php):
  comparison and distribution views.
- [age.php](age.php), [sexChart.php](sexChart.php),
  [resolution.php](resolution.php): demographic/display summaries.
- [personal.php](personal.php): modular chart selection.
- Corresponding `*Widget.php` pages: embedded chart versions.

This schema is specific to the related script project. The later
[MTurkTools application](https://github.com/edoardorex/MTurkTools) has its own
task-aware tables and integrated dashboard; it is not a drop-in database source.

## Original demonstration

[![Watch the original dashboard](Cattura.PNG)](https://drive.google.com/file/d/1R7hEdR1PL4Sk4YCNi7PqjyXeyBKS1AtC/view?usp=sharing)

The original video predates the screen-resolution and age charts.
Handle worker identifiers and demographics under the study's consent,
access-control, and retention requirements.

## Attribution

The original README credits **Edoardo Re, 2019**, and references Chart.js.
This repository is a fork of
[edoardore/DashboardForMTurkResults](https://github.com/edoardore/DashboardForMTurkResults).
Original source and history are preserved; no software license is added or changed.
