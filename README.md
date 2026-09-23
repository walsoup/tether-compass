# Tether Compass 🧭

> A minimal compass for long-distance partners that tells you when you're facing each other, anywhere on Earth.

Tether Compass runs directly in your phone's browser. It reads your device heading and GPS coordinates, computes the great-circle bearing toward your partner, and lets you know when your paths align in real time.

---

## What It Does

- **Live Great-Circle Bearing**: Calculates the exact forward azimuth and distance between two geographic coordinates using spherical trigonometry.
- **Orientation Matching**: Uses your phone's digital magnetometer (`DeviceOrientationEvent`) to track which direction you are facing.
- **Facing Detection**: Highlights when you and your partner are looking directly toward each other along the curvature of the earth.
- **Private & Client-Side**: Coordinates stay in your browser session. No background tracking or account logins.

---

## Usage

1. Open the web app on your phone.
2. Grant permission for **Location** (GPS) and **Motion / Compass Sensors** when prompted by your browser.
3. Share your session link or enter your partner's coordinates.
4. Rotate your phone until the needle locks onto their heading.

---

## Technical Details

- **Device Orientation**: Uses the Web Sensor API and `deviceorientationabsolute` (with fallback to `webkitCompassHeading` on iOS Safari).
- **Geodesic Math**:
  - Distance: Haversine formula over WGS84 mean earth radius ($R \approx 6371\text{ km}$).
  - Bearing: Forward azimuth formula:
    $$\theta = \text{atan2}(\sin(\Delta \lambda) \cdot \cos(\varphi_2), \cos(\varphi_1) \cdot \sin(\varphi_2) - \sin(\varphi_1) \cdot \cos(\varphi_2) \cdot \cos(\Delta \lambda))$$
- **Stack**: Single-file static HTML5, CSS3, and vanilla modern JavaScript. Deployable to GitHub Pages, Netlify, or Vercel with zero build step.

---

## Running Locally

Because modern mobile browsers restrict sensor and geolocation access to secure contexts, serve the file over HTTPS or `localhost`:

```bash
# Clone the repository
git clone https://github.com/walsoup/tether-compass.git
cd tether-compass

# Run a local HTTP server
python3 -m http.server 8000
```

Open `http://localhost:8000` (or access via local Wi-Fi with an HTTPS tunnel like cloudflared/ngrok for mobile testing).

---

## License

[MIT License](LICENSE)
