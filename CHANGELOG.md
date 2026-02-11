# Changelog

All notable changes to TagSmith will be documented in this file.

## [1.4.0] - 2026-02-10

### Changed
- **Source dropdown label updates**: Renamed "Derived" group to "Parsed"; removed trailing ellipses from "File Name Pattern" and "Custom / Sample / Erase" options
- **Opaque pattern-match highlight on sticky columns**: Purple source highlight on the File Name column now uses opaque backgrounds so scrolled content no longer bleeds through
- **Sampler tool purple color scheme**: Eyedropper button and sampled-cell glow changed from orange to purple, aligning with the source field's purple visual language
- **Immediate source column highlighting**: Purple source shading now appears as soon as a source field is selected, rather than waiting for a destination to be chosen — includes filename pattern matches
- **Checkbox column selection hint**: Replaced semi-transparent glow with opaque background and subtle pulsing border glow to prevent bleed-through over sticky columns
- **Reduced glow intensities**: Sampler cell glow and checkbox hint glow are smaller and less distracting
- **Toolbar visual refinement**: Toolbar now has its own distinct surface (`#272727` background with bottom shadow) to separate it from the file table. Vertical divider lines between Edit/GPS/Actions sections replaced with subtle background bands for professional, non-grid-like grouping
- **Always-visible summary banner**: The status row (file count, preview stats) is now always rendered — before a folder is loaded it shows an onboarding prompt, eliminating the vertical layout shift when files load
- **Removed header subtitle**: The "Select a folder to view metadata" text next to the logo has been removed; the always-visible summary banner and highlighted Select Folder button now serve this purpose
- **Expand/collapse toggle widened scope**: The column expand/collapse chevron (≫/≪) now affects GPS Latitude, GPS Longitude, and Camera Model columns in addition to all date columns; button tooltip updated from "Expand date columns" to "Expand columns"
- **Polished interface depth**: Toolbar, dropdowns, inputs, and buttons now use subtle gradients, inset shadows, and layered box-shadows for a more dimensional, desktop-app feel rather than flat web styling
  - Toolbar background uses a top-to-bottom gradient with stronger shadow for a floating panel look
  - All dropdowns and text inputs have rounded corners (6px), inset shadows, and subtle bottom highlights
  - Apply/Cancel/Preview buttons use vertical gradients with inner top highlights for a raised 3D effect
  - Icon buttons and erase toggle given matching gradient and shadow treatment
  - Focus states include a subtle blue glow ring
- **Inset GPS zone**: The GPS section in the toolbar is styled as a recessed panel (darker fill, inset shadows, reversed border lighting) to visually distinguish it from the raised toolbar surface
- **Actions zone container removed**: The shaded container around Apply Changes / Cancel buttons has been removed for a cleaner look
- **Merged header and status row**: Removed the divider line between the top header bar and the folder/status row; both now share a transparent background with the status row content shifted closer to the header
- **Header layout reorganization**: Cancel (scan) button moved from the top header into the status row between the scan status indicator and Rescan button, styled consistently as a small button; "Include Subfolders" label font size increased slightly for better visual hierarchy
- **Table header depth**: Column headers now use a subtle gradient background with a soft bottom shadow
- **Batch completion dialogs**: Replaced Chromium `alert()` with native Electron `dialog.showMessageBox()` for batch results — prevents input focus loss after dismissing the dialog

### Added
- **Filename Pattern source**: Extract dates from filenames using a configurable token-based parser
  - New "File Name Pattern…" option in the Source dropdown
  - Token chip builder: compose patterns from `YYYY`, `MM`, `DD`, `HH`, `mm`, `ss` tokens
  - Separator modes: any non-digit character, custom character set, or no separator
  - Match preference: first or last occurrence when multiple matches exist
  - Live match stats showing how many selected files matched successfully
  - Matched filenames highlighted in purple in the File Name column
  - Options area slides open below the toolbar when filename pattern is selected
- **Zoom limits**: Zoom In capped at 150% and Zoom Out capped at 50% to prevent toolbar overflow at extreme zoom levels
- **Responsive toolbar**: Source and Destination dropdowns reflow to a stacked layout at narrow effective widths, keeping Apply/Cancel buttons always visible
- **Dynamic zoom/resize policy**: Zoom cap and minimum window width are computed from the same invariant (`effectiveWidth ≥ 1080 CSS-px`), so the two constraints stay in lockstep
  - Zooming in raises the minimum window width (prevents shrinking too small for the zoom level)
  - Shrinking the window lowers the maximum zoom (prevents zooming in beyond what the width supports)
  - Zoom In menu item grays out when at the dynamic cap
  - Window can now shrink to 1080px at 100% zoom (previously locked at 1280px)

