
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>微光重力學｜地球物理探勘互動筆記</title>
    
    <!-- Google Fonts & FontAwesome Icons -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300;400;600;700&family=Cinzel:wght@400;600&family=JetBrains+Mono:wght@300;400;500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Chart.js for data visualization -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- MathJax for rendering LaTeX math formulas -->
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="mathjax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

    <style>
        :root {
            --bg-color: #fcfbf9;
            --paper-color: #ffffff;
            --text-main: #2c3237;
            --text-muted: #6c757d;
            --accent-sage: #6b8e23;
            --accent-warm: #c86d51;
            --accent-sand: #d4b896;
            --accent-navy: #2b4c6f;
            --border-color: #e8e5df;
            --shadow: 0 10px 30px rgba(0, 0, 0, 0.04);
            --transition: all 0.4s cubic-bezier(0.25, 1, 0.5, 1);
        }

        [data-theme="dark"] {
            --bg-color: #1a1c1e;
            --paper-color: #24272a;
            --text-main: #e2e4e6;
            --text-muted: #9aa0a6;
            --accent-sage: #8ab446;
            --accent-warm: #e07a5f;
            --accent-sand: #8c7355;
            --accent-navy: #648fff;
            --border-color: #34383c;
            --shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Noto Serif TC', serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.8;
            transition: var(--transition);
            overflow-x: hidden;
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(252, 251, 249, 0.85);
            backdrop-filter: blur(12px);
            z-index: 1000;
            border-bottom: 1px solid var(--border-color);
            transition: var(--transition);
        }

        [data-theme="dark"] nav {
            background: rgba(26, 28, 30, 0.85);
        }

        .nav-container {
            max-width: 1100px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1.2rem 2rem;
        }

        .brand {
            font-family: 'Cinzel', serif;
            font-size: 1.3rem;
            font-weight: 600;
            letter-spacing: 2px;
            color: var(--text-main);
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            text-decoration: none;
            color: var(--text-muted);
            font-size: 0.95rem;
            font-weight: 400;
            transition: var(--transition);
            position: relative;
        }

        .nav-links a:hover, .nav-links a.active {
            color: var(--accent-warm);
        }

        .theme-toggle {
            background: none;
            border: none;
            color: var(--text-main);
            cursor: pointer;
            font-size: 1.1rem;
            padding: 5px;
            transition: var(--transition);
        }

        /* Hero Header */
        header {
            padding: 10rem 2rem 5rem;
            text-align: center;
            max-width: 850px;
            margin: 0 auto;
        }

        .subtitle {
            font-family: 'Cinzel', serif;
            color: var(--accent-warm);
            letter-spacing: 3px;
            font-size: 0.9rem;
            text-transform: uppercase;
            margin-bottom: 1rem;
            display: block;
        }

        header h1 {
            font-size: 2.8rem;
            font-weight: 700;
            margin-bottom: 1.5rem;
            line-height: 1.3;
            letter-spacing: -0.5px;
        }

        header p {
            color: var(--text-muted);
            font-size: 1.1rem;
            font-weight: 300;
        }

        /* Container Sections */
        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 0 2rem 6rem;
        }

        section {
            background: var(--paper-color);
            border-radius: 16px;
            padding: 3rem;
            margin-bottom: 4rem;
            border: 1px solid var(--border-color);
            box-shadow: var(--shadow);
            transition: var(--transition);
        }

        .section-title {
            font-size: 1.8rem;
            font-weight: 600;
            margin-bottom: 2rem;
            position: relative;
            padding-bottom: 0.8rem;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 40px;
            height: 2px;
            background-color: var(--accent-warm);
        }

        /* Interactive Gravity Difference Component */
        .interactive-box {
            background: var(--bg-color);
            border-radius: 12px;
            padding: 2rem;
            margin: 2rem 0;
            border: 1px solid var(--border-color);
        }

        .controls-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .control-group {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .control-group label {
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--text-muted);
        }

        .slider {
            width: 100%;
            accent-color: var(--accent-warm);
            cursor: pointer;
        }

        .value-display {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.1rem;
            color: var(--accent-navy);
            font-weight: 500;
        }

        /* Cards & Grids */
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
        }

        @media (max-width: 768px) {
            .grid-2 { grid-template-columns: 1fr; }
            header h1 { font-size: 2rem; }
            section { padding: 1.8rem; }
            .nav-links { display: none; }
        }

        .card {
            background: var(--paper-color);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 1.8rem;
            transition: var(--transition);
        }

        .card:hover {
            transform: translateY(-3px);
        }

        .card h3 {
            font-size: 1.2rem;
            margin-bottom: 0.8rem;
            color: var(--accent-navy);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* Formula & Derivation Accordion/Steps */
        .derivation-step {
            border-left: 3px solid var(--accent-sand);
            padding-left: 1.5rem;
            margin-bottom: 2rem;
            position: relative;
        }

        .derivation-step h4 {
            font-size: 1.1rem;
            color: var(--accent-warm);
            margin-bottom: 0.5rem;
        }

        .formula-badge {
            display: inline-block;
            background: rgba(200, 109, 81, 0.1);
            color: var(--accent-warm);
            padding: 0.3rem 0.8rem;
            border-radius: 6px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.95rem;
            margin: 0.5rem 0;
        }

        /* Math Display Box */
        .math-block {
            background: var(--bg-color);
            padding: 1.2rem;
            border-radius: 8px;
            overflow-x: auto;
            margin: 1rem 0;
            border: 1px solid var(--border-color);
            font-family: 'JetBrains Mono', monospace;
        }

        /* Tabbed Example Section */
        .tab-container {
            display: flex;
            gap: 1rem;
            border-bottom: 1px solid var(--border-color);
            margin-bottom: 2rem;
        }

        .tab-btn {
            background: none;
            border: none;
            padding: 0.8rem 1.2rem;
            font-family: inherit;
            font-size: 1rem;
            color: var(--text-muted);
            cursor: pointer;
            border-bottom: 2px solid transparent;
            transition: var(--transition);
        }

        .tab-btn.active {
            color: var(--accent-warm);
            border-bottom-color: var(--accent-warm);
            font-weight: 600;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 3rem 2rem;
            color: var(--text-muted);
            font-size: 0.9rem;
            border-top: 1px solid var(--border-color);
        }

        .highlight-box {
            background: rgba(107, 142, 35, 0.08);
            border-left: 4px solid var(--accent-sage);
            padding: 1.2rem 1.5rem;
            border-radius: 0 8px 8px 0;
            margin: 1.5rem 0;
        }

        .badge {
            font-size: 0.75rem;
            padding: 2px 8px;
            border-radius: 4px;
            text-transform: uppercase;
            font-weight: 600;
        }

        .badge-plus { background: #d4edda; color: #155724; }
        .badge-minus { background: #f8d7da; color: #721c24; }
    </style>
</head>
<body>

    <!-- Nav -->
    <nav>
        <div class="nav-container">
            <a href="#" class="brand"><i class="fa-solid fa-globe"></i> GEOPHYSICS 1015</a>
            <ul class="nav-links">
                <li><a href="#diff"><i class="fa-solid fa-compass"></i> 重力異同</a></li>
                <li><a href="#corrections"><i class="fa-solid fa-sliders"></i> 布蓋修正與加減辨析</a></li>
                <li><a href="#derivation"><i class="fa-solid fa-square-root-variable"></i> 公式推導</a></li>
                <li><a href="#example"><i class="fa-solid fa-calculator"></i> 經典例題</a></li>
            </ul>
            <button class="theme-toggle" id="themeToggle"><i class="fa-solid fa-moon"></i></button>
        </div>
    </nav>

    <!-- Header -->
    <header>
        <span class="subtitle">臺北市立大學 地球環境暨生物資源學系</span>
        <h1>閱讀地球的微光重力</h1>
        <p>從牛頓萬有引力到地底隱藏質量的探勘美學。探索重力差異、自由空氣修正與布蓋修正的數學藝術。</p>
    </header>

    <div class="container">

        <!-- Section 1: 重力差異與全球探索 -->
        <section id="diff">
            <h2 class="section-title"><i class="fa-solid fa-earth-americas"></i> 不同地方的重力差異</h2>
            <p>在國中物理中，我們常以 \(g \approx 9.8 \text{ m/s}^2\) 作為常數。然而地球物理學告訴我們：<b>地球重力場並非均勻一致</b>。在全球尺度與區域探勘尺度下，重力加速數皆有些微卻關鍵的變化。</p>

            <div class="interactive-box">
                <h3 style="margin-bottom: 1rem;"><i class="fa-solid fa-chart-line"></i> 緯度與地球緯度重力模擬器</h3>
                <div class="controls-grid">
                    <div class="control-group">
                        <label for="latSlider">觀測點緯度 (\(\phi\)): <span id="latValue" class="value-display">48.12° N</span></label>
                        <input type="range" id="latSlider" class="slider" min="0" max="90" value="48.12" step="0.01">
                    </div>
                    <div class="control-group">
                        <label>理論重力值 (\(g_t\))</label>
                        <div id="theoreticalResult" class="value-display" style="font-size: 1.3rem;">980,901.60 mGal</div>
                    </div>
                </div>
                <div style="height: 220px; width: 100%;">
                    <canvas id="gravityLatChart"></canvas>
                </div>
                <p style="font-size: 0.85rem; color: var(--text-muted); margin-top: 1rem; text-align: center;">
                    依據 1967 年國際測地學協會公式：\(g_t = g_e (1 + 0.005278895 \sin^2\phi + 0.000023462 \sin^4\phi)\)
                </p>
            </div>

            <div class="grid-2">
                <div class="card">
                    <h3><i class="fa-solid fa-arrows-split-up-and-left"></i> 全球尺度：為何赤道比兩極「輕」？</h3>
                    <p>緯度越高，觀測到的重力值越大（赤道約 \(978,000\text{ mGal}\)；兩極約 \(983,000\text{ mGal}\)）：</p>
                    <ul style="padding-left: 1.2rem; margin-top: 0.5rem; color: var(--text-muted);">
                        <li><b>離心力效應：</b>赤道旋轉離心力最大，方向與重力相反，相互抵銷。</li>
                        <li><b>赤道隆起：</b>地球為扁球體，赤道地心距離 \(R\) 較大，依據平方反比律，\(g\) 較小。</li>
                    </ul>
                </div>
                <div class="card">
                    <h3><i class="fa-solid fa-mountain-sun"></i> 探勘尺度：地底質量的微細符號</h3>
                    <p>去除緯度效應後，地底密度的差異將以微小的重力異常（Anomaly）展現：</p>
                    <ul style="padding-left: 1.2rem; margin-top: 0.5rem; color: var(--text-muted);">
                        <li><b>重力高區 (Gravity High)：</b>地下埋藏高密度體（如鐵礦床），造成局部質量 \(M \uparrow \implies g \uparrow\)。</li>
                        <li><b>重力低區 (Gravity Low)：</b>地下存在低密度體（如石鹽丘、鐘乳石洞），造成質量 \(M \downarrow \implies g \downarrow\)。</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Section 2: BG FAC 修正與加減邏輯 -->
        <section id="corrections">
            <h2 class="section-title"><i class="fa-solid fa-sliders"></i> 重力修正：FAC 與 BC 應該加還是減？</h2>
            <p>在實際野外觀測時，儀器測得的「觀測重力值 (\(g_{obs}\))」會受到測站高程與測站下方岩層質量的影響。為了能與海平面基準面的理論重力值相比較，我們必須進行<b>高程修正</b>。</p>

            <div class="highlight-box">
                <h4 style="color: var(--accent-sage); margin-bottom: 0.5rem;"><i class="fa-solid fa-lightbulb"></i> 核心思考法則：歸一到海平面基準面（Datum）</h4>
                <p>異常值的基本定義為：<b>異常值 = 歸一修正後的重力值 - 理論重力值 (\(g_t\))</b>。加減號取決於「野外觀測值比海平面基準多還是少」。</p>
            </div>

            <div class="grid-2" style="margin-top: 2rem;">
                <div class="card">
                    <h3>自由空氣修正 (Free Air Correction, FAC)</h3>
                    <p><b>概念：</b>僅考量測站高度 \(h\) 離地心變遠（空氣無質量），不考慮中間物質。</p>
                    <div class="formula-badge">FAC = 0.3086 × h (mGal)</div>
                    <ul style="padding-left: 1.2rem; margin-top: 0.8rem; font-size: 0.95rem;">
                        <li><b>陸地上 (h > 0)：</b>測站偏高，離地心遠，測得重力<b>偏小</b>。要歸一到海平面，必須把少計的重力<b>「加」回來</b>。<br><span class="badge badge-plus">修正值 ＝ +0.3086 × h</span></li>
                        <li><b>海平面下 (h < 0)：</b>測站偏低，離地心近，必須<b>「減」去</b>高出的重力。</li>
                    </ul>
                </div>

                <div class="card">
                    <h3>布蓋修正 (Bouguer Correction, BC)</h3>
                    <p><b>概念：</b>扣除測站與海平面之間岩盤（無限板塊）額外質量所帶來的引力吸引。</p>
                    <div class="formula-badge">BC = 2πGρh ≈ 0.0419ρh (mGal)</div>
                    <ul style="padding-left: 1.2rem; margin-top: 0.8rem; font-size: 0.95rem;">
                        <li><b>陸地上 (h > 0)：</b>腳下的岩石提供了多餘的重力吸引，使觀測值<b>偏大</b>。要回歸基準面，必須<b>「減」掉</b>這層岩石的引力。<br><span class="badge badge-minus">修正值 ＝ -0.112 × h</span> (設 \(\rho=2.67\text{ g/cm}^3\))</li>
                        <li><b>海洋測站 (海深 d)：</b>海水密度 (\(1.03\)) 小於正常陸地地殼 (\(2.67\))，存在「質量虧損」，需要特別補算替換。</li>
                    </ul>
                </div>
            </div>

            <!-- Summarized Logic Table -->
            <div style="margin-top: 2.5rem; overflow-x: auto;">
                <table style="width: 100%; border-collapse: collapse; text-align: left; font-size: 0.95rem;">
                    <thead>
                        <tr style="border-bottom: 2px solid var(--border-color); color: var(--accent-navy);">
                            <th style="padding: 10px;">修正項目</th>
                            <th style="padding: 10px;">環境物理狀態</th>
                            <th style="padding: 10px;">對觀測值的影響</th>
                            <th style="padding: 10px;">歸一修正符號 (計算異常時)</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr style="border-bottom: 1px solid var(--border-color);">
                            <td style="padding: 12px; font-weight: 600;">FAC (自由空氣)</td>
                            <td style="padding: 12px;">陸地上高程 \(h > 0\) (距離地心變遠)</td>
                            <td style="padding: 12px;">重力衰減 (偏小)</td>
                            <td style="padding: 12px; color: var(--accent-sage); font-weight: 600;">加 (+) 補回衰減量</td>
                        </tr>
                        <tr>
                            <td style="padding: 12px; font-weight: 600;">BC (布蓋板塊)</td>
                            <td style="padding: 12px;">陸地上高程 \(h > 0\) (腳下多出一層岩盤)</td>
                            <td style="padding: 12px;">額外吸引力 (偏大)</td>
                            <td style="padding: 12px; color: var(--accent-warm); font-weight: 600;">減 (-) 扣除板塊質量</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <!-- Section 3: 公式推導 (FAC & BC Step-by-Step) -->
        <section id="derivation">
            <h2 class="section-title"><i class="fa-solid fa-square-root-variable"></i> 公式嚴謹推導</h2>
            <p>這裏記錄講義講稿中極具數學美感的微分與積分推導歷程。</p>

            <div class="derivation-step">
                <h4>Part 1: 自由空氣修正常數 (\(0.3086 \text{ mGal/m}\)) 推導</h4>
                <p>已知地球表面重力加速度公式為 \(g = \frac{GM}{R^2}\)。當觀測點上升高度 \(h\) 時，相較於地球平均半徑 \(R \approx 6,371 \text{ km}\)，\(h\) 極小。我們可以對高程 \(R\) 做全微分：</p>
                <div class="math-block">
                    $$\frac{dg}{dR} = \frac{d}{dR}\left( GM R^{-2} \right) = -2 GM R^{-3} = -\frac{2}{R} \left( \frac{GM}{R^2} \right) = -\frac{2g}{R}$$
                </div>
                <p>因此高度變化 \(h\) 引起的重力變化量 \(\Delta g\)（取絕對值）為：</p>
                <div class="math-block">
                    $$\text{FAC} = \frac{2g}{R} \times h$$
                </div>
                <p>將 \(g \approx 9.80665 \text{ m/s}^2\)，\(R \approx 6,371,000 \text{ m}\) 代入：</p>
                <div class="math-block">
                    $$\text{FAC} = \frac{2 \times 9.80665}{6371000} \times h \approx 3.078 \times 10^{-6} \text{ m/s}^2/\text{m} = \mathbf{0.3086 \text{ mGal/m}}$$
                </div>
            </div>

            <div class="derivation-step">
                <h4>Part 2: 布蓋板塊修正公式 (\(\text{BC} = 2\pi G \rho h\)) 積分推導</h4>
                <p>假設測站下方岩盤可模型化為半徑無限大、厚度為 \(h\)、密度為 \(\rho\) 的平鋪圓盤（Infinite Slab Model）。</p>
                
                <p><b>1. 微分薄圓環的重力垂直分量：</b></p>
                <p>設一圓環半徑為 \(x\)，寬度 \(dx\)，厚度 \(dz\)，深為 \(z\)。圓環體積 \(dV = 2\pi x \cdot dx \cdot dz\)，質量 \(dm = \rho \, dV = 2\pi \rho x \, dx \, dz\)。</p>
                <p>質點引力方向對測站 \(P\) 的夾角為 \(\theta\)，僅垂直向下分量 \(\cos\theta = \frac{z}{r} = \frac{z}{\sqrt{x^2+z^2}}\) 有效：</p>
                <div class="math-block">
                    $$dg_z = \frac{G \cdot dm}{r^2} \cos\theta = G \cdot \frac{2\pi \rho x \, dx \, dz}{x^2+z^2} \cdot \frac{z}{\sqrt{x^2+z^2}} = 2\pi G \rho z \, dz \cdot \frac{x \, dx}{(x^2+z^2)^{3/2}}$$
                </div>

                <p><b>2. 對水平無窮大薄圓盤積分 (\(x: 0 \to \infty\))：</b></p>
                <div class="math-block">
                    $$dg_{slab} = 2\pi G \rho z \, dz \int_{0}^{\infty} \frac{x \, dx}{(x^2+z^2)^{3/2}} = 2\pi G \rho z \, dz \left[ -\frac{1}{\sqrt{x^2+z^2}} \right]_{0}^{\infty} = 2\pi G \rho \, dz$$
                </div>

                <p><b>3. 對厚度積分 (\(z: 0 \to h\))：</b></p>
                <div class="math-block">
                    $$\text{BC} = \int_{0}^{h} 2\pi G \rho \, dz = \mathbf{2\pi G \rho h}$$
                </div>

                <p>代入萬有引力常數 \(G = 6.674 \times 10^{-11} \text{ m}^3\text{kg}^{-1}\text{s}^{-2}\)，若 \(\rho\) 單位為 \(\text{g/cm}^3\)，\(h\) 為 \(\text{m}\)：</p>
                <div class="math-block">
                    $$\text{BC} = 0.04193 \times \rho \times h \text{ (mGal)}$$
                    $$\text{若取標準地殼密度 } \rho = 2.67 \text{ g/cm}^3 \implies \mathbf{\text{BC} \approx 0.112 \times h \text{ (mGal)}}$$
                </div>
            </div>
        </section>

        <!-- Section 4: 講義 8-2 經典例題解算 -->
        <section id="example">
            <h2 class="section-title"><i class="fa-solid fa-calculator"></i> 經典例題示範 (講義 Problem 8-2)</h2>
            <p>透過講義中的實際測站數據，一步步拆解計算過程。</p>

            <!-- Interactive Tab Menu -->
            <div class="tab-container">
                <button class="tab-btn active" onclick="switchTab('tab-a')">小題 (a): 陸地高程測站</button>
                <button class="tab-btn" onclick="switchTab('tab-b')">小題 (b): 海洋水深測站</button>
            </div>

            <!-- Tab A Content -->
            <div id="tab-a" class="tab-content active">
                <div class="highlight-box" style="margin-bottom: 1.5rem;">
                    <b>測站已知條件：</b><br>
                    緯度 \(\phi = 48.1195^\circ\text{ N}\)｜經度 \(\lambda = 12.1878^\circ\text{ E}\)<br>
                    高程 \(h = 487.9\text{ m}\)｜觀測重力值 \(g_{obs} = 980,717.39\text{ mGal}\)
                </div>

                <div class="derivation-step">
                    <h4>i) 計算理論重力值 (\(g_t\))</h4>
                    <div class="math-block">
                        $$g_t = 978031.85 \left(1 + 0.005278895 \sin^2(48.1195^\circ) + 0.000023462 \sin^4(48.1195^\circ)\right)$$
                        $$g_t \approx \mathbf{980,901.60 \text{ mGal}}$$
                    </div>
                </div>

                <div class="derivation-step">
                    <h4>ii) 計算自由空氣修正量 (FAC) 與 異常值 (FAA)</h4>
                    <div class="math-block">
                        $$\text{FAC} = 0.3086 \times 487.9 = \mathbf{150.57 \text{ mGal}}$$
                        $$\text{FAA} = g_{obs} + \text{FAC} - g_t = 980717.39 + 150.57 - 980901.60 = \mathbf{-33.64 \text{ mGal}}$$
                    </div>
                </div>

                <div class="derivation-step">
                    <h4>iii) 計算布蓋修正量 (BC) 與 布蓋重力異常 (BA)</h4>
                    <p>假設地殼岩石密度 \(\rho = 2.67\text{ g/cm}^3\)：</p>
                    <div class="math-block">
                        $$\text{BC} = 0.112 \times 487.9 = \mathbf{54.64 \text{ mGal}}$$
                        $$\text{BA} = \text{FAA} - \text{BC} = -33.64 - 54.64 = \mathbf{-88.28 \text{ mGal}}$$
                    </div>
                </div>
            </div>

            <!-- Tab B Content -->
            <div id="tab-b" class="tab-content">
                <div class="highlight-box" style="margin-bottom: 1.5rem;">
                    <b>測站已知條件：</b><br>
                    相同緯度/經度/觀測值，但位於<b>海平面海面上</b>，水深 \(d = 487.9\text{ m}\)<br>
                    海水密度 \(\rho_w = 1.03\text{ g/cm}^3\)，地殼密度 \(\rho_m = 2.67\text{ g/cm}^3\)
                </div>

                <div class="derivation-step">
                    <h4>i) 海洋測站自由空氣異常 (FAA)</h4>
                    <p>因測站位於海平面上 (\(h = 0\))，故 \(\text{FAC} = 0\)：</p>
                    <div class="math-block">
                        $$\text{FAA} = g_{obs} - g_t = 980717.39 - 980901.60 = \mathbf{-184.21 \text{ mGal}}$$
                    </div>
                </div>

                <div class="derivation-step">
                    <h4>ii) 海洋布蓋修正 (Oceanic Bouguer Correction)</h4>
                    <p>海洋修正需將水深 \(d\) 的海水替換為同體積之標準地殼岩石，補足質量虧損（\(\Delta \rho = \rho_m - \rho_w = 2.67 - 1.03 = 1.64\text{ g/cm}^3\)）：</p>
                    <div class="math-block">
                        $$\text{BC}_{ocean} = 2\pi G (\rho_m - \rho_w) d = 0.04193 \times (2.67 - 1.03) \times 487.9$$
                        $$\text{BC}_{ocean} \approx 0.04193 \times 1.64 \times 487.9 \approx \mathbf{33.55 \text{ mGal}}$$
                        $$\text{BA}_{ocean} = \text{FAA} + \text{BC}_{ocean} = -184.21 + 33.55 = \mathbf{-150.66 \text{ mGal}}$$
                    </div>
                </div>
            </div>

        </section>

    </div>

    <!-- Footer -->
    <footer>
        <p>微光重力學 ‧ 地球物理探勘 1015 互動講義</p>
        <p style="font-size: 0.8rem; margin-top: 0.5rem; opacity: 0.7;">Design with Noto Serif TC & Cinzel | Math Powered by MathJax</p>
    </footer>

    <!-- Interactive Scripts -->
    <script>
        // 1. Dark Theme Toggle
        const themeToggle = document.getElementById('themeToggle');
        const body = bodyElement = document.body;

        themeToggle.addEventListener('click', () => {
            const currentTheme = body.getAttribute('data-theme');
            if (currentTheme === 'dark') {
                body.removeAttribute('data-theme');
                themeToggle.innerHTML = '<i class="fa-solid fa-moon"></i>';
            } else {
                body.setAttribute('data-theme', 'dark');
                themeToggle.innerHTML = '<i class="fa-solid fa-sun"></i>';
            }
            updateChartColors();
        });

        // 2. Interactive Latitude Chart & Calculator
        const latSlider = document.getElementById('latSlider');
        const latValue = document.getElementById('latValue');
        const theoreticalResult = document.getElementById('theoreticalResult');

        function calcTheoreticalGravity(lat) {
            const rad = lat * Math.PI / 180;
            const sin2 = Math.pow(Math.sin(rad), 2);
            const sin4 = Math.pow(Math.sin(rad), 4);
            // 1967 Formula
            const g = 978031.85 * (1 + 0.005278895 * sin2 + 0.000023462 * sin4);
            return g;
        }

        // Initialize Chart
        const ctx = document.getElementById('gravityLatChart').getContext('2d');
        const lats = Array.from({length: 91}, (_, i) => i);
        const gravData = lats.map(l => calcTheoreticalGravity(l));

        let chart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: lats,
                datasets: [{
                    label: '理論重力值 g_t (mGal)',
                    data: gravData,
                    borderColor: '#c86d51',
                    borderWidth: 2,
                    fill: false,
                    pointRadius: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: false }
                },
                scales: {
                    x: {
                        title: { display: true, text: '緯度 (°)' },
                        grid: { display: false }
                    },
                    y: {
                        title: { display: true, text: 'mGal' },
                        suggestedMin: 978000,
                        suggestedMax: 984000
                    }
                }
            }
        });

        function updateChartColors() {
            const isDark = body.getAttribute('data-theme') === 'dark';
            const color = isDark ? '#9aa0a6' : '#6c757d';
            chart.options.scales.x.title.color = color;
            chart.options.scales.y.title.color = color;
            chart.options.scales.x.ticks.color = color;
            chart.options.scales.y.ticks.color = color;
            chart.update();
        }

        latSlider.addEventListener('input', (e) => {
            const lat = parseFloat(e.target.value);
            latValue.innerText = `${lat.toFixed(2)}° N`;
            const gVal = calcTheoreticalGravity(lat);
            theoreticalResult.innerText = `${gVal.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})} mGal`;
        });

        // 3. Tab System Switcher
        function switchTab(tabId) {
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            
            event.currentTarget.classList.add('active');
            document.getElementById(tabId).classList.add('active');
        }
    </script>
</body>
</html>
