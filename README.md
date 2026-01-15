# Wild Birds AR Trading Cards 🦅

**WebAR that works on iOS Safari + Android Chrome. No app store. No install. Just scan.**

---

## ⚡ 30-Second Summary

1. User scans a printed card with their phone camera
2. 3D bird appears floating above the card
3. Collect all 12 monthly birds!

**Tech:** MindAR (image tracking) + A-Frame (3D rendering) + vanilla HTML/JS

---

## 🎯 Quick Start (Get It Running)

### Step 1: Host It
Upload files to any HTTPS host.

> ⚠️ **MUST be HTTPS** - cameras don't work on HTTP

### Step 2: Test It
1. Open demo URL on your phone
2. Tap "Start AR Experience"
3. Point camera at this image (open on another screen or print it):

**Demo Target:** https://cdn.jsdelivr.net/gh/hiukim/mind-ar-js@1.2.5/examples/image-tracking/assets/card-example/card.png

---

## 🔧 Customization Cheatsheet

### Change the 3D Model

**Find this in the HTML:**
```html
<a-asset-item id="bird-model" src="YOUR_MODEL_URL_HERE.glb"></a-asset-item>
```

**Free GLB models:**
- [Sketchfab](https://sketchfab.com) (filter: downloadable)
- [Poly Pizza](https://poly.pizza)
- [Google Poly Archive](https://github.com/nicklockwood/Poly)

**Model tips:**
- GLB or GLTF format only
- Keep under 5MB for fast mobile loading
- Test in [gltf-viewer.donmccurdy.com](https://gltf-viewer.donmccurdy.com/)

---

### Create Your Own Target Image (Trading Card)

**Tool:** https://hiukim.github.io/mind-ar-js-doc/tools/compile

1. Upload your card artwork (PNG/JPG)
2. Click "Compile"
3. Download the `.mind` file
4. Host the `.mind` file somewhere (same place as your HTML)
5. Update the HTML:

```html
<a-scene mindar-image="imageTargetSrc: YOUR_FILE.mind; ...">
```

**Good target images have:**
- ✅ High contrast
- ✅ Lots of unique details
- ✅ No large solid color areas
- ✅ No repeating patterns
- ❌ NOT just text
- ❌ NOT blurry

---

### Adjust Model Position/Size/Animation

**Find the `<a-gltf-model>` tag:**

```html
<a-gltf-model 
    src="#bird-model"
    position="0 0.1 0.15"      <!-- X Y Z: 0=center, positive Y=up, positive Z=toward camera -->
    scale="0.4 0.4 0.4"        <!-- make bigger: 1 1 1, smaller: 0.2 0.2 0.2 -->
    rotation="0 0 0"           <!-- degrees: X-tilt, Y-spin, Z-roll -->
    animation="property: rotation; to: 0 360 0; dur: 8000; loop: true">  <!-- spin animation -->
</a-gltf-model>
```

**Common tweaks:**

| Want this? | Change this |
|------------|-------------|
| Bigger model | `scale="1 1 1"` |
| Higher above card | `position="0 0.3 0.15"` (increase Y) |
| Spin faster | `dur: 4000` (milliseconds) |
| No spin | Delete the `animation` line |
| Face camera | `rotation="-90 0 0"` |

---

### Change Colors/Branding

**Key CSS variables to find/replace:**

| Color | What it styles |
|-------|----------------|
| `#4ade80` | Primary green (buttons, accents) |
| `#22c55e` | Secondary green (gradients) |
| `#1a3a2a` | Dark green (backgrounds) |
| `#0d1117` | Near-black (page background) |

**Quick rebrand:** Find & replace `#4ade80` with your brand color.

---

### Add Multiple Cards/Birds

**In `<a-assets>`, add more models:**
```html
<a-asset-item id="bird-january" src="hawk.glb"></a-asset-item>
<a-asset-item id="bird-february" src="cardinal.glb"></a-asset-item>
<a-asset-item id="bird-march" src="bluejay.glb"></a-asset-item>
```

**For multiple target images in one experience:**

1. Compile all card images together (upload multiple to the compiler)
2. Add multiple `<a-entity mindar-image-target>` blocks:

```html
<a-entity mindar-image-target="targetIndex: 0">
    <a-gltf-model src="#bird-january"></a-gltf-model>
</a-entity>

<a-entity mindar-image-target="targetIndex: 1">
    <a-gltf-model src="#bird-february"></a-gltf-model>
</a-entity>
```

---

## 📁 File Structure

```
wild-birds-ar/
├── index.html          # Simple demo
├── wild-birds-demo.html # Branded full demo
├── targets/
│   └── card.mind       # Compiled target image data
└── models/
    └── bird.glb        # 3D model file
```

---

## 🐛 Troubleshooting

| Problem | Fix |
|---------|-----|
| Camera won't start | Must be HTTPS, not HTTP |
| Model not appearing | Check browser console (F12) for 404 errors |
| Tracking is jittery | Print target larger, better lighting |
| iOS Safari not working | Make sure you granted camera permission |
| Model is huge/tiny | Adjust `scale` values |
| Model is underground | Increase Y in `position` |

---

## 🔗 Resources

- **MindAR Docs:** https://hiukim.github.io/mind-ar-js-doc/
- **A-Frame Docs:** https://aframe.io/docs/
- **Target Compiler:** https://hiukim.github.io/mind-ar-js-doc/tools/compile
- **GLB Viewer:** https://gltf-viewer.donmccurdy.com/
- **Free 3D Models:** https://poly.pizza

---

## ⚠️ Limitations

This uses **image tracking only** (not world tracking):

- ✅ Works when camera sees the card
- ❌ Content disappears when card leaves view  
- ❌ Can't place objects on floors/walls without a marker
- ❌ Can't do "walk around" AR experiences

For marker-free AR, you'd need world tracking (SLAM) which is experimental on iOS Safari. See: [AlvaAR](https://github.com/alanross/AlvaAR)

---

## 📱 Tested On

- ✅ iPhone (Safari)
- ✅ Android (Chrome)
- ✅ iPad (Safari)
- ✅ Desktop browsers (with webcam)

---

*Built with MindAR + A-Frame. No app store required.*
