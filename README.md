# Human Memory Dashboard

An interactive R Markdown flexdashboard visualizing memory performance across various learning and recall conditions, confidence levels, sleep quality, and voice type. Built using data from the Multimodal Memory Dataset collected at the Hutchinson Lab of Cognitive Neuroscience at University of Oregon.

**Authors:** Ziyuan Chen, Isha Chhabra, America Romero

------------------------------------------------------------------------

## Overview

This dashboard presents four analyses of recognition memory performance across up to 15 experimental sessions with 3 participants:

-   **Accuracy vs. Confidence** — how confidence ratings (high/low) relate to memory accuracy over sessions
-   **Accuracy vs. Memory Conditions** — how learning (encoding) condition and recall timing affect memory accuracy
-   **Accuracy vs. Sleep Quality** — whether self-reported sleep quality predicts session accuracy
-   **Accuracy vs. Voice** — whether the voice type during encoding affects memory accuracy

------------------------------------------------------------------------

## Repository Structure

```         
.
├── dashboard_product_v2.Rmd       # Main dashboard source file
├── index.html             # Pre-rendered dashboard (viewable via GitHub Pages)
├── README.md
└── data/                  # Not included — see Data section below
    ├── combined_data.csv
    └── Survey.xlsx
```

------------------------------------------------------------------------

## Data

The data files required to run this dashboard are **not included** in this repository as they contain unpublished lab data. Please contact the authors for more information.

### `combined_data.csv`

Trial-level recognition memory data with the following columns:

| Column | Description |
|------------------------------------|------------------------------------|
| `subjId` | Participant ID |
| `session` | Session number (1–15) |
| `run` | Run number within session |
| `trial` | Trial number within run |
| `cueId` | Cue identifier |
| `pairId` | Image-word pair identifier |
| `mmmId` | MMM dataset image ID |
| `nsdId` | NSD dataset image ID |
| `itmno` | Item number |
| `word` | Target word for the pair |
| `voiceId` | Numeric voice identifier |
| `voice` | Voice type used during encoding (nova, echo, onyx, shimmer) |
| `sharedId` | Shared stimulus identifier |
| `enCon` | Encoding condition (1 = Single, 2 = Repeats, 3 = Triplets) |
| `reCon` | Recall condition (1 = Within Session, 2 = Across Sessions) |
| `mmmId_lure` | MMM ID of the lure image |
| `nsdId_lure` | NSD ID of the lure image |
| `image1` | Filename of image 1 |
| `image2` | Filename of image 2 |
| `correct_resp` | Correct response |
| `resp` | Participant response (1 & 4 = high confidence, 2 & 3 = low confidence) |
| `resp_RT` | Response reaction time (seconds) |
| `recog` | Participant's recognition response |
| `trial_accuracy` | Trial accuracy (0 or 1) |
| `subject_id` | Source CSV filename for this trial |

### `Survey.xlsx`

Session-level survey data with the following columns:

| Column    | Description                                     |
|-----------|-------------------------------------------------|
| `subjId`  | Participant ID (must match `combined_data.csv`) |
| `Date`    | Date of session                                 |
| `session` | Session number (must match `combined_data.csv`) |
| `sleep`   | Subjective sleep quality rating (1–5 scale)     |
| `mood`    | Subjective mood rating (1–5 scale)              |
| `hunger`  | Subjective hunger rating (1–5 scale)            |
| `stress`  | Subjective stress rating (1–5 scale)            |

> **Note:** Only `sleep` is used in the current dashboard. The remaining survey columns (`mood`, `hunger`, `stress`) are available for future analyses.

------------------------------------------------------------------------

## Requirements

This dashboard requires **R** (≥ 4.1) and the following packages:

``` r
install.packages(c(
  "flexdashboard",
  "tidyverse",
  "ggplot2",
  "scales",
  "lme4",
  "emmeans",
  "readxl",
  "gt",
  "showtext",
  "viridis",
  "RColorBrewer",
  "colorspace",
  "ggrepel",
  "colorblindr",
  "gghighlight",
  "plotly",
  "afex",
  "paletteer",
  "htmltools"
))
```

> **Note:** `colorblindr` is not on CRAN. Install it from GitHub:
>
> ``` r
> remotes::install_github("clauswilke/colorblindr")
> ```

------------------------------------------------------------------------

## How to Run

1.  Clone this repository:

    ``` bash
    git clone https://github.com/zchen0351/edld652-dashboard-product.git
    cd edld652-dashboard-product
    ```

2.  Add data files to the project root:

    ```         
    combined_data.csv
    Survey.xlsx
    ```

3.  Open `dashboard_product_v2.Rmd` in RStudio and click **Knit**, or run from the R console:

    ``` r
    rmarkdown::render("dashboard_product_v2.Rmd")
    ```

4.  Open the rendered `dashboard_product_v2.html` in your browser to view the dashboard.

------------------------------------------------------------------------

## Notes

-   The dashboard uses [IBM Plex Sans](https://fonts.google.com/specimen/IBM+Plex+Sans) via `showtext` and `font_add_google()`. An internet connection is required on first render for the font to load.
-   All colour palettes use the [Okabe-Ito](https://jfly.uni-koeln.de/color/) CVD-safe scheme.
-   Mixed-effects models are fit using `lme4::lmer()` with random intercepts per participant.
