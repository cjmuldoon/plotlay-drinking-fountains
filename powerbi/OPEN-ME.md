# Opening the Power BI report

`DrinkingFountains.pbip` is a Power BI Project: the report (`DrinkingFountains.Report`, PBIR format) and the semantic model (`DrinkingFountains.SemanticModel`, TMDL) saved as text, so the repo can show every change. Power BI Desktop opens it like a `.pbix`.

## What you need

- Power BI Desktop for Windows, a recent version (2026). If Desktop is older than about mid 2025, turn on **File, Options and settings, Options, Preview features, Power BI Project (.pbip) save option** and **Store reports using enhanced metadata format (PBIR)**, then restart Desktop.
- The repo folder on the Windows machine. In Parallels the Mac home folder is usually shared as `\\Mac\Home`.

## Open it

1. In Windows, go to the repo's `powerbi` folder and double-click `DrinkingFountains.pbip`.
2. The visuals are empty the first time. Select **Refresh** on the Home ribbon.
   - By default the data is read from the repo's public copy on GitHub (`DataFolder` is `https://raw.githubusercontent.com/cjmuldoon/plotlay-drinking-fountains/main/data/`). If Desktop asks how to connect, choose **Anonymous** and then **Connect**.
   - To read the files from disk instead, go to **Home, Transform data, Edit parameters** and set `DataFolder` to the full path of the repo's `data` folder, **ending with a backslash**. Then select **OK** and **Apply changes**.
   - If Desktop warns about privacy levels, choose **Ignore privacy levels** (all the sources are public open data).
3. Check the numbers (below).

If the report was updated while open, close Power BI and reopen the .pbip rather than using Apply external changes. (After Apply external changes one export drew the page at about 57% inside a much larger canvas; a full close and reopen put it right.)

## Check the numbers after Refresh

After **Refresh**:

| Where | Should read |
|---|---|
| **Seven cities**, card: Fountains in the seven study areas | 820 |
| **Seven cities**, 5-minute bars, first and last | Rome 98.6%, San Francisco 50.1% |
| **Seven cities**, 2-minute bars, first | Barcelona 73.5% |
| **District table** (Melbourne), first row | Melbourne (Remainder), 86.5% |
| **Fountains** (Melbourne) | 150 points |

Each small map on **Districts** shows one city; its title gives the whole study area (for example Melbourne: 97.6%). The 5-minute bars use the street length (reached km over street km), so they match the README to the tenth of a percent.

## The model

- **Cities**: one row per city (`data/tables/cities.csv`), keyed by `city` (MEL, SYD, NYC, SFO, PAR, BCN, ROM). Its shares are for the whole study area.
- **Districts**: one row per district (`districts.csv`), keyed by `district` (MEL-Carlton, PAR-7510401...), related to Cities by `city`.
- **Fountains**: one row per fountain used (`data/fountains/fountains.csv`), related to Cities by `city`.
- Measures: `Streets within 5 min` (reached km over street km), `Streets within 2 min`, `Fountains in study areas`, `District streets in reach`, `Fountain count`.

## The maps

- **Shape Maps** (Districts page): one per city, each with its own map file saved inside the report (that city's districts, keeping only the district code), so they draw on open. The Shape Map has no base map: water and land outside the city show as the background. If a map shows the world instead (an older Desktop can ignore a saved map): select it, then **Format visual**, **Visual**, **Map settings**, **Map type: Custom map**, **Add map type**, and choose the city's file from `..\data\geometry\` after cutting it from `districts.topojson` (or use the saved copy in `DrinkingFountains.Report\StaticResources\RegisteredResources`). If the Shape Map is not in the Visualizations pane, turn it on in **File, Options and settings, Options, Preview features, Shape map visual** and restart Desktop.
- **Azure Maps** (Fountains page): each fountain of the city picked. Your organisation's admin must allow Azure Maps (on by default on a personal account).

If a map visual comes up empty, drag the fields back:
- Shape Map: Location `Districts[district]`, Color saturation `[District streets in reach]`.
- Azure Maps: Location `Fountains[fountain]`, Latitude `Fountains[lat]` (Average), Longitude `Fountains[lng]` (Average).

Then save with **File, Save**, and if you like **File, Save as** a `.pbix`, which includes the data.
