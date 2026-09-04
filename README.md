<div align="center">

![banner](assets/banner.png)

![Tableau](https://img.shields.io/badge/Tableau-Public-orange?style=flat-square&logo=tableau&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-measures-2E75B6?style=flat-square)
![Power Query](https://img.shields.io/badge/Power%20Query-M%20language-118DFF?style=flat-square)
![Excel](https://img.shields.io/badge/Excel-cleaning-217346?style=flat-square&logo=microsoftexcel&logoColor=white)
![CSV](https://img.shields.io/badge/CSV%20%2B%20Hyper-extracts-6E56CF?style=flat-square)
![Level](https://img.shields.io/badge/level-free%20time%20projects-brightgreen?style=flat-square)

![stats](assets/stats.png)

</div>

---

## 👀 Preview

<div align="center">

![previews](assets/previews.png)

</div>

---

## 📊 Projects

| # | Project | Tool | Source | Output | Links |
|:-:|---|---|---|---|---|
| 1 | **Netflix Content** | `TABLEAU` | `netflix_titles.csv` · 6,234 rows | 11 sheets · map · KPI · filters | [🔗 Tableau Public](https://public.tableau.com/views/NETFLIXSNUCABDUL/TOTALMOVIES?:language=en-US&:display_count=n&:origin=viz_share_link) |
| 2 | **Uber Bookings** | `POWER BI` | Uber booking data · 33K rows | 3 pages · bookmarks · drill-through | 📄 `PROJECTS_PDF/UBER_DASHBOARD.pdf` |
| 3 | **Virat Kohli Career** | `POWER BI` | 516 international matches | 6 KPI cards · DAX · slicer | [🔗 Power BI share](https://app.powerbi.com/links/axEGJlm8ma?ctid=5beb351c-3fb8-418f-b612-fe36ace96ef3&pbi_source=linkShare) |

---

##  1 · Netflix — Tableau

`🗺️ filled map` `🥧 movie vs show` `📊 top 10 genre` `⭐ rating breakdown` `📈 titles per year` `🔍 title detail`

**Cleaning done**

| Issue | Rows | What I did |
|---|--:|---|
| `date_added` stored as text | 6,234 | cast to `date` · `release_year` to `int` · `show_id` forced back to text |
| `director` empty | 1,969 | kept as-is, never aggregated, no fake `0` |
| `cast` empty | 570 | excluded from any cast-level counting |
| `country` empty | 476 | in totals, dropped from the map only |
| `rating` empty | 10 | aliased, not deleted |
| `date_added` empty | 11 | left null, flagged in tooltip |
| duplicate titles | 57 | verified they're genuinely different releases, no dedupe |
| multi-genre strings | all | split `listed_in` on `,` to rank genres |

**What the data said**

`4,265 movies / 1,969 TV shows` · `68% : 32%` · `US 2,032 → India 777 → UK 348` · `TV-MA 2,027 is the top rating` · `peak 2018 → 1,063 titles` · `Documentaries 299 · Stand-Up 273`

> **14 worksheet filters** on this workbook — no calculated fields, no sets. Kept it honest.

---

## 🚗 2 · Uber — Power BI

`🧭 page navigator` `🔘 bookmarks` `↩️ drill-through` `🖼️ dynamic images` `📅 CALENDAR table` `🧮 MeasureTable`

**M / Power Query steps**

- [x] import → rename tables
- [x] `Promote Headers`
- [x] `Table.TransformColumnTypes` → `Booking Status` as `text`, `Img` as `text`
- [x] `STATUS_IMAGE` lookup → 5 statuses × image URLs: `Cancelled by Customer` · `Cancelled by Driver` · `No Driver Found` · `Incomplete` · `Completed`
- [x] `VEHICLE_IMAGE` table → 6 vehicle tiles driven by a slicer
- [x] built `CALENDAR(Date[Date])` → `Year / Quarter / Month / Day / Month Index / Quarter`
- [x] 1 active relationship, date table on the `one` side
- [x] measures in their own table, not scattered in `UBER_DATA`

**KPI cards shipped**

| `33K` | `21K` | `13K` | `11M` | `25` |
|:--:|:--:|:--:|:--:|:--:|
| total booking count | completed bookings | cancelled rides | booking value | avg distance |

> ⚠️ Two cards on `OVERVIEW` say `CANCELLED RIDES` — one is a leftover copy, rename it to `CANCELLATION %` and move on.

<details>
<summary><b>🧾 What lives in MEASURETABLE</b></summary>

`MEASURETABLE` → `AVG_DISTANCE` · `BOOKING_COUNT` · `BOOKING_VALUE` · `CANCELLED_RIDES` · `COMPLETED_BOOKINGS` — measures live in their own table so the fact table stays raw.
`UBER_DATA` → `Booking ID` · `Booking Status` · `Booking Value` · `Cancelled Rides` · `Status_Image`.

Bookmarks for view switching on the Analysis page: `YEAR PREVIEW` · `MONTH PREVIEW` · `QUARTER PREVIEW` · `DAY PREVIEW` (the first one is the active/default view).

</details>

---

## 🏏 3 · Virat Kohli — Power BI

`🃏 6 cards` `📊 runs vs opponent` `🍩 opponent share` `📈 runs by year` `🎚️ year slicer` `🖼️ hero image`

**Model** — `Virat_Kohli` ⟶ `Calender` ⟶ `Measures_Table`

| DAX measure | Meaning |
|---|---|
| `100s` | centuries |
| `50s` | fifties |
| `30+` | **my bucket** — innings of 30+ runs, not a source column |
| `Runs` | total runs |
| `Total_Matches` | match count |
| `HighestScore` | peak innings |
| `T20_First_Match` | date card |

**Power Query** — selected only `player · match_type · year · match_no · opponent · venue · runs · date` · promoted first row · fixed wrong auto-detected date type · `0` runs kept as a real `0`, not blanked

**Reads** `516 matches` · `77 × 100s` · `129 × 50s` · `270 innings 30+` · `highest 254` · `Australia 25.62% · England 23.63% · South Africa 18.16% · West Indies 15.17%` · first T20 `12-06-2010`

---

## 🧰 Skills on display

`**Tableau**`
`filled map` `worksheet filters` `tooltips` `show/hide` `device preview` `packaged .twbx` `Tableau Public` `date & string params`

`**Power BI**`
`power query (m)` `star-ish model` `calendar table` `dax measures` `bookmarks` `drill-through` `page navigator` `slicers` `dynamic images`

`**Cleaning**`
`null vs zero` `type casting` `promoted headers` `split delimited fields` `dedupe checks` `lookup tables` `alias unknowns` `don't drop silently`

---

## 🗂️ Repo

```
DATA_DASHBOARDS/
├── assets/            banner.png · previews.png · stats.png
├── PROJECT_FILES/     NETFLIX_DASHBOARD.twbx · VIRATKOHLI_DASHBOARD.pbix
├── PROJECTS_PDF/      one export per dashboard
└── MANUAL/            build steps · NETFLIX 3p · UBER 20p · KOHLI 20p
```

<details>
<summary><b>🚧 Not done yet</b></summary>

- `UBER_DASHBOARD.pbix` is still on my laptop → needs to land in `PROJECT_FILES/`
- no calculated fields / sets in the Tableau workbook yet
- Kohli dashboard is a single page — needs a format filter (Test / ODI / T20)
- published Tableau sheet is `TOTALMOVIES`; the fuller `NETFLIX` sheet needs a real publish

</details>

---

<div align="center">

*Freelance-free, deadline-free, built in spare time. Data from public Kaggle-style sources — credits to whoever published it.*

**Abdul Rahuman M** · [github.com/Abdulsf26](https://github.com/Abdulsf26)

</div>
