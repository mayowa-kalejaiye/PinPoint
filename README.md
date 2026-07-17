<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/c175b61c-aed5-4a2a-8e13-f23a6741fa46" />


<img width="567" height="272" alt="image" src="https://github.com/user-attachments/assets/0d196e89-da6e-4c36-931b-8c83ab332b0c" />

_comments from LinkedIn, shared with thanks_

Linkedin Post: https://www.linkedin.com/posts/mayowa-kalejaiye_so-i-built-a-painkiller-for-nigerian-addresses-ugcPost-7445115089243762688-mAix/?utm_source=social_share_send&utm_medium=member_desktop_web&rcm=ACoAAE0lc38B0a5-G-fzx5ImUtRXYJGbp_5LJss


# PinPoint

PinPoint is a lightweight, single-file (HTML/JS/CSS) pick-up location app designed for quick driver/customer coordination.

- Customer selects destination with map pin
- Landmark photo upload + share link generation
- Driver real-time tracking with route and badges
- Works on mobile browsers (iOS/Android), optimized for low friction

---

## 🌟 Features

### Customer path

- Step 1: Location selection
  - map drag pin
  - search address (Nominatim)
  - "Use current location" button
  - persistent search history
  - collapsible bottom sheet (toggle arrow) with saved state

- Step 2: Landmark photo
  - upload/choose image from local mobile camera/gallery
  - photo preview
  - photo is encoded and preserved in share URL (`pb` parameter)

- Step 3+: Share link
  - dynamic share URL includes encoded coordinates, name, photo
  - copy to clipboard / WhatsApp / generic link


### Driver path

- `?m=drv` mode accepts query params or session history
- location permission auto-request + explicit re-request button
- permissions badge with query API (`navigator.permissions.query`) and status updates
- toast alerts for permission/grant/denial/timeouts
- driver marker sync pushes to central sync mechanism
- customer sees driver car marker movement


### Map + route UX

- All UI overlays set with high `z-index` to avoid being hidden by Leaflet map
- "Calculating route" overlay always visible
- Top badges (ETA/route status) are above map panes


## 🧩 Architecture

`index.html` contains:

- DOM views: `s1` (customer map), `s-drv` (driver view), plus step sheets
- State object: `ST` stores lat/lng, address, photo keys, route state
- Map handlers: `initMap`, `geo`, `toLm`, pin confirm flow
- Search/locate: `searchAddress`, `useCurrentLocation`, history in `localStorage`
- Driver geo: `watchDrv`, `requestDriverLocation`, `onDrvPos`, `Sync.push`
- Draggable sheet control: `sheetToggle` interaction + persistent collapse state
- Toastr: `showToast` for short message/feedback


## 🛠️ Setup & run

No build is required. Simply open `index.html` in a browser.

### Recommendation

- Deploy as a static site on any host (GitHub Pages, Netlify, Apache, nginx)
- Prefer HTTPS for geolocation permissions
- Enable cross-device sharing (copy or WhatsApp)


## 🔑 Config

In `index.html`, optional variables:

- `OPEN_CAGE_KEY` (string, empty by default) for better geocoding fallback
- `ST` status and debug keys stored in `localStorage`, e.g. `pinpoint_s1_collapsed`


## 🧪 Test flow (manual)

1. Customer mode: open app, enter location, search address, or use GPS
2. Confirm and add landmark photo
3. Share generated URL with driver
4. Driver mode: open link, grant location permissions, watch the car marker move
5. Customer map should update with driver position and route status


## 🩹 Troubleshooting

- iOS location denied: must enable `Location Services` for browser in iOS Settings
- GPS stale: use `Use current location` and refresh
- Generic `Ifako/Ijaye` geocoder: use exact address search input


## 📌 Next enhancements

- Additional geocoder providers (OpenCage/Google) as a fallback
- Live WebSocket-driven updates instead of polling URL/shared state
- Multi-stop driver route/ETA improvements
- Server-backed persistence for photo and trip records

---

## 👋 License

MIT-like: use and adapt freely. No guarantees.
