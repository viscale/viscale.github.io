# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a static website for the **ViSCALE (Test-time Scaling for Computer Vision) Workshop** at CVPR2025. The site is built with pure HTML, CSS, and vanilla JavaScript, hosted on GitHub Pages.

## Architecture

### Site Structure
- **index.html** - Main landing page containing all sections (introduction, speakers, schedule, organizers, accepted papers, sponsors, contact)
- **schedule.html** - Standalone schedule component (embedded in index.html)
- **styles.css** - All styling with responsive design breakpoints at 768px and 480px
- **resources/** - Static assets organized by type:
  - `committee/` - Organizer profile images
  - `speaker/` - Speaker profile images
  - `sponsor/` - Sponsor logos
  - Cover images and favicon variants

### Key Features
1. **Dynamic Timezone Schedule** (index.html:383-426)
   - JavaScript converts UTC event times to user-selected timezone
   - Events array at line 384-409 defines all sessions in UTC
   - `updateSchedule()` function handles timezone conversion

2. **Responsive Navigation** (index.html:22-56)
   - Desktop: Horizontal nav bar with fixed positioning
   - Mobile (<480px): Hamburger dropdown menu
   - Implemented with vanilla JS toggle functions (myFunction, Close)

3. **CSS Architecture**
   - Custom properties using clamp() for responsive typography (styles.css:6)
   - Dark theme (#121212 background) throughout
   - Grid layouts for speakers (3 columns) and organizers (5 columns)
   - Responsive breakpoints collapse grids on smaller screens

## Development Workflow

### Local Development
Since this is a static site with no build process:
```bash
# Serve locally (any static server works)
python3 -m http.server 8000
# or
npx serve .
```

Visit http://localhost:8000 to preview changes.

### Deployment
The site deploys automatically via GitHub Pages from the `main` branch. Any push to main triggers deployment.

## Common Modifications

### Adding a Speaker/Organizer
1. Add profile image to `resources/speaker/` or `resources/committee/`
2. Add entry to respective grid in index.html:
   - Speakers section starts at line 81
   - Organizers section starts at line 280
3. Follow the existing `<div class="committee-member">` pattern with image, link, and name

### Updating Schedule
1. Modify the `events` array in the inline script (index.html:384-409)
2. Update the corresponding table rows in the schedule section (index.html:151-196)
3. Ensure time IDs (time1, time2, etc.) match the array indices

### Adding Accepted Papers
Update the list in the papers section starting at index.html:267

### Styling Changes
- All styles are in styles.css
- Key sections: navbar (.navbar), cover (.cover), sections (.section), grids (.committee-grid, .speaker-grid)
- Responsive breakpoints at 768px and 480px handle mobile layouts

## Important Notes

- No build system, package manager, or dependencies required
- All JavaScript is inline in index.html (lines 381-458)
- Images should be optimized before adding to resources/ (current PNGs are large)
- The site uses Font Awesome 4.7.0 from CDN for the hamburger icon
- Timezone selection supports 9 timezones; times are stored as UTC ISO strings