### Fixed
- Filename pattern source cells not highlighting purple (sourceField type mapping mismatch)
- **Auto-zoom-out on window resize**: Shrinking the window to its minimum width would sometimes auto-reduce zoom level, causing a visible content "jump". Resize events now only update constraints (min window size, Zoom In menu state) without altering the zoom factor itself
- **GPS erase preview not showing**: Activating GPS erase mode (🗑️) did not display erase previews in the table — stale coordinate values from previous input shadowed the erase indicators. GPS write preview is now correctly suppressed during erase mode
- **Empty `.table-root:focus` ruleset**: Removed vestigial empty CSS rule; intent comment consolidated onto `outline: none` declaration
- **GPS city search not greyed out**: The GPS city search input now correctly appears disabled (greyed out) when "Apply GPS" is unchecked, matching the behaviour of the Latitude and Longitude fields
- **GPS trash icon line wrap**: Prevented the GPS erase button from dropping to a second line at narrow window widths by increasing `MIN_EFFECTIVE_WIDTH` from 1056 to 1080
- **"Apply GPS" label wrapping**: The "Apply GPS" checkbox label text no longer wraps to two lines at intermediate window widths
- **Folder load not resetting toolbar state**: Loading a new folder now properly resets sampler mode, erase mode, GPS erase mode, date/time picker visibility, and GPS sampler — previously these could persist across folder changes
- **Input fields unfocusable after native dialogs**: Text inputs (GPS lat/lng, city search) could become unclickable after a native dialog closed (folder picker, About box, batch completion). Fixed by re-focusing webContents after native dialogs and replacing Chromium `alert()` with Electron's native `dialog.showMessageBox()`

## [1.3.0] - 2026-02-04

### Added
- **Graphical Date Picker**: Click the calendar icon (📅) to select dates visually
  - Month/year navigation with decade view
  - Highlights today and currently selected date
  - Click a date to instantly apply it
- **Graphical Time Picker**: Click the clock icon (🕐) to set time with spinner controls
  - Hour, minute, and second spinners with up/down buttons
  - Direct input supported in each field
  - Badge indicator shows when custom time is set (non-default)
- **Date/Time Sampler Tool**: Click the eyedropper icon to sample dates from existing files
  - Click any date cell in the table to copy its value
  - Automatically fills both date and time fields
  - Visual feedback with highlighted sampler cursor
- **GPS Sampler Tool**: Sample GPS coordinates from existing files
  - Click the eyedropper next to GPS fields to activate
  - Click any file's GPS cell to copy its coordinates
  - Works with both latitude and longitude fields

### Changed
- **Streamlined header**: Subtext changed to "Select a folder to view metadata" which now only appears when file table is empty
- Date/time picker buttons now properly toggle closed on second click (previously would flicker closed then reopen)
- Time picker resets to default noon (12:00:00) when loading a new folder or after completing a batch operation

### Fixed
- **Custom time not applied**: Time picker selections were being ignored, always defaulting to 12:00:00 when applying changes
- **UI accessible during batch processing**: All source/destination controls, GPS settings, and file table are now disabled during batch apply operations to prevent accidental changes (scrolling remains enabled to monitor progress)

## [1.2.0] - 2026-01-30

### Added
- **Metadata Table**: Read-only diagnostic view showing all existing metadata organized by source
  - Categories: File System, EXIF, XMP, QuickTime, GPS, Camera
  - Collapsible sections with field count badges
  - Displays below preview image (right dock) or beside it (bottom dock)
- **Column Visibility**: Customize which columns are shown in the file table
  - Right-click any column header or use View → Columns... to access
  - Grouped by category: File System, EXIF, XMP, QuickTime, GPS, Camera
  - New Camera columns: Make, Model, Lens
  - "Show All" and "Defaults" buttons for quick configuration
  - Settings persisted across sessions
  - Columns automatically revealed when selected as source or destination
  - GPS columns auto-reveal when "Apply GPS" is checked
