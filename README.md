MiniWeb

Write websites in simple words.

A tiny, browser-based website builder that turns plain English-like commands into real HTML — with a live preview, multi-page routing, and one-click export. No install. No build step. No backend.


TABLE OF CONTENTS

- What is MiniWeb?
- Why
- Features
- Quick start
- The language
  - Page setup
  - Creating elements
  - Styling by id
  - Layout
  - Effects
  - Actions
  - Multiple pages
- The editor
- Settings
- Files and folders
- Sharing and exporting
- How it works
- Keyboard shortcuts
- Project structure
- Running locally
- Deploying to GitHub Pages
- Browser support
- Roadmap
- FAQ
- Contributing
- Credits
- License


WHAT IS MINIWEB?

MiniWeb is a mini language for building front-end web pages, plus a self-contained editor that runs entirely in your browser.

You write things like this:

    page "My Site"
    background #f3f5f9

    heading =title1 "Hello, world!"
    position =title1 center
    color =title1 #2f6fed
    size =title1 44

    button =btn1 "Click me"
    bg =btn1 #2f6fed
    color =btn1 white
    radius =btn1 10

    click =btn1 -> set =title1 "You clicked it!"

...and MiniWeb turns it into a real, working site.html you can open anywhere.

There is no framework, no bundler, and no server. One HTML file, running in your browser, compiles your code in real time.


WHY

Writing a website today usually means juggling four languages (HTML, CSS, JavaScript, and often a framework) before you see anything on screen. For a beginner, that's a lot of ceremony just to center a heading.

MiniWeb starts from a different angle: what if a website were described in the same words you'd use to explain it out loud?

"Put a heading at the top, center it, make it big and blue. Add a button under it. When the button is clicked, change the heading."

That's exactly what MiniWeb code looks like:

    heading =title1 "Hello"
    position =title1 center
    size =title1 44
    color =title1 blue

    button =btn1 "Click me"
    click =btn1 -> set =title1 "Clicked!"

MiniWeb is designed for:

- Beginners learning how a web page is put together, without drowning in syntax
- Teachers who want a fast way to introduce the web without setting up tooling
- Prototypers who want a mock page in 30 seconds without opening a real editor
- Tinkerers who want to understand how a mini-language compiles to HTML

It is not trying to replace professional web development. It's a friendly doorway into it — and everything you build can be exported as normal HTML.


FEATURES

- Live preview — the right panel updates as you type. What you see is what you get.
- Multi-file projects — as many pages as you want, plus .css and .js files that are injected into every page.
- Explorer with folders — real nested folders in the sidebar. Create, delete, collapse.
- Multi-page routing — link =nav1 "About" -> about navigates between .miniweb files.
- Autocomplete — keywords, style properties, action verbs, and every =id you've already defined, suggested as you type.
- Click-to-inspect — click any element in the preview and the editor jumps to the line that made it.
- Responsive preview — toggle between phone (375px), tablet (768px), and desktop widths.
- Syntax highlighting — colors for keywords, strings, properties, ids, numbers, and arrows.
- Line numbers with red highlighting on lines that have errors.
- Problems panel — a list of everything MiniWeb couldn't parse, with click-to-jump.
- Copy HTML, Export .html, and Share link (the whole project encoded into a URL hash).
- Auto-save to localStorage, plus a settings page you can customize.
- Built-in guide — the whole language documented in the app itself.
- No backend, no account, no tracking. Everything happens on your machine.


QUICK START

Use the hosted version

Open the live site in your browser. The default project loads automatically. Start editing the code on the left; the preview updates on the right.

Or run it yourself

1. Download index.html.
2. Open it by double-clicking — no server needed.
3. Start editing.

That's it.


THE LANGUAGE

MiniWeb is line-based. Each line does one thing. Blank lines are ignored. Lines starting with # or // are comments.

Page setup

Set the browser tab title and the page background.

    page "My Site"
    background #f3f5f9

- page "..." — the <title> of the document. One per file.
- background <color> — background color of the whole page. Accepts any CSS color value (names, hex, rgb(), etc.).

Creating elements

Every element has a type, a name (its id, prefixed with =), and optional content in quotes.

    heading =title1 "Hello"
    text    =text1  "Some words"
    button  =btn1   "Click me"
    box     =box1   "content"
    image   =pic1   "cat.png"
    input   =in1    "type here"
    link    =nav1   "About" -> about

Type     | Renders as | Notes
---------|------------|------------------------------------
heading  | <h1>       | Big title text
text     | <p>        | Paragraph
button   | <button>   | Clickable button
box      | <div>      | Container for grouping
image    | <img>      | Content is the image URL
input    | <input>    | Content is the placeholder
link     | <a>        | Extra -> route makes it a page link

The id is what you use to style and act on the element. Use any name you like — =title1, =myheading, =hero_text, =nav_home.

