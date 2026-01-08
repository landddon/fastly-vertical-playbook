<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Fastly Vertical Master Command Center</title>
    <style>
        :root { --fastly-red: #ff282d; --bg: #0a0a0a; --sidebar-bg: #000; --card-bg: #141414; --border: #2a2a2a; --text: #d1d1d1; --accent: #00d1ff; --gold: #ffd700; --green: #2ecc71; --persona-blue: #3498db; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background: var(--bg); color: var(--text); margin: 0; display: flex; height: 100vh; overflow: hidden; }
        #sidebar { width: 320px; background: var(--sidebar-bg); border-right: 1px solid var(--border); padding: 25px; overflow-y: auto; flex-shrink: 0; }
        .nav-head { color: var(--fastly-red); font-weight: 800; text-transform: uppercase; font-size: 11px; margin: 20px 0 8px; letter-spacing: 1.2px; }
        .btn { display: block; width: 100%; padding: 12px; margin-bottom: 5px; background: #111; border: 1px solid var(--border); color: #888; text-align: left; cursor: pointer; border-radius: 6px; font-size: 13px; transition: 0.2s; }
        .btn:hover { background: #222; color: #fff; }
        .btn.active { background: var(--fastly-red); color: #fff; border-color: var(--fastly-red); font-weight: bold; }
        #content { flex-grow: 1; padding: 25px; overflow-y: auto; scroll-behavior: smooth; }
        .vertical-section { display: none; max-width: 1400px; margin: 0 auto; }
        .vertical-section.active { display: block; }
        .toggle-container { display: flex; justify-content: center; margin-bottom: 20px; background: #1a1a1a; padding: 5px; border-radius: 50px; width: fit-content; margin: 0 auto; border: 1px solid #333; }
        .toggle-btn { padding: 10px 30px; border-radius: 50px; border: none; cursor: pointer; background: transparent; color: #888; font-weight: bold; transition: 0.3s; }
        .toggle-btn.active.cdn-mode { background: var(--accent); color: #000; }
        .toggle-btn.active.waf-mode { background: #f39c12; color: #000; }
        .exec-brief { display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px; margin-bottom: 20px; }
        .brief-box { background: #1a1a1a; padding: 15px; border-radius: 8px; border: 1px solid #333; font-size: 13px; }
        .brief-box h4 { margin: 0 0 10px 0; color: var(--fastly-red); font-size: 11px; text-transform: uppercase; letter-spacing: 1px; border-bottom: 1px solid #333; padding-bottom: 5px; }
        details { margin-bottom: 8px; cursor: pointer; }
        details summary { color: #fff; font-weight: 600; list-style: none; display: flex; align-items: center; }
        details summary::after { content: ' ▼'; font-size: 9px; margin-left: 5px; color: var(--accent); }
        details p { font-size: 12.5px; color: #aaa; margin: 5px 0 0 10px; line-height: 1.5; border-left: 1px solid var(--accent); padding-left: 8px; }
        .detail-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        .box { background: var(--card-bg); padding: 20px; border-radius: 10px; border: 1px solid var(--border); }
        .full { grid-column: span 2; }
        h3 { color: var(--fastly-red); margin-top: 0; font-size: 12px; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 15px; }
        .obj-box { border: 1px solid var(--gold); background: rgba(255, 215, 0, 0.05); }
        .persona-box { border: 1px solid var(--persona-blue); background: rgba(52, 152, 219, 0.05); }
        .talk-points-box { border: 1px solid var(--green); background: rgba(46, 204, 113, 0.05); }
        .kill-phrase { font-style: italic; background: rgba(255,255,255,0.05); padding: 12px; border-radius: 4px; display: block; margin-top: 10px; color: #fff; border-left: 3px solid var(--gold); font-size: 13.5px; }
        .hook-list { list-style: none; padding: 0; margin: 0; }
        .hook-list li { margin-bottom: 10px; padding-left: 25px; position: relative; font-size: 14px; line-height: 1.4; }
        .hook-list li::before { content: '💬'; position: absolute; left: 0; }
        .persona-track { margin-bottom: 15px; }
        .persona-track b { color: var(--persona-blue); display: block; font-size: 12px; text-transform: uppercase; margin-bottom: 4px; }
        .mode-content { display: none; }
        .mode-content.active { display: block; animation: slideIn 0.3s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .case-link { color: var(--accent); font-size: 12.5px; text-decoration: none; font-weight: bold; margin-top: 10px; display: inline-block; }
    </style>
</head>
<body>

<nav id="sidebar">
    <div style="font-size: 24px; font-weight: 900; color: #fff;">FASTLY<span style="color:var(--fastly-red)">.</span></div>
    <div style="font-size: 11px; color: #555; margin-bottom: 25px;">TITAN AE COMMAND V3 (2026)</div>

    <div class="nav-head">SAAS & PAAS</div>
    <button class="btn active" onclick="showVertical('saas-infra', this)">Infrastructure</button>
    <button class="btn" onclick="showVertical('saas-sec', this)">Security</button>
    <button class="btn" onclick="showVertical('saas-app', this)">Applications</button>

    <div class="nav-head">ECOMMERCE</div>
    <button class="btn" onclick="showVertical('ecom-fashion', this)">Fast Fashion</button>
    <button class="btn" onclick="showVertical('ecom-merch', this)">General Merchandise</button>
    <button class="btn" onclick="showVertical('ecom-pure', this)">Pure Play / Specialty</button>

    <div class="nav-head">FINANCIAL SERVICES</div>
    <button class="btn" onclick="showVertical('fin-retail', this)">Retail Banking</button>
    <button class="btn" onclick="showVertical('fin-invest', this)">Investment / Brokerage</button>
</nav>

<main id="content">

    <div id="saas-infra" class="vertical-section active">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('saas-infra', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('saas-infra', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>SaaS Infra: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Origin Shielding</summary><p>Acts as a centralized caching layer that protects your origin servers from global traffic spikes, reducing server load and cloud costs.</p></details>
                    <details><summary>Terraform Provider</summary><p>Integrates CDN configuration directly into DevOps workflows, allowing for automated infrastructure management and CI/CD consistency.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Prohibitive cloud egress fees and "Origin Collapse" during user surges.</li><li><b>Solution:</b> Request collapsing and high Cache Hit Ratio (95%+) to shield origin.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>VCL Flexibility:</b> Write custom logic directly at the edge for unique routing.</li><li><b>Scale:</b> 300+ Tbps global capacity for massive thundering herds.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How much of your subscription margin is currently lost to AWS/GCP egress fees?"</li><li>"What is the current wait time for your engineers to deploy a global configuration change?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Origin Shielding:</b> Focus on the "Insurance Policy" for their cloud.</li><li><b>Agility:</b> Contrast our 13s deploy time with legacy 15-minute windows.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>SRE/DevOps:</b> "Manage your whole delivery stack via Terraform without filing a support ticket."</div>
                    <div class="persona-track"><b>VP Eng:</b> "We help your team ship faster by removing the bottleneck of slow network configurations."</div>
                    <div class="persona-track"><b>CTO:</b> "We protect your cloud margins by eliminating up to 90% of your AWS/GCP data transfer fees."</div>
                </div>
                <div class="box"><h3>Core Tech: Request Collapsing</h3><p>Fastly merges identical requests for the same piece of content into a single request back to your backend, preventing origin overload.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We use CloudFront because it's bundled." <span class="kill-phrase">"Bundled CDNs often cost 2x more in hidden egress fees than a high-performance programmable edge."</span></p></div>
                <div class="box full"><h3>Proof: GitHub</h3><p>GitHub uses Fastly to manage millions of repo requests, achieving sub-second global delivery. <a href="https://www.fastly.com/customers/github" class="case-link">GitHub Case Study 🔗</a></p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>SaaS Infra: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Next-Gen WAF</summary><p>Uses signal-based detection to identify malicious intent without the performance tax of traditional regular expression-based WAFs.</p></details>
                    <details><summary>Real-time Logs</summary><p>Streams 100% of security event data to your SOC stack (Splunk/Datadog) in under 1 second for instant mitigation.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> False positives blocking legitimate customers.</li><li><b>Solution:</b> SmartParse logic engine that understands intent, allowing 90%+ Blocking Mode.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Deployment:</b> Install at the edge, cloud, or as a local agent on your servers.</li><li><b>Agility:</b> No "learning mode" required; immediate protection.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"Are you currently running your WAF in blocking mode, or just logging attacks?"</li><li>"How many hours a week does your team spend 'tuning' WAF rules?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Full Blocking:</b> 90% of our customers run in blocking mode—unheard of in legacy WAF.</li><li><b>Visibility:</b> "The Microscope"—seeing every blocked request instantly.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>SRE/DevOps:</b> "Security is finally part of your CI/CD. No more manual rule tuning."</div>
                    <div class="persona-track"><b>VP Eng:</b> "We eliminate the friction between security and dev. Your devs can focus on features."</div>
                    <div class="persona-track"><b>CISO:</b> "Fastly stops 95% of threats at the network edge, before they touch your cloud compute."</div>
                </div>
                <div class="box"><h3>Core Tech: SmartParse</h3><p>Evaluates request syntax to detect injections and XSS with surgical accuracy, avoiding brittle pattern matching.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We have a WAF in our Load Balancer." <span class="kill-phrase">"Legacy WAFs are black boxes; Fastly gives you a microscope into why requests were blocked."</span></p></div>
                <div class="box full"><h3>Proof: Okta</h3><p>Okta uses Fastly to stop account takeovers and credential stuffing at the network edge. <a href="https://www.fastly.com/customers/okta" class="case-link">Okta Case Study 🔗</a></p></div>
            </div>
        </div>
    </div>

    <div id="saas-sec" class="vertical-section">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('saas-sec', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('saas-sec', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>SaaS Security: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Instant Purge</summary><p>Allows security providers to invalidate globally cached session tokens or revoked keys in under 150 milliseconds.</p></details>
                    <details><summary>TLS Termination</summary><p>High-performance encryption at the edge ensuring end-to-end data privacy without adding latency.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Compromised tokens staying active in the cache too long.</li><li><b>Solution:</b> Sub-second global purge for immediate security consistency.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Accuracy:</b> Global consistency guarantees for security-sensitive assets.</li><li><b>Speed:</b> Fastest purge in the industry (average 150ms).</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"When a security token is revoked, how long does it take for that to be enforced globally?"</li><li>"Do your users experience lag during initial secure handshakes?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Global Revocation:</b> The importance of 150ms purge for session security.</li><li><b>Edge Encrypt:</b> Offloading TLS to the edge without losing visibility.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Dev:</b> "Invalidate specific user sessions globally in one API call."</div>
                    <div class="persona-track"><b>VP Eng:</b> "Maintain a consistent security posture globally with no 'stale' session windows."</div>
                    <div class="persona-track"><b>CISO:</b> "Reduce your attack surface by handling revocation at the network perimeter."</div>
                </div>
                <div class="box"><h3>Core Tech: Surrogate Keys</h3><p>Tag multiple related security objects with a single key to purge them all instantly with one API call.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"Security doesn't need a CDN." <span class="kill-phrase">"Caching tokens at the edge is only safe if you can purge them in milliseconds."</span></p></div>
                <div class="box full"><h3>Proof: Identity Providers</h3><p>Uses Fastly's edge to deliver authentication assets and security tokens with microsecond latency.</p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>SaaS Security: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Virtual Patching</summary><p>Blocks zero-day exploits at the network layer instantly, giving devs time to patch code safely.</p></details>
                    <details><summary>Credential Stuffing Protection</summary><p>Identifies automated login attempts using behavioral signals rather than simple IP blacklisting.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> High cost of manual response to new CVEs.</li><li><b>Solution:</b> Network-layer virtual patches deployed in seconds.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Zero-Downtime:</b> No restarts required for security policy updates.</li><li><b>Intent Detection:</b> Blocks the attack, not the legitimate user behind a shared IP.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How many credential stuffing attempts reach your database daily?"</li><li>"How long did it take you to patch for Log4j across your infrastructure?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Virtual Patch:</b> Stop the bleeding at the edge while the dev team works.</li><li><b>User Trust:</b> Protecting accounts without friction (no CAPTCHAs).</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>SecOps:</b> "Set threshold-based blocking for credential stuffing in minutes."</div>
                    <div class="persona-track"><b>VP Eng:</b> "Shield your origin from brute-force surges that impact app performance."</div>
                    <div class="persona-track"><b>CISO:</b> "Protect brand reputation by stopping account takeovers before they happen."</div>
                </div>
                <div class="box"><h3>Core Tech: Behavioral Signals</h3><p>Uses risk signals to identify automation by analyzing request frequency and TLS fingerprints.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We use a cloud provider WAF." <span class="kill-phrase">"Most cloud WAFs require a 24/7 team to tune rules. We automate the accuracy."</span></p></div>
                <div class="box full"><h3>Proof: Auth Providers</h3><p>Fastly protects the world's largest auth providers from automated ATO (Account Takeover) attacks.</p></div>
            </div>
        </div>
    </div>

    <div id="saas-app" class="vertical-section">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('saas-app', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('saas-app', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>SaaS Apps: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Compute@Edge</summary><p>Run custom logic (A/B testing, auth) at the edge in Rust/Go with zero cold starts.</p></details>
                    <details><summary>Soft Purge</summary><p>Serve 'stale' content to users while refreshing the cache in the background to ensure no 'slow' hits.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> 'Stale' data in collaborative apps causing user confusion.</li><li><b>Solution:</b> Instant global invalidation (150ms) for real-time consistency.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Edge Logic:</b> Move CPU-intensive logic away from origin to the network edge.</li><li><b>Observability:</b> Real-time analytics on app performance per region.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How do you ensure user changes are consistent globally and instantly?"</li><li>"Do users complain about UI lag when first loading your app?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Collaborative Speed:</b> Making a global app feel local.</li><li><b>Resource Offload:</b> Running A/B tests at the edge to save origin CPU.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Product Dev:</b> "Build personalization at the edge without the 'flicker' of client-side scripts."</div>
                    <div class="persona-track"><b>VP Eng:</b> "Lower your infrastructure TCO by moving dynamic logic to the edge."</div>
                    <div class="persona-track"><b>CTO:</b> "A faster app experience leads directly to higher user retention and NPS."</div>
                </div>
                <div class="box"><h3>Core Tech: WebAssembly (Wasm)</h3><p>Fastly's Compute uses Wasm for memory-isolated, microsecond execution with no cold starts.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"Our app is too dynamic for CDN." <span class="kill-phrase">"Fastly was built for dynamic apps. If your data changes every second, you need a CDN that purges in 150ms."</span></p></div>
                <div class="box full"><h3>Proof: Slack</h3><p>Slack uses Fastly to ensure millions have sub-second delivery of assets and consistent connectivity. <a href="https://www.fastly.com/customers/slack" class="case-link">Slack Case Study 🔗</a></p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>SaaS Apps: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>API Protection</summary><p>Deep inspection of API payloads to protect against mass assignment and injection attacks.</p></details>
                    <details><summary>Bot Protection</summary><p>Distinguishes between 'good bots' (search engines) and 'malicious scrapers' stealing lead lists.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> B2B app scrapers stealing customer lead lists or proprietary data.</li><li><b>Solution:</b> Advanced bot detection identifying scraping behavior without friction.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>API Visibility:</b> Automatically discover and protect shadow APIs.</li><li><b>GraphQL Security:</b> Protect complex nested queries from DDoS.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How are you preventing competitors from scraping your proprietary pricing or lead data?"</li><li>"Is your security layer adding noticeable latency to API response times?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Scraper Defense:</b> Protect your intellectual property from automated theft.</li><li><b>API Health:</b> Secure your endpoints without the 'WAF Tax' on speed.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>API Dev:</b> "Secure your endpoints with intent-based logic that won't block valid JSON."</div>
                    <div class="persona-track"><b>VP Eng:</b> "Scale your API infrastructure safely while reducing SOC overhead."</div>
                    <div class="persona-track"><b>CISO:</b> "Ensure compliance and data privacy across all your B2B app endpoints."</div>
                </div>
                <div class="box"><h3>Core Tech: Threshold Analysis</h3><p>Monitors client behavior across the app to identify scrapers based on session logic, not just IP.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"Security is a Dev issue." <span class="kill-phrase">"Stop threats at the network perimeter before they consume your origin resources."</span></p></div>
                <div class="box full"><h3>Proof: LaunchDarkly</h3><p>Uses Fastly to secure feature flags and configs globally. <a href="https://www.fastly.com/customers/launchdarkly" class="case-link">LaunchDarkly Case Study 🔗</a></p></div>
            </div>
        </div>
    </div>

    <div id="ecom-fashion" class="vertical-section">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('ecom-fashion', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('ecom-fashion', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>Fashion: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Image Optimizer</summary><p>Automates resizing and format conversion at the edge for faster mobile loads.</p></details>
                    <details><summary>Video Delivery</summary><p>High-bitrate delivery for catwalk videos and social commerce loops.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> High mobile bounce rates due to heavy hero images and video lag.</li><li><b>Solution:</b> Edge optimization to reduce page weight by up to 80%.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>SEO Lift:</b> Directly improves LCP scores for better organic rankings.</li><li><b>UX:</b> One high-res source serves every screen perfectly.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"If your gallery takes 3s to load on mobile, how many carts are abandoned?"</li><li>"How do you currently manage image variants for mobile vs desktop?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Mobile Conversion:</b> Speed = Revenue for fashion shoppers.</li><li><b>Dev Efficiency:</b> Stop manual image resizing and let the edge do the work.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Creative/Frontend:</b> "Upload once. Fastly handles every device and browser automatically."</div>
                    <div class="persona-track"><b>Ecom Manager:</b> "Improve your Google search rank by optimizing your Core Web Vitals."</div>
                    <div class="persona-track"><b>CTO:</b> "Reduce origin storage and egress costs by serving optimized assets from the edge."</div>
                </div>
                <div class="box"><h3>Core Tech: Auto-Format</h3><p>Detects the browser (Chrome/Safari) and serves the smallest format (WebP/AVIF) automatically.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We use a resizer script." <span class="kill-phrase">"Script-based resizers add latency. Fastly optimizes in-flight inside the network path."</span></p></div>
                <div class="box full"><h3>Proof: Revolve</h3><p>Saw a massive lift in mobile conversion and SEO rank via Fastly IO. <a href="https://www.fastly.com/customers/revolve" class="case-link">Revolve Case Study 🔗</a></p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>Fashion: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Bot Management</summary><p>Identifies inventory hoarders who block real customers during limited drops.</p></details>
                    <details><summary>DDoS Protection</summary><p>Absorbs massive traffic spikes during influencer-driven hype drops.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Limited edition drops resold instantly by bots while fans are blocked.</li><li><b>Solution:</b> Real-time fingerprinting that protects inventory for real human buyers.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Frictionless:</b> No CAPTCHAs to kill conversion during a high-heat sale.</li><li><b>Block the Bot:</b> Ensures fair access for actual brand loyalists.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"Are bots buying out your limited drops before fans can even load the page?"</li><li>"How much inventory is locked in 'ghost carts' during your sales?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Fair Play:</b> Keep your product in the hands of fans, not resellers' bots.</li><li><b>Checkout Speed:</b> Security that won't slow down the 'Add to Cart' path.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Marketing:</b> "Ensure your influencers' fans actually get the product they're hyped for."</div>
                    <div class="persona-track"><b>Ecom Lead:</b> "Stop bot-driven inventory hoarding that leads to false 'out of stock' messages."</div>
                    <div class="persona-track"><b>CISO:</b> "Protect customer accounts from ATO attacks during high-traffic events."</div>
                </div>
                <div class="box"><h3>Core Tech: Behavioral Logic</h3><p>Analyzes mouse movements and TLS fingerprints to spot bots without user friction.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We use CAPTCHA." <span class="kill-phrase">"CAPTCHAs are conversion killers. If a bot can't be stopped silently, the security has failed."</span></p></div>
                <div class="box full"><h3>Proof: Hype Retailers</h3><p>Fastly protects some of the world's most aggressive 'sneaker drops' and fashion launches.</p></div>
            </div>
        </div>
    </div>

    <div id="ecom-merch" class="vertical-section">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('ecom-merch', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('ecom-merch', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>Merch: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Surrogate Keys</summary><p>Group thousands of SKUs (e.g., all 'Sale' items) for instant batch purging.</p></details>
                    <details><summary>Shielding</summary><p>Protects origin from thundering herds during holiday sales.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> 'Out of Stock' messages lagging DB, leading to refunds.</li><li><b>Solution:</b> 150ms global sync between storefront and database.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Inventory Accuracy:</b> The only CDN that can sync massive catalogs at speed.</li><li><b>Scale:</b> Built for Black Friday level traffic spikes.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"Does your storefront lag when the inventory database updates?"</li><li>"What was your origin offload during the last holiday peak?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Real-time Pricing:</b> Updating thousands of sale prices in seconds.</li><li><b>Cloud Savings:</b> Minimizing origin load to save on server costs.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Ops:</b> "Keep your servers up during the holiday rush with 90%+ cache hit ratio."</div>
                    <div class="persona-track"><b>Ecom Lead:</b> "Avoid lost sales by ensuring stock levels are accurate in the cache."</div>
                    <div class="persona-track"><b>CFO:</b> "Lower your annual cloud hosting bill by offloading traffic to the edge."</div>
                </div>
                <div class="box"><h3>Core Tech: Granular Purge</h3><p>Purges only the specific changed SKU rather than a full site flush, maintaining speed.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We have a long contract." <span class="kill-phrase">"Offload your highest-cost Inventory APIs to Fastly today as a starting point."</span></p></div>
                <div class="box full"><h3>Proof: Target</h3><p>Handles extreme holiday spikes by offloading traffic to Fastly. <a href="https://www.fastly.com/blog/target-architecting-for-peak-traffic" class="case-link">Target Case Study 🔗</a></p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>Merch: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Rate Limiting</summary><p>Prevents DDoS on 'Buy' buttons without blocking real traffic.</p></details>
                    <details><summary>GraphQL Security</summary><p>Protects headless commerce APIs from data exfiltration.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Competitor scrapers stealing price data and stock levels.</li><li><b>Solution:</b> Deceive scrapers with fake data while shoppers see the truth.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>No Performance Tax:</b> Security that won't slow down the checkout path.</li><li><b>Detailed Logs:</b> Identify exactly which APIs are targeted by bots.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How much of your traffic is competitors scraping your pricing?"</li><li>"Are security rules slowing down your 'Time to Checkout'?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Anti-Scrape:</b> Protect your competitive advantage in the market.</li><li><b>Headless Security:</b> Secure your React/Vue apps at the network layer.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Security Eng:</b> "Get full visibility into every bot trying to scrap your catalog."</div>
                    <div class="persona-track"><b>Ecom Lead:</b> "Protect your checkout funnel from automated fraud without adding lag."</div>
                    <div class="persona-track"><b>CISO:</b> "Secure your entire modern API stack with one unified security layer."</div>
                </div>
                <div class="box"><h3>Core Tech: Deception Logic</h3><p>Wastes bot resources by feeding them fake responses, protecting real origin data.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"Origin security is enough." <span class="kill-phrase">"Bots at the origin consume your budget. Stop them at the edge before they cost money."</span></p></div>
                <div class="box full"><h3>Proof: Ticketmaster</h3><p>Secures global ticket sales against massive bot surges during events. <a href="https://www.fastly.com/customers/ticketmaster" class="case-link">Ticketmaster Security 🔗</a></p></div>
            </div>
        </div>
    </div>

    <div id="ecom-pure" class="vertical-section">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('ecom-pure', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('ecom-pure', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>Pure Play: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Edge Personalization</summary><p>Run logic at the edge to serve localized pricing or banners instantly.</p></details>
                    <details><summary>A/B Testing</summary><p>Test UI/UX variants at the network level for zero-flicker experiments.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Personalization scripts causing UI 'flicker' and slow interactivity.</li><li><b>Solution:</b> Server-side personalization at the edge for seamless loads.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>No Flicker:</b> Fastly decisioning happens before the page even loads.</li><li><b>VCL Control:</b> Build complex referrals and loyalty logic at the edge.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"Do A/B testing scripts cause 'flicker' that hurts your conversion?"</li><li>"How do you localize pricing globally without origin lag?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Zero Flicker:</b> Maintain brand trust with professional personalization.</li><li><b>Log Obsession:</b> Use 100% request visibility to fix checkout drop-offs.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>UX Dev:</b> "Run experiments at the edge to eliminate JS-heavy testing lag."</div>
                    <div class="persona-track"><b>Product:</b> "Deliver a personalized experience to every user globally in under 50ms."</div>
                    <div class="persona-track"><b>CTO:</b> "Modernize your 'Headless' stack by moving logic to the network edge."</div>
                </div>
                <div class="box"><h3>Core Tech: Edge Decisioning</h3><p>Evaluates user cookies to serve the correct site variant instantly from the edge cache.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We use Optimizely." <span class="kill-phrase">"Script-based tools cost 500ms of lag. Fastly does it at the network layer for zero lag."</span></p></div>
                <div class="box full"><h3>Proof: Priceline</h3><p>Uses Fastly to deliver millions of travel search results instantly. <a href="https://www.fastly.com/customers/priceline" class="case-link">Priceline Case Study 🔗</a></p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>Pure Play: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Account Takeover (ATO)</summary><p>Stops automated credential stuffing against digital-only user accounts.</p></details>
                    <details><summary>Headless Security</summary><p>Protects GraphQL and React/Vue stacks at the network edge.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Scrapers stealing lead lists or proprietary digital catalogs.</li><li><b>Solution:</b> Deep API inspection that validates queries at the edge.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Dev Alignment:</b> Security that fits a modern digital-native workflow.</li><li><b>Performance:</b> 95% of threats stopped without origin hits.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How are you currently securing your GraphQL endpoints?"</li><li>"Do you have visibility into which APIs bots are targeting right now?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Brand Integrity:</b> Prevent account takeovers that ruin digital customer trust.</li><li><b>API Shielding:</b> Protecting the most vulnerable part of a headless stack.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Sec Eng:</b> "Get a debugger for the network to see why bots are targeting your APIs."</div>
                    <div class="persona-track"><b>Product:</b> "Secure your digital-first brand without ruining the shopper UX."</div>
                    <div class="persona-track"><b>CISO:</b> "Scale your business safely with security that can't be bypassed by automation."</div>
                </div>
                <div class="box"><h3>Core Tech: API Logic Parsing</h3><p>Inspects API calls to ensure attackers aren't bypassing auth or scraping the whole database.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We're a small team." <span class="kill-phrase">"Fastly automates security accuracy, acting as a force multiplier for your small team."</span></p></div>
                <div class="box full"><h3>Proof: 1stdibs</h3><p>Delivers and secures a high-end luxury marketplace with sub-second performance. <a href="https://www.fastly.com/customers/1stdibs" class="case-link">1stdibs Case Study 🔗</a></p></div>
            </div>
        </div>
    </div>

    <div id="fin-retail" class="vertical-section">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('fin-retail', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('fin-retail', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>Retail Bank: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>PCI DSS Level 1</summary><p>Highest security standard for processing and delivering payment/bank data.</p></details>
                    <details><summary>Data Pinning</summary><p>Ensures sensitive logs/traffic are restricted to specific regions (EU/US/AUS).</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Strict regulatory requirements for data residency and audit logs.</li><li><b>Solution:</b> Geo-fencing and regional pinning of all banking traffic and logs.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Audit Ready:</b> Every single request is logged for annual compliance audits.</li><li><b>Speed:</b> Banking apps that feel local and fast globally.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How do you guarantee that banking data/logs stay inside regional borders?"</li><li>"How much time is spent preparing traffic logs for annual compliance audits?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Compliant Speed:</b> Performance that doesn't break the rules.</li><li><b>Log Sovereignty:</b> Give the auditors exactly what they need instantly.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Infrastructure:</b> "Pin your services to specific POPs to ensure strict data residency compliance."</div>
                    <div class="persona-track"><b>Compliance:</b> "Stream 100% of transaction logs to your secure internal vault for audits."</div>
                    <div class="persona-track"><b>CTO:</b> "Modernize your banking UX to compete with fintechs while staying compliant."</div>
                </div>
                <div class="box"><h3>Core Tech: Regional Pins</h3><p>Ensures traffic never leaves a required jurisdiction, meeting strict legal requirements.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"Compliance says no Cloud." <span class="kill-phrase">"Fastly is PCI Level 1 and SOC2 compliant. We are the trusted edge for global banks."</span></p></div>
                <div class="box full"><h3>Proof: Canstar</h3><p>Delivers leading financial comparison with banking-grade speed and security. <a href="https://www.fastly.com/customers/canstar" class="case-link">Canstar Case Study 🔗</a></p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>Retail Bank: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>NGWAF</summary><p>Identifies credential stuffing with surgical accuracy via the SmartParse engine.</p></details>
                    <details><summary>ATO Protection</summary><p>Stops account takeover attempts on banking portals before they hit the DB.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Brittle WAF rules blocking legitimate bank customers.</li><li><b>Solution:</b> Intent-based analysis allowing high-accuracy Blocking Mode.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Trust:</b> No human 'tuning' required to avoid blocking valid bank logins.</li><li><b>Immediate:</b> 90% of customers block threats from Day 1.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How many customers were blocked by your current WAF last month?"</li><li>"How long does it take your team to patch a new banking portal vulnerability?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Zero False Blocks:</b> Ensure your customers can always access their money.</li><li><b>ATO Defense:</b> Protecting the front door from automated password testers.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>SOC Team:</b> "Eliminate Friday night rule-tuning marathons with automated accuracy."</div>
                    <div class="persona-track"><b>VP Eng:</b> "Keep your banking portal up and secure during massive volatility spikes."</div>
                    <div class="persona-track"><b>CISO:</b> "Reduce risk by stopping 95% of attacks at the perimeter, far from the vault."</div>
                </div>
                <div class="box"><h3>Core Tech: Syntax Evaluation</h3><p>Differentiates between a complex user password and a SQL command with logic, not regex.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We use hardware F5s." <span class="kill-phrase">"Hardware can't keep up with cloud-scale botnets. You need a distributed edge to win."</span></p></div>
                <div class="box full"><h3>Proof: Global Finance</h3><p>Secures login portals for millions with zero false-positive blocks and zero downtime.</p></div>
            </div>
        </div>
    </div>

    <div id="fin-invest" class="vertical-section">
        <div class="toggle-container">
            <button class="toggle-btn active cdn-mode" onclick="flipMode('fin-invest', 'cdn', this)">CDN Mode</button>
            <button class="toggle-btn" onclick="flipMode('fin-invest', 'waf', this)">WAF Mode</button>
        </div>
        <div class="mode-content active cdn-view">
            <h1>Investment: CDN View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>Fanout (WebSockets)</summary><p>Pushes real-time market data to millions of users simultaneously with low latency.</p></details>
                    <details><summary>Micro-Caching</summary><p>Caches ticker data for milliseconds to ensure real-time delivery with origin protection.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> Ticker lag during market volatility causing 'stale' trader data.</li><li><b>Solution:</b> Fanout pushes updates globally in microseconds, bypassing origin load.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Push-Based:</b> Data is pushed to users, not polled, for ultra-low latency.</li><li><b>Scale:</b> Maintain millions of open connections without origin overhead.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"What happens to your ticker lag when market volatility spikes 10x?"</li><li>"How do you currently scale WebSockets for millions of traders?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Trading Agility:</b> Microseconds define the winner in this market.</li><li><b>Origin Relief:</b> Keep your trading engine focused on trades, not data push.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>Infra Dev:</b> "Offload WebSocket connection management to Fastly's edge cloud."</div>
                    <div class="persona-track"><b>Head of Trading:</b> "Ensure every trader globally gets price updates at exactly the same microsecond."</div>
                    <div class="persona-track"><b>CTO:</b> "Handle trillion-dollar market volatility without adding network latency."</div>
                </div>
                <div class="box"><h3>Core Tech: Fanout</h3><p>Allows the edge to maintain open pipes, fanning out one origin update to millions of clients.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"Our current speed is 'good enough'." <span class="kill-phrase">"In trading, 'good enough' is being 50ms behind the market. You're losing."</span></p></div>
                <div class="box full"><h3>Proof: Tradeweb</h3><p>Monitors trillions in trades with sub-second logging and visibility. <a href="https://www.fastly.com/blog/how-tradeweb-monitors-trillions-of-dollars-in-trades-with-fastly-logging" class="case-link">Tradeweb Case Study 🔗</a></p></div>
            </div>
        </div>
        <div class="mode-content waf-view">
            <h1>Investment: WAF View</h1>
            <div class="exec-brief">
                <div class="brief-box"><h4>Product Overview</h4>
                    <details><summary>API Protection</summary><p>Inspects gRPC/GraphQL trading APIs to prevent trade injection or theft.</p></details>
                    <details><summary>DDoS Absorption</summary><p>100+ Tbps capacity to absorb attacks without affecting trade speed.</p></details>
                </div>
                <div class="brief-box"><h4>Pain & Solution</h4><ul><li><b>Pain:</b> DDoS attacks targeting trading endpoints during market open/close.</li><li><b>Solution:</b> Distributed edge network that stops attacks far from the trading core.</li></ul></div>
                <div class="brief-box"><h4>Unique USPs</h4><ul><li><b>Precision:</b> Blocks the attack, not the shared IP used by good traders.</li><li><b>Performance:</b> microsecond security checks for zero trade lag.</li></ul></div>
            </div>
            <div class="detail-grid">
                <div class="box full"><h3>Discovery Hooks</h3><ul class="hook-list"><li>"How do you distinguish between a massive trade spike and a DDoS?"</li><li>"What would 5 minutes of downtime cost your brand during a market surge?"</li></ul></div>
                <div class="box talk-points-box"><h3>Core Talking Points</h3><ul class="hook-list"><li><b>Invisible Security:</b> Protect your trades without adding a single millisecond.</li><li><b>Endpoint Shield:</b> Stop automated trade injection at the perimeter.</li></ul></div>
                <div class="box persona-box"><h3>Persona Talk Tracks</h3>
                    <div class="persona-track"><b>API Eng:</b> "Secure gRPC trading endpoints with line-speed syntax inspection."</div>
                    <div class="persona-track"><b>Risk Officer:</b> "Mitigate the impact of zero-day exploits on your trading floor instantly."</div>
                    <div class="persona-track"><b>CISO:</b> "Defend against sophisticated, multi-vector DDoS attacks on your trade core."</div>
                </div>
                <div class="box"><h3>Core Tech: Zero-Latency Logic</h3><p>Inspects traffic at line speed, ensuring zero 'security tax' on transaction execution.</p></div>
                <div class="box obj-box"><h3>Objection Handling</h3><p>"We have on-prem hardware." <span class="kill-phrase">"Hardware is a bottleneck. The cloud edge is the only place to stop a cloud-scale attack."</span></p></div>
                <div class="box full"><h3>Proof: Brokerages</h3><p>Global brokerages use Fastly to secure trading portals with microsecond-level accuracy.</p></div>
            </div>
        </div>
    </div>

</main>

<script>
    function showVertical(vid, btn) {
        document.querySelectorAll('.vertical-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.btn').forEach(b => b.classList.remove('active'));
        document.getElementById(vid).classList.add('active');
        btn.classList.add('active');
    }
    function flipMode(vid, mode, btn) {
        const container = document.getElementById(vid);
        container.querySelectorAll('.mode-content').forEach(m => m.classList.remove('active'));
        container.querySelectorAll('.toggle-btn').forEach(b => b.classList.remove('active', 'cdn-mode', 'waf-mode'));
        if (mode === 'cdn') { container.querySelector('.cdn-view').classList.add('active'); btn.classList.add('cdn-mode'); }
        else { container.querySelector('.waf-view').classList.add('active'); btn.classList.add('waf-mode'); }
        btn.classList.add('active');
    }
</script>

</body>
</html>
