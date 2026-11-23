# Changelog

All notable changes to **Dropout YouTube Organised** (originally "Dropout Browser (Local)") are documented here.

## [v20] - 2026-11-22
### Changed
- Browser tab title changed from "Dropout Browser (Local)" to **"Dropout YT Organised"**.
- Tab icon is now the "D" cropped from the Dropout logo on a transparent background (embedded as a data URI).
- README rewritten (prerequisites, API-key setup, features, privacy); screenshot link fixed by saving the image as `assets/screenshot.png` (the previous path contained spaces and quotes and did not render).

## [v19] - 2026-11-22
### Fixed
- **Sorting leaked between sections.** The Top Shows, Other Shows, Only on YouTube and Not on YouTube sections all shared the single `browse` sort introduced in [v8](#v8---2026-09-27), so changing one changed the rest. Each now has its own mode and direction (`browseTop`, `browseOther`, `browseOnlyYt`, `browseNotYt`). Existing saved sort is copied into each section once, so nothing resets.
- "Not on YouTube" cards showed the default arrow cursor on hover even though they are clickable (they open the show on watch.dropout.tv, from [v3](#v3---2026-09-27)); they now show the pointer.

## [v18] - 2026-11-22
### Added
- **Only on YouTube** section, placed before Not on YouTube. Holds every playlist that did not match a show, including "(Free Episodes)" playlists (unless they merely duplicate a show that already matched). Playlists with similar names are clubbed into seasons by stripping years, season and part numbers, so *CollegeHumor Shorts 2019* and *2020* become one show with two seasons.
- **Hide / Unhide show** in the right-click menu (introduced in [v11](#v11---2026-10-04)) for every show on every tab. A **"Show hidden shows"** toggle in Settings brings hidden shows back as normal. Hidden shows are removed from Latest, Favourites and My List unless the toggle is on.
- GPL-3.0-or-later licence header in the file; repository files (`LICENSE`, `README.md`, `.gitignore`, `.nojekyll`, GitHub Pages workflow, screenshot folder).

### Fixed
- The Latest and Favourites headers from [v16](#v16---2026-11-21) still did not match Top Shows (different font size, and a gap appeared at the top while scrolling) after the first attempt in [v17](#v17---2026-11-21). They now use exactly the Top Shows header markup.
- The translucent block on the peek card ([v16](#v16---2026-11-21)) still revealed the background at its right corners after the [v17](#v17---2026-11-21) edge fix. Corners are now square and the block slightly over-extends the card.
- The "Open this season's playlist on YouTube" button still used the old thin glyph; it now uses the same bold top-right SVG arrow as the rest of the app.

### Removed
- "Preview ribbons" button and the "keep Free-Episodes-only shows" checklist, both added as stop-gaps in [v17](#v17---2026-11-21).
- "Show unmatched playlists" button, added as a diagnostic in [v14](#v14---2026-10-05); its job is now done by the Only on YouTube section.
- Settings text shortened to "Move your data (favorites, watched history, API key, seasons left at)".

## [v17] - 2026-11-21
First GitHub-ready build. Mostly polish on the [v16](#v16---2026-11-21) Latest work after first real use.
### Added
- **Automatic new-show discovery.** v16 relied on the hardcoded catalogue, so brand-new shows such as *MP3* never appeared (and so never reached Latest). Unmatched "(Full Episodes)" playlists are now grouped by name and added as shows, with a **"New Show"** ribbon.
- "N shows" count on the Latest heading, as Top Shows has.
- Settings checklist for shows whose only playlist is a "(Free Episodes)" one, and a temporary "Preview ribbons" button (both replaced in [v18](#v18---2026-11-22)).
- First repository package prepared for GitHub.

### Changed
- Show-more arrow and **all sort arrows** replaced with bold, centred SVG icons (the v8/v16 glyph arrows were too thin and sat off-centre).

### Fixed
- Favourites rows with fewer than six entries showed blank grey placeholder cards ([v16](#v16---2026-11-21)); they now leave empty space and the overlay is hidden.
- Scrollbars on the Latest and Favourites rows hidden (rows still scroll).
- Translucent block did not fully cover the sixth card at the right edge (partially fixed here; finished in [v18](#v18---2026-11-22)).
- Latest heading style (partially fixed here; finished in [v18](#v18---2026-11-22)).

## [v16] - 2026-11-21
### Added
- **Latest** row above Top Shows (5 newest shows, one entry per show, Dimension 20 included) and a **Latest** tab after All Shows listing every show newest-first. A show with a new season moves to the top; the channel's own "Latest" playlist is ignored.
- **Peek card** in the Favourites and Latest rows: a sixth card half-covered by a sticky translucent black block with a circled arrow (Favourites → My List, Latest → Latest tab). Rows scroll horizontally while the block stays in place. This replaces the "Show more →" button used since [v8](#v8---2026-09-27).
- **Ribbons** peeking from behind the top-left of a card on every tab: "New Season" / "New Episode", detected by comparing playlist and item counts with a stored snapshot. First load only records a baseline; a ribbon clears when the show is opened.

### Changed
- "(Free Episodes)" playlists are now ignored when matching shows (they overlap with, but are incomplete compared to, the "(Full Episodes)" ones).
- "Mark all previous episodes watched/unwatched" ([v5](#v5---2026-09-27)) now includes the current episode.

## [v15] - 2026-10-05
### Fixed
- Cross-checked against [soitchu/unofficial-dropout-youtube-browser](https://github.com/soitchu/unofficial-dropout-youtube-browser) (GPL-3.0). The fuzzy matcher from [v2](#v2---2026-09-27) and [v14](#v14---2026-10-05) still missed shows whose YouTube titles drift between seasons, so hand-verified playlist IDs (`KNOWN_PLAYLIST_IDS`) are now merged in as a safety net; newer seasons found by matching are never dropped.
- EXTRA detection ([v9](#v9---2026-10-02)) refined: added "Last Looks" and bonus clip/episode/scene patterns, and fixed a bare "bonus" pattern that over-matched ordinary episodes.

## [v14] - 2026-10-05
### Fixed
- **Shows showing fewer seasons than the catalogue says** (reported for *Breaking News*: 7 seasons exist, only season 2 appeared). The title matcher added in [v2](#v2---2026-09-27) required near-exact names; it now also accepts whole-word containment when both names are at least 8 characters, to avoid collisions between short titles.

### Added
- "Show unmatched playlists" button in Settings to list channel playlists that matched no show (diagnostic; removed in [v18](#v18---2026-11-22)).

## [v13] - 2026-10-05
### Changed
- Logo reduced from 3× to **2×** (84px → 56px) after the [v11](#v11---2026-10-04) size proved too large.

### Fixed
- Sticky bars from [v11](#v11---2026-10-04): the Favourites bar stayed visible behind later section headers when scrolling past Top Shows. Each favourites bar and its row are now wrapped so the bar only sticks while its own row is on screen.
- Small gap above the frozen Dimension 20 bar.
- **Sort settings were not saved in Export/Import** (export was introduced in [v9](#v9---2026-10-02)). They are now included, and older export files without them still import (defaults fill in).

## [v11] - 2026-10-04
### Added
- **Right-click menu** on every show card: set custom cover (moved here from the card, where it appeared since [v3](#v3---2026-09-27)) and **Move to Top Shows / Move to Other Shows**.
- **Dimension 20 tab** between All Shows and My List, with its own Favourites row. Dimension 20 shows move out of the main browse view.
- **My List split** into an All Shows section and a Dimension 20 section, each with independent sorting and sticky bars.
- Sort state tracked for the new sections (`mylist`, `mylistD20`, `d20`, Favourites rows).

### Changed
- "Browse" tab renamed **All Shows**. The "All Shows N shows" heading scrolls away; the Top Shows, Other Shows and Not on YouTube bars freeze, keeping their sort controls.
- Logo enlarged to 3× (28px → 84px); judged too big and reduced in [v13](#v13---2026-10-05).
- Confirmed manually set covers for Not on YouTube shows are carried by Export/Import.

## [v10] - 2026-10-02
### Added
- **"Import data from a file…"** on the API-key setup screen, so a fresh copy of the file can be restored without entering a key first. Follow-up to the Export/Import added in [v9](#v9---2026-10-02), which was only reachable from Settings.

## [v9] - 2026-10-02
### Added
- **Export / Import data** (Settings): one JSON file with API key, watched episodes, favourites, covers and last-viewed seasons. Needed because browsers key `localStorage` to the file path, so a renamed or re-saved copy started empty.
- **Settings toggle "First season / Latest season"** for which season opens the first time a show is opened; the remembered season ([v7](#v7---2026-09-27)) takes over afterwards.
- Season controls reordered: `[season ▾] [‹] [↗ playlist] [›] [episode count]`, with prev/next greyed at the ends. Builds on the playlist button from [v5](#v5---2026-09-27).
- **"EXTRA" labelling:** trailers, Behind the Scenes and bonus content no longer consume episode numbers and show "EXTRA" instead; real episodes number sequentially.
- Real Dropout logo (image embedded, upscaled), replacing the text logo.

### Changed
- **Favourites row** ([v8](#v8---2026-09-27)) no longer has sort modes: it is always in the order favourited, newest first, with only the direction arrow.

### Fixed
- The text-rendered logo from [v8](#v8---2026-09-27) looked off; replaced by the real image above.

## [v8] - 2026-09-27
### Added
- **Favourites row** at the top of Browse: last five favourites, horizontally scrollable, own sort, and a "Show more →" link to My List.
- Sticky double header (favourites bar plus section bar) with a dynamic offset for the nav bar.

### Changed
- Sort dropdowns replaced by a **pill that cycles modes** (Alphabetical, Season Count, Series Release Date, Latest Season) with a circular ↑/↓ direction button. Replaces the dropdown and the "Last updated" option from [v4](#v4---2026-09-27).
- First-pass logo colour fix (replaced by the real logo in [v9](#v9---2026-10-02)).

## [v7] - 2026-09-27
### Added
- The app remembers the **last-viewed season per show** and reopens it.

## [v6] - 2026-09-27
### Fixed
- Episode label was based on its index in the sorted list, so it changed when sort direction flipped ([v5](#v5---2026-09-27)); it now uses the real playlist position.
### Changed
- Episodes open in **playlist context** on YouTube (`watch?v=…&list=…&index=…`) so the next episode autoplays.

## [v5] - 2026-09-27
### Added
- Button beside the season dropdown that opens that season's YouTube playlist.
- "Mark all previous episodes watched/unwatched" button on each episode card.
- Cover art for more Not on YouTube shows (e.g. Troopers, Cartoon Hell, Hardly Working, Very Mary-Kate).

### Changed
- Episode sort dropdown replaced by a single ↑/↓ icon button at the far right, after the episode count.

## [v4] - 2026-09-27
### Added
- "Last updated" sort option, from the newest playlist date per show (replaced in [v8](#v8---2026-09-27)).

## [v3] - 2026-09-27
### Added
- **Sectioned Browse view**: Top Shows, Dimension 20, Other Shows and **Not on YouTube**.
- Not on YouTube shows are listed greyed with a badge and open their page on watch.dropout.tv.
- Section headers with show counts; custom-cover and star buttons on cards.

### Changed
- The catalogue from [v2](#v2---2026-09-27) is now shown instead of every playlist on the channel.

## [v2] - 2026-09-27
### Added
- **Hardcoded catalogue (~120 shows)** from watch.dropout.tv/series, curated real cover art, and a fuzzy matcher linking each show to channel playlists. Replaces the title-grouping from [v1](#v1---2026-09-26).
- Dropout-style visual design: nav bar, search, refresh and settings buttons, show hero area.
- Watched episodes shown in greyscale; clicking the backdrop closes modals; API-key fields hardened against password managers.

### Removed
- Embedded video player ([v1](#v1---2026-09-26)) removed (it failed with error 153); episodes open on YouTube instead.

## [v1] - 2026-09-26
### Added
- Initial single-file, client-side app using the user's YouTube Data API v3 key: playlists grouped into shows by title, show grid with search, season and episode lists with durations, watched tracking, My List, custom covers and an embedded player.