Styling by id

Style commands take the form:

    <property> =<id> <value>

For example:

    color =title1 red
    size =title1 44
    position =title1 center

Numbers (like 44, 20, 1.5) are automatically turned into pixels for size-related properties. Other values pass through as-is.

Colors

    color    =text1 red
    bg       =text1 #2f6fed
    color    =text1 rgb(255, 100, 0)
    bg       =body  #f3f5f9

Target =body or =page to style the whole document.

Typography

    size      =text1 18
    font      =text1 Arial
    bold      =text1 yes
    italic    =text1
    underline =text1
    upper     =text1
    lower     =text1
    spacing   =text1 2
    leading   =text1 1.6

Box

    padding  =text1 20
    margin   =text1 10
    width    =box1  300
    height   =box1  120
    border   =text1 2px solid black
    radius   =text1 12
    shadow   =box1  0 4px 12px gray
    opacity  =text1 0.5
    overflow =box1  hidden

Position

    position =text1 center
    position =text1 left
    position =text1 right
    z        =box1  10

Layout

    display =box1 grid
    flex    =box1 row
    flex    =box1 column
    align   =box1 center
    justify =box1 space-between
    gap     =box1 20
    columns =box1 3
    nowrap  =text1

- flex row / flex column — set flex direction
- align — vertical alignment (CSS align-items)
- justify — horizontal alignment (CSS justify-content)
- columns 3 — a grid with 3 equal columns
- nowrap — prevent the element from wrapping

Effects

    rotate     =box1 45
    scale      =box1 1.2
    transition =box1 all .2s
    cursor     =btn1 pointer

Actions

Actions attach behavior to elements. The syntax is:

    click =<id> -> <action>
    hover =<id> -> <action>

Available actions

Action    | Example               | What it does
----------|-----------------------|---------------------------------
Set text  | set =text1 "New!"     | Replace the element's text
Hide      | hide =text1           | Set display: none
Show      | show =text1           | Remove display: none
Toggle    | toggle =text1         | Flip visibility
Alert     | alert "Hi!"           | Show a browser popup
Any style | color =text1 blue     | Change a style live

You can chain several by writing several lines:

    click =btn1 -> color =text1 green
    click =btn1 -> set =text1 "You clicked it!"
    click =btn1 -> scale =btn1 1.1

Each line attaches another listener to the same element.

Multiple pages

Every .miniweb file is its own page. The name of the file (minus the extension) is the route.

about.miniweb is reachable at route about. index.miniweb is the default when nothing else matches.

Link between pages with link:

    link =nav1 "About" -> about
    link =back "Home" -> index

The preview navigates between pages live — no reload, no server.


THE EDITOR

MiniWeb ships with a full editing environment.

Explorer

The left sidebar (opened by the folder icon in the activity bar) shows your project as a file tree.

- + creates a new file
- The folder icon creates a new folder
- Hover a row and click x to delete it
- Click a folder's chevron to collapse it
- Click a file to open it in a tab

Tabs

Every file you've opened appears as a tab. The active tab shows a colored bar at the top.

Editor

A code editor with:

- Syntax highlighting — comments in green, strings in orange, keywords in blue, style properties in yellow, ids in light blue, numbers in green, arrows in pink
- Line numbers on the left. Lines with errors turn red.
- Automatic indentation with the Tab key (configurable in Settings)
- Auto-save every ~500ms
- Auto-run of the preview every ~300ms

Autocomplete

As you type, MiniWeb suggests:

- Keywords — page, heading, text, button, box, image, input, link, click, hover, background
- Style properties — color, bg, size, padding, and everything else in the language
- Action verbs — set, hide, show, toggle, alert
- Every id you've already defined — as soon as you write =title1, future typing of title will suggest =title1

Navigate with up/down arrows, accept with Enter or Tab, close with Esc.

Problems panel

Below the editor is a problems panel. Every line MiniWeb can't parse shows up here with its line number.

Click any problem to jump to and select that line in the editor.

Right panel

The right side of the screen is a multi-tab panel:

- Preview — live render of your active page in a sandboxed iframe
- HTML — the full compiled HTML, with a Copy button and a Download button
- Guide — the complete language reference, formatted
- Settings — editor and preview preferences

Above the preview there are:

- Device toggles — Phone (375px), Tablet (768px), Desktop
- Inspect — a crosshair mode. Click any element in the preview and the editor jumps to the line that created it.
- Reload — rebuild the preview

Status bar

The blue bar at the bottom shows:

- Current status (Ready or N problems)
- Cursor position (Ln 12, Col 4)
- Save indicator (flashes green when saved)


SETTINGS

Open the right panel, Settings tab, to configure:

