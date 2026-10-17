# StoryCast

StoryCast is a small 3-page website for audio and video stories. I built it for my accessibility assignment. The main idea is that every story has captions and a full written transcript, so people who can't hear the video still get the whole story. I made it mainly for deaf and hard-of-hearing users, but it also helps anyone who watches with the sound off.

Only one story is finished (the video one). The other two cards on the home page are marked "Coming soon" because I didn't have time to record them.

## Links

- Research document: `docs/research.pdf` folder (PDF)
- Sitemap: `docs/sitemap.png` (see the file in that docs folder)
- Wireframes (Figma): "https://www.figma.com/design/0pYjVPr4esoHPLw3I5jV9P/Untitled?node-id=0-1&t=hZ38o0AUij032hmV-1"
- High-fidelity mockups (Figma): "https://www.figma.com/design/0pYjVPr4esoHPLw3I5jV9P/Untitled?node-id=0-1&t=hZ38o0AUij032hmV-1"

## Pages

| Page | File | What it has |
| --- | --- | --- |
| Home | `index.html` | Intro, a button to the first story, 3 featured story cards |
| Story | `story/story-1.html` | Video with captions, a transcript you can hide, related stories |
| About / Access | `about.html` | Why I made it, the accessibility features, how to use the site |

## Project structure

```
storycast/
├── index.html
├── about.html
├── story/
│   └── story-1.html
├── sass/
│   ├── main.scss
│   ├── _layers.scss
│   ├── _colors.scss
│   ├── _typography.scss
│   ├── _spacing.scss
│   ├── _base.scss
│   ├── _layout.scss
│   └── _components.scss
├── css/
│   └── main.css          (made by Sass)
├── assets/
│   ├── media/            (the video)
│   ├── transcripts/      (the captions file, .vtt)
│   └── images/           (cover photos)
├── docs/                 (research document PDF, sitemap)
├── package.json
└── README.md
```

## How I built it

- Plain HTML, Sass and a tiny bit of JavaScript. No frameworks.
- **Sass partials and tokens:** colours, fonts and spacing are variables in `_colors.scss`, `_typography.scss` and `_spacing.scss`. The other partials use them.
- **Cascade layers:** `_layers.scss` sets the order `reset, base, layout, components`. Each partial puts its styles in its own layer.
- **BEM class names:** for example `card`, `card__image`, `card__title` and `nav__link--current`.
- **Grid and Flexbox:** Grid is used for the story card list, the story page layout and the feature boxes. Flexbox is used for the header, the nav and the related stories column.
- **Container query:** each card sits in a `.card-box` wrapper. When that box is wide (40rem or more), the photo moves to the side of the text. When it is narrow, the photo goes on top. It reacts to the box, not the screen.
- **JavaScript:** only the show/hide button for the transcript, on the story page.

## Accessibility checklist

This is how I tried to meet WCAG 2.1 AA.

- [x] Semantic HTML: `header`, `nav`, `main`, `article`, `section`, `aside`, `figure`, `footer`
- [x] One `h1` per page, and headings go in order (h1, h2, h3)
- [x] `lang="en"` on every page
- [x] Skip link ("Skip to main content") is the first thing you reach with Tab
- [x] Video has a captions track (`<track kind="captions">` with a `.vtt` file)
- [x] Full transcript on the story page, and it can be hidden or shown
- [x] The transcript button uses `aria-expanded` so a screen reader knows if it is open
- [x] The current page link in the menu has `aria-current="page"`
- [x] `<figcaption>` describes what you can see in the video
- [x] Cover photos have empty `alt=""` because the card title next to them already says what the story is
- [x] Colour contrast: I checked every colour pair with a small script. The lowest one is 7.37:1, and the minimum for AA is 4.5:1
- [x] Visible focus outline (thick amber) on all links and buttons
- [x] Nothing autoplays
- [x] Layout works on small screens
- [ ] Tabbed through all 3 pages with only the keyboard (tick when done)
- [ ] Ran Lighthouse on all 3 pages (tick when done, add the scores below)
- [ ] Checked the page at 200% zoom (tick when done)

Lighthouse accessibility scores: Home __85_ , Story __89_ , About _92__

### Colours I used

| Name | Hex | Used for |
| --- | --- | --- |
| Background | `#0b1f3a` | page background |
| Text | `#f5f1e8` | main text |
| Accent | `#ffb547` | links, buttons, focus outline |
| Card | `#16315a` | cards and transcript box |
| Muted | `#c9d3e3` | smaller grey-blue text |

| Pair | Ratio |
| --- | --- |
| Text on background | 14.65 |
| Text on card | 11.49 |
| Accent on background | 9.40 |
| Accent on card | 7.37 |
| Muted on background | 10.94 |
| Muted on card | 8.58 |
| Background on accent (button text) | 9.40 |

## Run it locally

You need [Node.js](https://nodejs.org) installed.

1. Clone the repo and go into the folder:
```
   git clone https://github.com/CherishHub0/storycast.git
   cd storycast
```
2. Install Sass:
```
   npm install
```
3. Build the CSS once:
```
   npm run sass
```
   Or keep it watching for changes while you edit:
```
   npm run watch
```
4. Open `index.html` in your browser. If you use VS Code, the Live Server extension ("Go Live") works well too.

The compiled `css/main.css` is already in the repo, so the site also works if you just open `index.html` without running Sass.

## Known problems

- Only one story has a real video. The other two are "Coming soon" placeholders and don't link anywhere.
- There is no `<audio>` story yet, only the card for it.
- The captions were timed by hand against my own recording, so they may be a little off in places.
- The video file is fairly big, so it can load slowly on a bad connection.

## Credits

- Cover photos are from Unsplash. 
- Font: Atkinson Hyperlegible, by the Braille Institute, loaded from Google Fonts.
- Story and video: written and recorded by me.

## Help I had

I used Claude (an AI assistant) to help me plan the project, explain Sass, BEM and cascade layers, and write and debug the code. I tested everything in the browser myself and edited it to fit my project.