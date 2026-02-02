# Changelog

All notable changes to TagSmith will be documented in this file.

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
