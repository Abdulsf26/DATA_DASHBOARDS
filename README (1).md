<h1 align="center">📊 DATA DASHBOARDS</h1>

<p align="center">
  <img src="https://img.shields.io/badge/TABLEAU-PUBLIC-E97627?style=for-the-badge&logo=tableau&logoColor=white" alt="Tableau">
  <img src="https://img.shields.io/badge/POWER%20BI-DESKTOP-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI">
  <img src="https://img.shields.io/badge/DAX-MEASURES-118DFF?style=for-the-badge&logo=microsoftexcel&logoColor=white" alt="DAX">
  <img src="https://img.shields.io/badge/POWER%20QUERY-M%20LANGUAGE-2E75B6?style=for-the-badge&logoColor=white" alt="Power Query">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/rows%20shaped-6,750-3fb950?style=social&labelColor=24292f" alt="rows">
  <img src="https://img.shields.io/badge/dashboards-3-58a6ff?style=social&labelColor=24292f" alt="dashboards">
  <img src="https://img.shields.io/badge/dax%20measures-11-d2a8ff?style=social&labelColor=24292f" alt="measures">
  <img src="https://img.shields.io/badge/tableau%20sheets-11-f778ba?style=social&labelColor=24292f" alt="sheets">
  <img src="https://img.shields.io/badge/nulls%20handled-25-ffa657?style=social&labelColor=24292f" alt="nulls">
  <img src="https://img.shields.io/badge/worksheets%20filtered-14-7ee787?style=social&labelColor=24292f" alt="filters">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/real%20datasets-3%20clean%200%20faked-3fb950?style=flat-square" alt="honest">
  <img src="https://img.shields.io/badge/build%20docs-20%20page%20PDFs-555?style=flat-square" alt="docs">
  <img src="https://img.shields.io/badge/when-free%20time%20only-888?style=flat-square" alt="free time">
</p>

---

<details>
<summary><b>🖼️ optional — dashboard screenshots</b> <i>(only renders if you upload the <code>assets/</code> folder; README works fine without it)</i></summary>

![previews](assets/previews.png)

</details>

---

## 📊 Projects

| # | Project | Tool | Source | Output | Links |
|:-:|---|---|---|---|---|
| 1 | **Netflix Content** | `TABLEAU` | `netflix_titles.csv` · 6,234 rows | 11 sheets · map · KPI · filters | [🔗 Tableau Public](https://public.tableau.com/views/NETFLIXSNUCABDUL/TOTALMOVIES?:language=en-US&:display_count=n&:origin=viz_share_link) |
| 2 | **Uber Bookings** | `POWER BI` | Uber booking data · 33K rows | 3 pages · bookmarks · drill-through | 📄 `PROJECTS_PDF/UBER_DASHBOARD.pdf` |
| 3 | **Virat Kohli Career** | `POWER BI` | 516 international matches | 6 KPI cards · DAX · slicer | [🔗 Power BI share](https://app.powerbi.com/links/axEGJlm8ma?ctid=5beb351c-3fb8-418f-b612-fe36ace96ef3&pbi_source=linkShare) |

---

## 🎬 1 · Netflix — Tableau

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

`4,265 movies / 1,969 TV shows` · `68% : 32%` · `US 2,032 → India 777 → UK 348` · `TV-MA 2,027 top rating` · `peak 2018 → 1,063 titles` · `Documentaries 299 · Stand-Up 273`

> **14 worksheet filters** in this workbook · **0 calculated fields, 0 sets** — kept it simple and honest.

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
- [x] measures in their own table, not scattered inside `UBER_DATA`

**KPI cards shipped**

| `33K` | `21K` | `13K` | `11M` | `25` |
|:--:|:--:|:--:|:--:|:--:|
| total booking count | completed bookings | cancelled rides | booking value | avg distance |

> ⚠️ Two cards on `OVERVIEW` both say `CANCELLED RIDES` — one is a leftover copy, rename it to `CANCELLATION %`.

<details>
<summary><b>🧾 What lives in MEASURETABLE</b></summary>

`MEASURETABLE` → `AVG_DISTANCE` · `BOOKING_COUNT` · `BOOKING_VALUE` · `CANCELLED_RIDES` · `COMPLETED_BOOKINGS` — measures live in their own table so the fact table stays raw.
`UBER_DATA` → `Booking ID` · `Booking Status` · `Booking Value` · `Cancelled Rides` · `Status_Image`.

Bookmarks for view switching on the Analysis page: `YEAR PREVIEW` · `MONTH PREVIEW` · `QUARTER PREVIEW` · `DAY PREVIEW` (first one is the default view).

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

**Power Query** — selected only `player · match_type · year · match_no · opponent · venue · runs · date` · promoted first row · fixed a wrong auto-detected date type · `0` runs kept as a real `0`, not blanked

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
├── PROJECT_FILES/     NETFLIX_DASHBOARD.twbx · VIRATKOHLI_DASHBOARD.pbix
├── PROJECTS_PDF/      one dashboard export per project
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

<p align="center">
  <img src="https://img.shields.io/badge/no%20client%20work-no%20deadlines-3fb950?style=flat&logo=github&logoColor=white" alt="free time">
  <img src="https://img.shields.io/badge/data-public%20sources-58a6ff?style=flat-square" alt="data">
  <img src="https://img.shields.io/badge/github-@Abdulsf26-24292f?style=flat-square&logo=github&logoColor=white" alt="me">
</p>
