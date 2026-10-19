# Sider Fullscreen Reproduction Test

A minimal reproduction page for investigating an issue where the Sider AI assistant's floating UI becomes unavailable or invisible when a webpage enters browser fullscreen.

## Purpose

This repository provides a simple, standalone webpage that uses the standard browser Fullscreen API.

The goal is to reproduce the following behavior:

> Sider's floating interface is visible while the webpage is in normal windowed mode, but becomes unavailable/invisible after the webpage enters fullscreen. When fullscreen is exited, the Sider interface becomes available again.

This page does **not** modify, detect, or interfere with Sider. It simply provides a controlled webpage on which the behavior can be tested.

---

## Live Test Page

After enabling GitHub Pages, the test page will be available at:

```text
https://YOUR-USERNAME.github.io/sider-fullscreen-test/
```

Replace `YOUR-USERNAME` with the GitHub username that owns this repository.

---

## How to Reproduce

### 1. Open the test page

Open the GitHub Pages URL directly in Google Chrome.

Do not use the GitHub editor or repository preview.

### 2. Open Sider

Open the Sider AI assistant normally and verify that its floating interface is visible.

### 3. Start a screen recording

Start recording the browser window so the complete behavior can be observed.

### 4. Enter fullscreen

On the test page, click:

```text
⛶ Enter Fullscreen
```

The page will request fullscreen using:

```javascript
document.documentElement.requestFullscreen();
```

### 5. Check Sider

While fullscreen is active, check whether:

- Sider's floating button disappears
- Sider's floating interface becomes inaccessible
- Sider's UI cannot be opened
- Other Sider UI behavior changes

### 6. Exit fullscreen

Use the page's:

```text
✕ Exit Fullscreen
```

button or press `Esc`.

### 7. Check Sider again

Verify whether the Sider interface immediately becomes visible/usable again.

---

## Expected Behavior

Sider's interface should remain available while the webpage is fullscreen, assuming the browser and extension permit extension UI to remain visible during fullscreen.

## Observed Behavior

On the affected setup:

```text
Normal webpage
      ↓
Sider UI visible
      ↓
Enter browser fullscreen
      ↓
Sider UI becomes unavailable/invisible
      ↓
Exit fullscreen
      ↓
Sider UI becomes available again
```

---

## Technical Details

The page is intentionally minimal.

It uses the browser's standard Fullscreen API:

```javascript
document.documentElement.requestFullscreen();
```

and:

```javascript
document.exitFullscreen();
```

The page also listens for:

```javascript
document.addEventListener(
    "fullscreenchange",
    ...
);
```

to report the current fullscreen state.

No Sider-specific JavaScript is included in the page.

No attempt is made to access or manipulate Sider's DOM, Shadow DOM, extension APIs, or injected elements.

---

## Diagnostics

The page displays:

- Fullscreen API state
- Current fullscreen element
- Browser viewport dimensions
- Browser name
- Fullscreen event log

This information is intended to make the reproduction easier to investigate.

---

## Repository Structure

```text
sider-fullscreen-test/
│
├── index.html
└── README.md
```

The entire test page is contained in `index.html`.

No external JavaScript libraries or frameworks are required.

---

## Test Environment

Please record the following when reporting the issue:

- Operating system
- Browser and version
- Sider version
- Sider browser extension version
- Whether the browser is Chrome, Edge, etc.
- Whether the issue occurs in a normal browser window
- Whether the issue occurs only after entering fullscreen

Example:

```text
OS: Windows 11
Browser: Google Chrome
Sider version: [version]
Sider extension version: [version]
Fullscreen API: Enabled
```

---

## Screen Recording

A screen recording should ideally show:

1. The test page in normal mode
2. Sider visible
3. Clicking "Enter Fullscreen"
4. Sider becoming unavailable/invisible
5. Clicking "Exit Fullscreen"
6. Sider becoming available again

This provides a complete reproduction sequence.

---

## Notes for Investigation

The important point is that the issue is reproducible on a standalone HTTPS webpage using the browser's native Fullscreen API.

The page does not implement any fullscreen restrictions itself beyond calling the standard API.

The purpose of this repository is therefore to provide Sider's developers with a controlled environment for investigating how the browser's fullscreen rendering context interacts with Sider's injected/floating UI.

---

## License

This repository is provided solely as a technical reproduction case for debugging and investigation.
