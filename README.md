2BOS-OB-SIGNAL-BOT/
├── _redirects
├── index.html
├── app.js
├── manifest.json
├── sw.js
├── netlify.toml
└── icons/
    ├── icon-192x192.png
    └── icon-512x512.png
    /*    /index.html   200
    <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="theme-color" content="#121212" />
  <title>2BOS = MSS Signal Viewer</title>
  <link rel="manifest" href="manifest.json" />
</head>
<body>
  <div id="app">
    <p>Loading signals…</p>
  </div>
  <script src="app.js"></script>
</body>
</html>
// app.js
// Connect to your WebSocket signal server and render cards inside #app

const ws = new WebSocket('wss://YOUR_BACKEND_SERVER');
const app = document.getElementById('app');

ws.onmessage = ({ data }) => {
  const sig = JSON.parse(data);
  app.innerHTML = `
    <div class="signal-card">
      <h2>${sig.pair} — <span class="${sig.direction.toLowerCase()}">${sig.direction}</span></h2>
      <p>Entry: ${sig.entry}</p>
      <p>SL: ${sig.stopLoss}</p>
      <p>TP: ${sig.takeProfit}</p>
      <small>${new Date(sig.timestamp).toLocaleTimeString()}</small>
    </div>
  `;
};
{
  "name": "2BOS = MSS Signal Viewer",
  "short_name": "2BOS Signals",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#121212",
  "theme_color": "#121212",
  "icons": [
    { "src": "icons/icon-192x192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "icons/icon-512x512.png", "sizes": "512x512", "type": "image/png" }
  ]
}
const cacheName = '2bos-mss-v1';
const assets = [
  '/', '/index.html', '/app.js', '/manifest.json',
  '/icons/icon-192x192.png', '/icons/icon-512x512.png'
];

self.addEventListener('install', e =>
  e.waitUntil(caches.open(cacheName).then(c => c.addAll(assets)))
);

self.addEventListener('fetch', e => {
  e.respondWith(caches.match(e.request).then(r => r || fetch(e.request)));
});
[build]
  publish = "."
  command = ""

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
