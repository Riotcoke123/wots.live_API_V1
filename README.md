<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />

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