- **Frozen columns**: Checkbox, status, and File Name columns now stay visible when scrolling horizontally
- **Keyboard Shortcuts Help** (`F1`): New dialog showing all keyboard shortcuts organized by category
- **Preview on Hover toggle** (View menu): When disabled (default), preview only updates on click or right-click, not on mouse hover
- **Right-click preview (no selection change)**: Right-click a row to move the highlight bar and update preview without modifying selection
- Smart prefetching: Next/previous 2 files are prefetched for instant navigation

### Changed
- **Edge-to-edge layout**: File table, preview pane, and log panel now extend to window edges for a cleaner appearance
- **Sharp corners throughout**: Removed rounded borders from main content areas for consistent visual language
- **Aligned headers**: File table and preview pane headers share identical height for perfect divider alignment
- **Simplified splitter**: Resize handle between table and logs is now a clean horizontal line
- **Preview pane separation**: Added subtle border to distinguish preview pane from file table
- **View menu reorganization**: Reordered items with Columns at top, Logs grouped with layout options near bottom
- **Default column visibility**: Streamlined visible columns (File Modified, EXIF Original, QuickTime Create/Modify, GPS Lat/Lng, Camera Model)
- **Preview pane default width**: Increased right-docked preview width from 15% to 20%
- Preview now follows keyboard highlight bar (not checkbox selection)
- Row highlight is more visible and consistent between mouse hover and keyboard navigation

### Fixed
- **Zoom In keyboard shortcut**: `Ctrl+=` now works correctly on Windows
- Cell shading during preview: Source (purple) and destination (orange) backgrounds display correctly for selected rows
- Header shading accuracy: Destination column headers only highlight when they contain pending changes
- GPS column header shading: Latitude and Longitude headers correctly highlight when GPS data will be written or erased

## [1.1.0] - 2026-01-27

### Added
- **Image Preview Pane**: New split-view preview pane for quick visual identification of files
  - Preview images directly in the app without leaving TagSmith
  - Supports JPG, PNG, GIF, HEIC (Windows 11+), and RAW formats (CR2, NEF, ARW, DNG, etc.)
  - Toggle between "fit to pane" and "100% zoom" with click or Space key
  - Resizable pane with drag handle
  - Switch between right-side and bottom positions
  - Layout preferences (size, position, visibility) are persisted across sessions
  - Preview updated on hover by default (equivalent to today's "Preview on Hover" mode)
- **Video Thumbnails**: MP4 and MOV files display preview thumbnails
  - Uses OS-native thumbnail generation for fast, reliable previews
  - HEVC/H.265 videos require Microsoft HEVC Video Extensions codec
  - Graceful fallback to placeholder with codec hint when unavailable
- **Norton Commander-style keyboard navigation**:
  - Arrow keys move highlight bar without affecting selection
  - First file is auto-highlighted when folder loads for immediate keyboard use
  - `INSERT` toggles selection and moves to next file
  - `SHIFT+Arrow` inverts selection while moving through files
  - `Ctrl+B` sets range anchor, `Ctrl+E` selects range to current position
  - `Ctrl+D` deselects all files
  - `Ctrl+A` selects all supported files
  - `Ctrl+Enter` opens highlighted file in default app
  - `P` to toggle preview pane visibility
  - `Ctrl+Shift+R` toggles preview between right and bottom positions
  - `Ctrl+L` toggles logs panel
- **View menu enhancements**: Preview position controls, "Restore Default Layout" option

### Changed
- Table focus border changed from bright cyan to subtle gray for less visual distraction

## [1.0.1] - 2026-01-19

### Fixed
- App icon now displays correctly in taskbar and window title (was showing default Electron icon)
- Header logo now loads properly in packaged builds

### Changed
- Build process updated to use two-phase icon embedding via rcedit to work around Windows symlink permission issues

## [1.0.0] - 2026-01-18

### Added
- Initial release
- Scan folders for media files with EXIF/XMP/QuickTime metadata
- View filesystem timestamps (created, modified, accessed)
- View EXIF timestamps (DateTimeOriginal, CreateDate, ModifyDate)
- View XMP timestamps (DateCreated, CreateDate, ModifyDate)
- View QuickTime timestamps (CreateDate, ModifyDate, TrackCreateDate, TrackModifyDate, MediaCreateDate, MediaModifyDate)
- Batch edit timestamps across multiple files
- Copy timestamps between metadata fields
- Set custom date/time values
- Erase metadata timestamps
- GPS coordinate viewing and editing
- GPS place lookup (cities, states, countries) with autocomplete
- Subfolder scanning option
- Virtualized table for handling large folders
- Real-time scan progress with streaming results
