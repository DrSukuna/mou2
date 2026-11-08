# Morium Khatun — Interactive 3D Portrait & Memory Gallery

Transform the 3D photo archive into a personal portfolio and memory gallery for **Morium Khatun**, Class 9 student at Banagram SB High School (HS). This integrates all 28 uploaded photos into the 3D Fibonacci sphere and flat grid, adds rich visual animations (interactive 3D card tilt, floating particle embers, idle orbit drift), and provides a live photo uploader to easily add or update photos anytime.

## User Review & Critical Decisions

> [!IMPORTANT]
> Morium has provided 28 portraits and personal background details. The plan synthesizes these real assets into the 3D showcase with custom captions and celebratory Bengali/English subtitle motifs.

- **Confirmed Identity & Bio**: Name updated to **Morium Khatun** (`Morium<em>Khatun</em>`). Bio set to: *"Student of Banagram SB High School (HS), Class 9. A personal archive of memories, festivals, and captured smiles."*
- **Photo Selection**: All 28 uploaded photos will be featured. 21–28 will populate the interactive Fibonacci 3D sphere with an avatar icon for Morium, and all photos will appear in the high-res flat grid view and FLIP lightbox.
- **Enhanced Animations**:
  - **3D Card Hover Tilt**: Subtle mouse-position based perspective tilting (`rotateX`/`rotateY`) on individual photo cards.
  - **Floating Ambient Dust / Stars**: Canvas-based ambient particle field drifting smoothly in 3D behind the sphere.
  - **Gentle Idle Drift**: Very slow, subtle auto-rotation when no interaction is occurring, pausing instantly on touch/drag.
  - **In-App Photo Manager**: Quick upload modal so Morium can add or swap pictures directly from her phone or computer anytime without coding.

---

## 1. Overview & Core Concept

- **What It Does**: A showcase for Morium Khatun combining a 3D spherical photo gallery, fluid drag/momentum rotation, scroll dolly zoom, full-screen curated grid, and an animated FLIP lightbox with personalized photo captions.
- **Target Audience / Purpose**: Personal memory gallery and creative portfolio for Morium, her school friends, and family.
- **Key Value**: Preserves the high-performance CSS 3D Fibonacci engine while personalizing the storytelling, branding, and imagery with delightful micro-animations.

---

## 2. User Experience & Visual Design

### Key User Flows
1. **Intro & Splash Reveal**: Splash screen introduces *Morium Khatun — Memories & Moments 2026*, loading her photos seamlessly with an elegant progress bar.
2. **Interactive 3D Sphere**: User drags to rotate the sphere in 3D space, scrolls to dolly camera zoom, and observes floating ambient light particles. The center title *"Memories in the Wild"* or *"Cherished Moments"* remains optically centered.
3. **Card Interaction & Tilt**: Hovering over cards causes a subtle 3D tilt responding to cursor position. Clicking any card initiates a smooth FLIP transition opening the lightbox with story captions.
4. **Grid & Upload View**: Toggle into the full masonry/grid view to see all 28 photos, with an "Add Photo" button to upload new pictures directly.

### Visual Identity & Theme
- **Color Palette**: Rich deep obsidian background (`#050505`), soft warm cream ink (`#f4f2ef`), warm rose-gold accent highlights (`#e0a899` / `#d4a373`), and translucent glass chrome.
- **Typography**: Editorial serif (*Playfair Display*) for name and memory titles paired with clean *Inter* for descriptions and metadata.
- **Motion & Feedback**:
  - Luminous floating dust particles with varying z-depth.
  - Inertia momentum with gentle idle floating when released.
  - FLIP lightbox zoom with high-contrast text and photo details.

---

## 3. Technical Architecture & Component Structure

```
┌────────────────────────────────────────────────────────┐
│                   Top Navigation Chrome                │
│   [Morium Khatun]                    [Menu / Add Photo]│
└───────────────────────────────────────────┬────────────┘
                                            │
                     ┌──────────────────────┴──────────────────────┐
                     ▼                                             ▼
       ┌───────────────────────────┐                 ┌───────────────────────────┐
       │   3D Stage (#stage)       │                 │   Flat Grid (#grid)       │
       │  ┌─────────────────────┐  │                 │  ┌─────────────────────┐  │
       │  │ #world (Preserve 3D)│  │                 │  │ 28 Photo Figures    │  │
       │  │  ├─ #particles      │  │                 │  │ with Hover Captions │  │
       │  │  ├─ #orb (28 Cards) │  │                 │  └─────────────────────┘  │
       │  │  └─ #headline       │  │                 └───────────────────────────┘
       │  └─────────────────────┘  │                               ▲
       └─────────────┬─────────────┘                               │
                     │                                             │
                     └──────────────────────┬──────────────────────┘
                                            ▼
                             ┌───────────────────────────┐
                             │    FLIP Lightbox (#lit)   │
                             │  - High-res Image Preview │
                             │  - Memory Story & Date    │
                             │  - Close (ESC / Button)   │
                             └───────────────────────────┘
```

---

## 4. Implementation Steps

1. **Photo Cataloging & Integration**:
   - Map all 28 uploaded images from `/public/assets/aistudio/...` with titles, dates, and locations (e.g., Banagram School life, festive celebrations, outdoor portraits, pet moments).
   - Set Morium's best portrait as the avatar in `.bio`.
2. **Metadata & Branding**:
   - Update `metadata.json`, `<title>`, and meta description to Morium Khatun.
   - Update wordmark, photographer bio, and footer colophon to reflect her school and class details.
3. **Animation Enhancements**:
   - Add a subtle canvas particle star/dust layer that rotates in depth.
   - Add 3D card tilt physics on pointer hover (`transform: perspective(600px) rotateX(...) rotateY(...)`).
   - Add gentle idle orbit drift when no drag occurs for 3 seconds.
4. **Client-Side Photo Uploader**:
   - Add a clean "Add Photo" button in the menu and grid toolbar.
   - Support drag-and-drop or file picker, generating instant local Blob previews that seamlessly insert into both the 3D sphere and grid view.
5. **Verification**: Run `compile_applet` and `lint_applet` to ensure zero compilation or syntax errors.
