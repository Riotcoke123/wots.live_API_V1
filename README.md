<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Livebeam Public API for wots.live</title>
  <style>
    :root {
      --bg: #0b0f13;
      --panel: #121821;
      --text: #e6edf3;
      --muted: #a9b5c1;
      --accent: #5b9cff;
      --border: #1f2a36;
      --code: #0e141b;
      --success: #22c55e;
      --warn: #f59e0b;
    }
    html, body { background: var(--bg); color: var(--text); font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", Arial, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", sans-serif; margin: 0; }
    .container { max-width: 980px; margin: 0 auto; padding: 48px 20px 80px; }
    h1, h2, h3 { line-height: 1.2; margin: 0 0 12px; }
    h1 { font-size: 2rem; }
    h2 { font-size: 1.35rem; margin-top: 36px; padding-top: 8px; border-top: 1px solid var(--border); }
    h3 { font-size: 1.05rem; margin-top: 24px; color: var(--muted); }
    p { margin: 0 0 12px; color: var(--muted); }
    a { color: var(--accent); text-decoration: none; }
    a:hover { text-decoration: underline; }
    .panel { background: var(--panel); border: 1px solid var(--border); border-radius: 14px; padding: 18px; margin: 16px 0; }
    .kvs { display: grid; grid-template-columns: 180px 1fr; gap: 10px 18px; }
    .kvs div { padding: 6px 0; }
    .tag { display: inline-block; font-size: 12px; padding: 2px 8px; border: 1px solid var(--border); border-radius: 999px; color: var(--muted); }
    code, pre { font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace; }
    pre { background: var(--code); border: 1px solid var(--border); border-radius: 10px; padding: 14px; overflow: auto; }
    .endpoint { display: grid; grid-template-columns: 180px 1fr; gap: 10px 18px; align-items: start; padding: 14px; border: 1px solid var(--border); border-radius: 12px; background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.0)); margin-bottom: 12px; }
    .method { font-weight: 700; }
    .GET { color: var(--accent); }
    .POST { color: var(--warn); }
    .status-note { display: inline-flex; align-items: center; gap: 8px; padding: 10px 12px; border: 1px dashed var(--border); border-radius: 12px; background: rgba(91,156,255,0.06); }
    .soon { color: var(--warn); font-weight: 600; }
    .ok { color: var(--success); font-weight: 600; }
    .mono { font-variant-ligatures: none; }
    .small { font-size: 0.92rem; color: var(--muted); }
  </style>
</head>
<body>
  <main class="container">
    <header>
      <h1>Livebeam Public API for wots.live</h1>
      <p>
        🔗 Website API: <a href="https://wots.live/" target="_blank" rel="noopener">https://wots.live/</a>
      </p>
      <div class="panel status-note">
        <span class="soon">Note:</span>
        <span class="small">Chat APIs are currently being refactored and are not yet available for external development. Once stabilized, we’ll enable bot integrations and publish full documentation.</span>
      </div>
    </header>
    <section>
      <h2>Base URL</h2>
      <pre><code class="mono">https://api.livebeam.live/api</code></pre>
    </section>
    <section>
      <h2>Response Envelope</h2>
      <p>All endpoints return JSON using a consistent envelope:</p>
      <pre><code>{
  "success": boolean,
  "data"?: any,
  "error"?: string
}</code></pre>
    </section>
    <section>
      <h2>General &amp; Channel Info</h2>
      <div class="endpoint">
        <div class="method GET">GET</div>
        <div>
          <div><code>/api/health</code></div>
          <p class="small">Returns overall service health, including Redis status.</p>
        </div>
      </div>
      <div class="endpoint">
        <div class="method GET">GET</div>
        <div>
          <div><code>/api/channel/:username</code></div>
          <p class="small">Resolves a username to its corresponding <code>channel_id</code>.</p>
        </div>
      </div>
      <div class="endpoint">
        <div class="method GET">GET</div>
        <div>
          <div><code>/api/follower-count/:channelId</code></div>
          <p class="small">Returns the total follower count for the specified channel.</p>
        </div>
      </div>

      <div class="endpoint">
        <div class="method POST">POST</div>
        <div>
          <div><code>/api/sidebar-data</code></div>
          <p class="small">Returns followed and recommended streams.</p>
          <div class="panel kvs">
            <div><span class="tag">Body</span></div>
            <div><code>user_id</code> (optional)</div>
          </div>
        </div>
      </div>
    </section>
    <section>
      <h2>Stream Status &amp; Playback</h2>

      <div class="endpoint">
        <div class="method GET">GET</div>
        <div>
          <div><code>/api/live-status/:channelName</code></div>
          <p class="small">Returns live/offline status, viewer count, and current title.</p>
        </div>
      </div>

      <div class="endpoint">
        <div class="method GET">GET</div>
        <div>
          <div><code>/api/get_livestream?channel_id=</code></div>
          <p class="small">Returns details for the current live stream.</p>
        </div>
      </div>
      <div class="endpoint">
        <div class="method GET">GET</div>
        <div>
          <div><code>/api/get-livestreams?channel_id=&amp;page=&amp;limit=</code></div>
          <p class="small">Returns a paginated list of past streams.</p>
          <div class="panel kvs">
            <div><span class="tag">Query</span></div>
            <div>
              <code>channel_id</code> (required) &nbsp;·&nbsp;
              <code>page</code> (optional, default <code>1</code>) &nbsp;·&nbsp;
              <code>limit</code> (optional, default <code>20</code>)
            </div>
          </div>
        </div>
      </div>
      <div class="endpoint">
        <div class="method GET">GET</div>
        <div>
          <div><code>/api/livepeer/playback/:playbackId</code></div>
          <p class="small">Returns Livepeer playback metadata.</p>
        </div>
      </div>
    </section>
    <section>
      <h2>Availability</h2>
      <p class="small">
        The endpoints above are production-ready for streamer information and general service data.
        Chat functionality is under active development; we will announce availability and provide integration guides once the refactor is complete.
      </p>
    </section>
  </main>
</body>
</html>

