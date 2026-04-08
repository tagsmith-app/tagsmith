# TagSmith

**A desktop app for viewing and batch-editing media file metadata**

Fix timestamps, add GPS, propagate location, and edit IPTC keywords across hundreds of photos and videos — offline by default, no accounts required.

## Download

**[Get TagSmith from the Microsoft Store →](https://apps.microsoft.com/detail/9PL73JZKCG80?hl=en-us&gl=US&ocid=pdpshare)**

*(Free, Windows 10/11)*

## Features

- **View all metadata at a glance** – See filesystem, EXIF, XMP, and QuickTime dates side-by-side with an integrated preview pane
- **Edit timestamps** – Batch-edit EXIF, XMP, QuickTime, and filesystem timestamps; double-click any date cell to edit inline
- **Time Shift** – Fix an incorrect camera clock by shifting all selected timestamps by hours, minutes, or seconds
- **GPS tagging** – Add, edit, or erase GPS coordinates with an offline city database (68,000 cities, no internet required)
- **GPS Propagation** – Geotag DSLR files from your phone's GPS trail using timestamp proximity
- **Offline reverse geocoding** – Convert GPS coordinates to city and country text entirely offline
- **IPTC keywords** – Double-click any keyword cell to add, remove, or clear tags without overwriting existing ones
- **IPTC location metadata** – Add country, state, city, and sublocation fields written to both XMP and IPTC groups for maximum DAM compatibility (Lightroom, Capture One, stock agencies)
- **Filename date recovery** – Extract capture dates from structured filenames using flexible token patterns (useful for WhatsApp photos, screenshots, and scans)
- **Sampler tools** – Copy date, time, or GPS from one file and apply it across hundreds with live before/after previews
- **Edit queue** – Stage multiple selections and changes, review together, then apply in one batch with per-file status tracking
- **Preview before applying** – Review exactly what will change before writing to any file
- **Keyboard-driven workflow** – Norton Commander-style navigation for power users
- **AI landmark identification** *(optional)* – Identify landmarks and batch-geotag using Google Gemini and Google Places (requires your own API key)

## Supported Formats

| Category | Formats |
|----------|---------|
| **Images** | JPG, PNG, HEIC, TIFF, GIF, BMP, WebP |
| **RAW** | CR2, NEF, ARW, DNG, ORF, RW2, RAF, ERF, MRW, RAW |
| **Video** | MP4, MOV, M4V, M4A, MKV, WMV, 3GP |

## How It Works

1. **Open a folder** – Select a folder to scan for media files
2. **Select files** – Use checkboxes, click, or keyboard shortcuts to select files
3. **Make changes** – Edit dates inline, look up GPS, add keywords, shift timestamps, or parse dates from filenames
4. **Preview & Apply** – Review all pending changes, then apply in one batch

## Support & Feedback

- **Bug reports**: [Open an issue](https://github.com/tagsmith-app/tagsmith/issues)
- **Feature requests**: [Open an issue](https://github.com/tagsmith-app/tagsmith/issues)

## About This Repository

This repository is for **issue tracking and documentation only**. TagSmith is proprietary software; source code is not published here.

Official releases are distributed exclusively through the [Microsoft Store](https://apps.microsoft.com/detail/9PL73JZKCG80?hl=en-us&gl=US&ocid=pdpshare).

**Why no standalone installer?** A signed installer outside the Store requires a code signing certificate (~$300–500/year) — not practical for a free solo project. The Store version is free, signed by Microsoft, and auto-updates. If demand for a direct download grows, a GitHub Release becomes more feasible and I'll revisit it.

---

*TagSmith uses [ExifTool](https://exiftool.org/) by Phil Harvey for metadata processing and [GeoNames](https://www.geonames.org/) data (CC BY 4.0) for offline reverse geocoding.*
