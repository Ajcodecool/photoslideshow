# Pi Dashboard Pro + Live Chat (Uhale Frame Edition)

A highly optimized, lightweight web dashboard designed specifically for legacy Android digital photo frames. This project provides a beautiful background slideshow, live clock, local weather, sleep/wake scheduling, and a live chat widget connected to a Supabase backend.

![Dashboard Preview](https://via.placeholder.com/800x450.png?text=Dashboard+Preview) ## ⚠️ Hardware Context & Compatibility

This dashboard was precision-engineered to run on the **Uhale Digital Photo Frame** running **Android 6.0 (Marshmallow)**. 

Under the hood, these frames are powered by the **Rockchip RK3066**, a dual-core processor originally released in **2012**. The RK3066 is an incredibly low-powered chip that was historically used in early budget electronics, such as:
* Early Android TV sticks (e.g., the popular MK808)
* First-generation budget tablets (e.g., HP Slate 7)
* Retro gaming handheld emulators
* Basic digital signage players

Because Android 6 relies on a severely outdated WebView (Chrome ~44), modern web technologies will instantly crash the device. **This project is written strictly in ES5 JavaScript** and bypasses heavy modern libraries to ensure a buttery smooth experience without causing memory overflow or CPU bottlenecking on the RK3066.

## ✨ Features

* **Live Weather & Clock:** Fetches real-time temperature and conditions via the Open-Meteo API.
* **Ken Burns Slideshow:** A rotating background photo gallery with hardware-accelerated CSS transitions (Fade, Slide, Zoom) that won't tax the CPU.
* **Live Chat Widget:** Displays the last 5 messages from a custom React/Supabase project.
* **Night Mode Scheduler:** Automatically turns the screen black during user-defined sleep hours to save power and reduce glare in dark rooms.
* **On-Screen Settings Panel:** Tap the background to access transition controls and manual night-mode overrides.

## 🛠️ Technical Implementation for Legacy Hardware

To prevent the RK3066 processor from freezing, several specific architectural choices were made:
1. **Zero Modern Syntax:** No `const`, `let`, `async/await`, template literals, or arrow functions. The entire codebase is written in ES5 to prevent Android 6 parsing errors.
2. **No Heavy SDKs:** The official Supabase JavaScript SDK was removed. It is too heavy for this processor and causes the page to crash on load.
3. **REST Polling over WebSockets:** Persistent WebSocket connections (used for real-time database listening) easily exhaust the memory limits of this device. Instead, the dashboard uses legacy `XMLHttpRequest` polling to fetch the 5 newest chat messages every 10 seconds.

## 🚀 Setup & Installation

### 1. Configure Credentials
Before deploying, open the `index.html` file and locate the API credentials section. Add your Supabase (or custom API) URL and Anon Key.

```javascript
// Replace these with your actual Supabase / API credentials
var PI_URL = '[https://your-api-url.com](https://your-api-url.com)';
var PI_KEY = 'your-anon-jwt-key-here';
