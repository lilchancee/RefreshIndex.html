# RefreshIndex.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>South Made Global: Live Campaign Matrix</title>
  <style>
    /* Base Style */
    body {
      margin: 0;
      font-family: 'Helvetica Neue', sans-serif;
      background: #121212;
      color: #f5f5f5;
    }

    /* Campaign Header */
    header {
      padding: 20px;
      background: #1b1b1b;
      text-align: center;
      font-size: 1.8em;
      font-weight: 700;
      letter-spacing: 1px;
      border-bottom: 2px solid #27ae60;
    }

    /* Responsive Grid */
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
      gap: 16px;
      padding: 20px;
    }

    /* Node Cards */
    .node-card {
      background: #222;
      padding: 16px;
      border-radius: 10px;
      text-align: center;
      transition: transform 0.3s ease, background 0.3s ease;
    }

    /* State-based Colors (Style Language) */
    .node-card.active { background: #2ecc71; }     /* Deep green for active */
    .node-card.redirect { background: #f1c40f; }   /* Swamp gold for redirect */
    .node-card.feedback { background: #3498db; }   /* Cool blue for feedback */
    .node-card.dormant { background: #7f8c8d; }    /* Smoke gray for dormant */

    /* Typography */
    .label {
      font-size: 1.2em;
      margin-bottom: 8px;
      font-weight: bold;
    }
    .behavior {
      font-style: italic;
    }

    /* Refresh Button */
    .refresh-btn {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      font-size: 1em;
      background: #27ae60;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    .refresh-btn:hover {
      background: #219150;
    }

    /* Mobile Scaling */
    @media (max-width: 600px) {
      header { font-size: 1.4em; padding: 15px; }
    }
  </style>
</head>
<body>
  <!-- Campaign Header -->
  <header>
    South Made Global: Live Campaign Matrix
  </header>

  <!-- Refresh Button -->
  <button class="refresh-btn" id="refreshButton">Refresh Matrix</button>

  <!-- Responsive Node Grid -->
  <div class="grid" id="nodeGrid"></div>

  <script>
    // Initial node configuration
    const nodes = {
      spotify: { state: 'active', behavior: 'amplify' },
      tiktok: { state: 'redirect', behavior: 'targetCrossover' },
      youtube: { state: 'feedback', behavior: 'analyzeComments' },
      soundcloud: { state: 'dormant', behavior: 'monitor' }
    };

    const grid = document.getElementById('nodeGrid');

    // Define possible states for simulation
    const possibleStates = ['active', 'redirect', 'feedback', 'dormant'];

    // Function to render the node cards based on current state
    function renderNodes() {
      grid.innerHTML = ''; // Clear grid content
      Object.entries(nodes).forEach(([platform, data]) => {
        const card = document.createElement('div');
        card.className = `node-card ${data.state}`;
        card.innerHTML = `
          <div class="label">${platform.toUpperCase()}</div>
          <div class="behavior">${data.behavior}</div>
        `;
        grid.appendChild(card);
      });
    }

    // Function to simulate random state updates
    function updateNodesRandomly() {
      Object.keys(nodes).forEach(key => {
        // Reassign a random state
        const randomIndex = Math.floor(Math.random() * possibleStates.length);
        nodes[key].state = possibleStates[randomIndex];
      });
    }

    // Initial render of nodes
    renderNodes();

    // Refresh Matrix on button click: update states & re-render
    document.getElementById('refreshButton').addEventListener('click', () => {
      updateNodesRandomly();
      renderNodes();
    });
  </script>
</body>
</html>
