<h2>Live Demo</h2>

You can run the app by simply opening index.html in your browser, or host it via GitHub Pages (instructions below).

<h3>Features</h3>

🌱 Goal-based planning: Predefined milestones with friendly names (Go Getter ₹2L, Achiever ₹5L, Warrior ₹10L, Sharpshooter ₹25L, Maestro ₹50L).

📈 Monthly compounding: Converts annual return to a monthly rate and simulates month-by-month.

➕ Yearly SIP step-up: Optional fixed ₹ increase to monthly SIP every 12 months.

💼 Annual top-up: Optional lump sum added to the corpus once a year.

🎯 Single-goal summary + comparative chart: See time to a selected goal and months needed across milestones.

💬 Tooltips + FAQs: Inline help and an accordion FAQ (with a video embed for “What is a SIP?”).

🔗 Blog CTAs: Three centered, themed buttons linking to related articles.

🧪 Built-in sanity checks: Quick console tests for monotonicity & effect of step-ups/top-ups.

<em>Note: The Ambassador (₹1 Cr) goal is intentionally removed in this repo.</em>

<h3>How It Works (1-minute)</h3>

The simulator advances one month at a time.

Monthly rate = (annualReturn% / 100) / 12.

Each month:
total = total * (1 + monthlyRate) + monthlySIP.

Every 12 months (months 12, 24, 36, …):

- If top-up enabled: add topUpAmt before growth & SIP.

- If step-up enabled: increase monthlySIP += stepUpAmt.

For each milestone, we count months until total >= goal. If it never reaches within a hard cap, it’s “Not reachable”.

<h3>Quick Start</h3>

Open index.html in a modern browser.

Set:

Initial corpus (₹)

Monthly SIP (₹)

Expected annual return (%)

(Optional) Toggle Yearly SIP step-up and set amount.

(Optional) Toggle Annual corpus top-up and set amount.

Click Calculate, then click a milestone button to see time (years + months).

<h3>Inputs Explained</h3>

Initial corpus (₹): Money you already have invested at the start. (0 is fine.)

Monthly SIP (₹): Added at the end of each month.

Expected annual return (%): Estimated yearly growth, converted to a monthly rate internally. Use conservative values (e.g., 8–12%).

Yearly SIP step-up: Fixed ₹ added to your SIP every 12 months (simulates salary increments).

Annual corpus top-up: Lump sum added once a year (good for bonuses/windfalls).

<h3>Reading the Results</h3>

Single-goal summary: After selecting a milestone, you’ll see “You’ll reach [Goal] in X years Y months.”

Chart: X-axis lists milestones; Y-axis is months needed. Lower is faster.

Not reachable: The model couldn’t achieve the milestone within its limit—try higher SIP, add step-ups/top-ups, or adjust return assumptions.

Customization
1) Theming

All brand colors live in the CSS root:

<code>
:root{
  --brand-green:#1faa59;
  --brand-yellow:#f5c842;
  --brand-deep:#0b2c20;
}
</code>


2) Blog CTA Buttons (centered, accessible, readable on hover)

Buttons live above the FAQ. The custom class ensures white text on green hover:

/* In <style> */
<code>
.btn-outline-brand{
  border-color: var(--brand-green);
  color: var(--brand-green);
}
.btn-outline-brand:hover,
.btn-outline-brand:focus{
  background-color: var(--brand-green);
  border-color: var(--brand-green);
  color: #fff;
}

<div class="text-center my-4">
  <div class="d-inline-flex justify-content-center gap-2 flex-wrap">
    <a class="btn btn-outline-brand" href="https://example.com/compounding" target="_blank" rel="noopener">
      Power of Compounding: Explained
    </a>
    <a class="btn btn-outline-brand" href="https://example.com/link-sip-to-goals" target="_blank" rel="noopener">
      Link Your SIP to Goals
    </a>
    <a class="btn btn-outline-brand" href="https://example.com/detailed-method" target="_blank" rel="noopener">
      Detailed Calculation Method
    </a>
  </div>
</div>
</code>

3) “What is a SIP?” — Video Embed

The first FAQ pane embeds a responsive YouTube video via Bootstrap’s ratio helper:

<code>
<div class="ratio ratio-16x9">
  <iframe
    src="https://www.youtube.com/embed/5h0PagpUsIs?si=HJyxVKj3A0CcYcxh"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    referrerpolicy="strict-origin-when-cross-origin"
    allowfullscreen
    loading="lazy"></iframe>
</div>
</code>

4) Tooltip Copy (Step-up & Top-up)

<code>
<!-- Step-up toggle tooltip -->
<span class="help" data-bs-toggle="tooltip" title="Want your wealth to grow faster? Give your SIP a raise – step up and reach your goals sooner.">?</span>

<!-- Top-up toggle tooltip -->
<span class="help" data-bs-toggle="tooltip" title="Want your wealth to grow faster? Give your SIP a raise – add an annual top-up and reach your goals sooner.">?</span>
</code>

5) Change Frequency (Yearly → Half-Yearly)

In monthsToReachGoal(...), switch the modulo checks:

<code>
// Yearly (default)
if (top > 0 && m > 0 && m % 12 === 0) { total += top; }
if (step > 0 && m > 0 && m % 12 === 0) { monthlySIP += step; }

// Half-yearly
// if (top > 0 && m > 0 && m % 6 === 0) { total += top; }
// if (step > 0 && m > 0 && m % 6 === 0) { monthlySIP += step; }
</code>

6) Add/Remove Milestones

Update the goals array + goalMeta map. The chart updates automatically.

<code>
const goals = [200000, 500000, 1000000, 2500000, 5000000]; // Ambassador removed
const goalMeta = {
  200000: 'Go Getter',
  500000: 'Achiever',
  1000000: 'Warrior',
  2500000: 'Sharpshooter',
  5000000: 'Maestro',
};
</code>

Project Structure
.
├── index.html    # Single-file app: HTML, CSS (in <style>), JS (in <script>)
└── README.md     # You are here


(Optional) Add a docs/ folder to include a user guide or screenshots:

docs/
  ├── user-guide.pdf
  └── screenshot.png

<h3>Local Development</h3>

Option A: Double-click index.html to open it in your browser.

Option B (recommended): Use a lightweight dev server so tooltips & imports behave consistently:

VS Code extension: Live Server

or run python -m http.server (then open http://localhost:8000)

Deploy to GitHub Pages

Push this repo to GitHub.

In your repo: Settings → Pages.

Source: Deploy from a branch → choose main and set folder to /root (or /docs if you place files there).

Save. Your app will be available at:
https://<your-username>.github.io/<your-repo>/

<h3>Troubleshooting</h3>

No change after clicking Calculate: Ensure expected return > 0% and either initial corpus > 0 or monthly SIP > 0.

Chart gaps / Not reachable: Increase SIP, add step-ups/top-ups, or adjust return (within reason).

Buttons text invisible on hover: Use the .btn-outline-brand CSS above (text turns white on green).

Tooltips not showing: Ensure Bootstrap JS is loading and the page is served over a local server (not a file:// URL) if your browser blocks some features.

License

MIT — feel free to use, modify, and distribute with attribution.