Setting       | Default  | Description
--------------|----------|--------------------------------
Font size     | 13.5px   | Editor text size
Tab size      | 2 spaces | Spaces inserted by Tab
Auto-run      | on       | Rebuild the preview as you type
Auto-save     | on       | Persist to localStorage
Line numbers  | on       | Show the gutter
Word wrap     | off      | Wrap long lines

Settings are saved separately from your project, so resetting one doesn't lose the other.

There's also a Wipe all data button at the bottom of the Settings pane that clears both project and settings from the browser.


FILES AND FOLDERS

A MiniWeb project is a flat map of paths to file contents. Folders exist implicitly — any path with a / in it creates the folders along the way.

The three file types:

Extension  | Purpose
-----------|-----------------------------------------------------------
.miniweb   | A page. Each one becomes a route.
.css       | Extra CSS. Injected into every page.
.js        | Extra JavaScript. Injected into every page, before generated actions.

Example structure:

    index.miniweb
    about.miniweb
    contact.miniweb
    styles.css
    script.js
    pages/pricing.miniweb

All .css and .js files apply globally, so you can put shared styles or a helper library there.


SHARING AND EXPORTING

Copy HTML

Copies the compiled HTML of the current preview page to your clipboard. Paste it into any .html file and it works standalone.

Two buttons do this:

- Title bar, Copy HTML
- HTML pane, Copy

Export

Downloads the compiled HTML as a file named after the active route (e.g. about.html).

Share link

Click Share in the title bar. MiniWeb encodes the entire project (all files) into a base64 string and puts it in the URL hash.

Anyone who opens that link gets your whole project loaded. No server, no account — the data is in the URL itself.

Note: Very large projects produce very long URLs. Browsers handle up to about 64,000 characters, but some chat apps will mangle anything over a few thousand. If the link is huge, MiniWeb asks for confirmation.


HOW IT WORKS

MiniWeb is a small compiler plus a code editor, both written in vanilla JavaScript.

    .miniweb source
          |
          v
       Parser (lines)
          |
          v
      Generator (HTML/CSS)
          |
          v
       iframe live preview

1. Parse — each line is matched against a small set of patterns:
   - page "..." sets the title
   - background <color> sets the body background
   - <type> =<id> "<content>" adds an element
   - <action> =<id> -> <something> adds an event listener
   - <property> =<id> <value> adds a style rule
   - anything else is recorded as an error

2. Generate — the parsed program is turned into a full HTML document:
   - A base stylesheet gives sane defaults
   - Style rules are grouped by id and emitted as #id { ... }
   - Elements are emitted as real HTML tags with id and data-mw-id attributes
   - Actions are emitted as addEventListener calls
   - Optional .css and .js files are concatenated in

3. Render — the compiled HTML is put into a sandboxed iframe srcdoc, which runs it as its own document.

4. Communicate — the iframe posts messages back to the parent for nav (page changes from <a> clicks) and inspect (element clicks in inspect mode).

The whole app is one file because it doesn't need a build step. The parser, generator, editor, tree, and preview all live in the same script block.


KEYBOARD SHORTCUTS

Shortcut              | Action
----------------------|------------------------
Ctrl / Cmd + Enter    | Run the preview
Ctrl / Cmd + S        | Save the project
Ctrl / Cmd + B        | Toggle the sidebar
Tab                   | Insert spaces
Up / Down arrows      | Navigate autocomplete
Enter / Tab           | Accept autocomplete
Esc                   | Close autocomplete


PROJECT STRUCTURE

    nardjaywebbuilder2/
    ├── index.html      The entire app — parser, editor, preview, all of it
    ├── README.md       This file
    ├── LICENSE         MIT
    ├── screenshot.png  (optional) preview image for the README
    └── .gitignore

There is no package.json, no node_modules, no build script.


RUNNING LOCALLY

Just open the file:

    open index.html          (macOS)
    start index.html         (Windows)
    xdg-open index.html      (Linux)

Or serve it with any static server if you prefer:

    python3 -m http.server 8000
    then open http://localhost:8000

Both work. Serving is recommended for the Share-link feature, because some browsers treat file:// URLs differently for clipboard operations.


DEPLOYING TO GITHUB PAGES

1. Rename the app file to index.html (it likely already is).
2. Push the repo to GitHub.
3. Go to Settings, then Pages.
4. Set Source to Deploy from a branch.
5. Choose branch main and folder /root.
6. Save.

After about 30 seconds, your site is live at:

    https://nardjay.github.io/nardjaywebbuilder2/

Works the same on Netlify, Vercel, Cloudflare Pages, or any static host — just drag the folder in.


BROWSER SUPPORT

MiniWeb uses modern browser features and works in:

- Chrome / Edge 90+
- Firefox 88+
- Safari 15+
- Any Chromium-based browser (Brave, Arc, Opera)

Older browsers may have issues with dialog, clipboard.writeText, and ES2020 syntax.


ROADMAP

Things that are planned or under discussion. Contributions welcome.

[ ] CSS and JS syntax highlighting — currently .css and .js files use the MiniWeb highlighter, which is wrong
[ ] Rename files by double-clicking a tree row
[ ] Drag to reorder files and tabs
[ ] Duplicate file button
[ ] Close tabs with Ctrl+W
[ ] Templates menu — Portfolio, Landing, Blog card, Contact form
[ ] Editor themes — Monokai, Dracula, Solarized
[ ] Variables — let maincolor = #2f6fed, then color =text1 maincolor
[ ] Loops — repeat 3 { text =item "hi" }
[ ] Nested element targets — put an element inside a box by id
[ ] Export as a zip with all files
[ ] Import a project from a zip or a JSON file
[ ] Live element highlight while hovering in inspect mode

If you want one of these, open an issue — it helps to know what people actually want.


FAQ

Is MiniWeb a replacement for HTML?
No. It's a friendly front door. If you want full control, export the HTML and keep going in a real editor. MiniWeb's output is normal, standards-compliant HTML.

Does MiniWeb need a server?
No. It runs entirely in your browser. The only reason to run a server is to make Share links play nicely with clipboard APIs.

Where is my project stored?
In your browser's localStorage, under the key miniweb:project:v4. Clearing site data wipes it. Use Export or Share to back it up.

Can other people edit my project?
Yes — send them a Share link. Anyone who opens it gets your project in their browser.

Can I use MiniWeb to build a real site?
Absolutely. Export the HTML, open it in a real editor, and use it as a starting point. Some people use MiniWeb for prototypes and mockups instead.

Is there a backend?
No. MiniWeb is a pure front-end tool. There is no server, no account, no telemetry, no network requests. What happens in your browser stays in your browser.

Why one giant file?
So it works as a single double-click. No build, no install, no npm install. If you want to fork it into a modular project, the code is organized in clearly labeled sections — go for it.

Does it support images?
Yes — image =pic1 "https://example.com/cat.png" renders an <img> with that source. Local paths work if the file is accessible to the page.


CONTRIBUTING

Contributions are welcome. Here's the short version:

1. Fork the repo.
2. Make a change. Any size is fine — a bug fix, a new style property, a doc fix.
3. Test it. Open the file in a browser. Click around. Make sure the preview works.
4. Open a pull request. Explain what you changed and why.

Some guidelines:

- Keep the app a single HTML file. It's a feature, not an accident.
- No dependencies. No frameworks, no bundlers, no CDN scripts. Vanilla JS only.
- Match the existing style. Two-space indent, single quotes, semicolons.
- Comment the tricky bits. The parser especially.
- Add to the Guide. If you add a language feature, add a row to GUIDE_DATA so it shows up in the built-in docs.

If you're not sure where to start, look for issues labeled good first issue or help wanted.

Reporting bugs

When filing an issue, include:

- What you did
- What you expected
- What actually happened
- Your browser and OS
- A snippet of the MiniWeb code that triggered it, if possible


CREDITS

Author

nardjay — creator and maintainer
GitHub: @nardjay

Built with

- Vanilla JavaScript — no framework, no bundler, no build step
- The browser itself — the parser, the editor, the preview, the sandboxed iframe, and localStorage are the entire runtime
- CSS Grid and Flexbox — for the entire editor layout
- The humble textarea — doing the hard work under a transparent overlay

Inspired by

MiniWeb borrows its spirit from several places:

- HTML and CSS themselves — the original declarative mini-languages of the web
- Markdown — proving that plain words can beat angle brackets
- Scratch and Blockly — showing that programming can be a first language, not a last one
- HyperCard — the original "one file, one stack, everything works" tool
- JSFiddle, CodePen, and StackBlitz — the idea that writing code in a browser, with a preview next to it, is the right default
- VS Code — for the editor chrome: activity bar, explorer, tabs, status bar, problems panel

Thanks

- To the web platform for shipping an iframe srcdoc attribute that lets one file host another file safely
- To everyone who has ever used a textarea as an editor and discovered that a transparent one behind a pre is a surprisingly great way to build a code editor in 40 lines
- To the open-source community for the tools this project doesn't need but is glad exists

Third-party assets

None. No fonts, no icon packs, no CSS frameworks, no libraries, no CDN scripts.

The traffic-light dots in the title bar are divs with border-radius: 50%. The file icons are Unicode characters. The buttons are Unicode glyphs and inline SVG. That's it.


LICENSE

Released under the MIT License.

You're free to use, modify, and distribute MiniWeb, including for commercial purposes. Attribution is appreciated but not required. See the LICENSE file for the full text.


Built with vanilla JavaScript and a lot of textarea.

If MiniWeb helped you, consider giving the repo a star — it helps other people find it.
