<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Legacy 26.3 — Setup (.exe)</title>
  <style>
    :root {
      --bg: #070a12;
      --card: rgba(255,255,255,.06);
      --stroke: rgba(255,255,255,.12);
      --text: #eaf0ff;
      --muted: #94a3b8;
      --accent: #7c5cff;
      --accent2: #22d3ee;
      --danger: #ff5c7a;
      --radius: 20px;
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color: var(--text);
      background:
        radial-gradient(900px 500px at 15% 10%, rgba(124,92,255,.25), transparent 60%),
        radial-gradient(700px 500px at 85% 25%, rgba(34,211,238,.16), transparent 55%),
        radial-gradient(900px 700px at 50% 120%, rgba(255,92,122,.12), transparent 60%),
        var(--bg);
      min-height: 100vh;
      overflow-x: hidden;
    }

    .noise {
      position: fixed; inset: 0; pointer-events: none; opacity: .035;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.8' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.6'/%3E%3C/svg%3E");
      z-index: 999;
    }

    .wrap { width: min(1160px, 92%); margin: 0 auto; }

    header {
      position: sticky; top: 0; z-index: 50;
      backdrop-filter: blur(16px);
      background: rgba(7,10,18,.68);
      border-bottom: 1px solid var(--stroke);
    }

    .nav {
      display: flex; align-items: center; justify-content: space-between;
      gap: 16px; padding: 14px 0;
    }

    .brand {
      display: flex; align-items: center; gap: 10px;
      font-weight: 800; letter-spacing: .3px;
      text-decoration: none; color: var(--text);
    }

    .logo {
      width: 34px; height: 34px; border-radius: 12px;
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      box-shadow: 0 0 24px rgba(124,92,255,.45);
      display: grid; place-items: center; font-size: 16px;
    }

    .nav-links {
      display: flex; gap: 18px; align-items: center;
      font-size: 14px; color: var(--muted);
    }

    .nav-links a { color: var(--muted); text-decoration: none; transition: .2s; }
    .nav-links a:hover { color: var(--text); }

    .btn {
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,.07);
      color: var(--text);
      padding: 10px 16px;
      border-radius: 12px;
      font-weight: 700;
      cursor: pointer;
      transition: .2s;
      text-decoration: none;
      display: inline-flex; align-items: center; justify-content: center;
      gap: 8px;
    }

    .btn:hover { transform: translateY(-1px); background: rgba(255,255,255,.11); }

    .btn-primary {
      background: linear-gradient(135deg, var(--accent), #4f46e5);
      border-color: transparent;
      box-shadow: 0 10px 30px rgba(124,92,255,.28);
    }

    .btn-primary:hover { box-shadow: 0 14px 38px rgba(124,92,255,.38); }

    .hero {
      padding: 76px 0 42px;
      display: grid;
      grid-template-columns: 1.15fr .85fr;
      gap: 36px;
      align-items: center;
    }

    .pill {
      display: inline-flex; align-items: center; gap: 8px;
      padding: 7px 12px;
      border-radius: 999px;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,.05);
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 18px;
    }

    .dot {
      width: 8px; height: 8px; border-radius: 50%;
      background: #34d399;
      box-shadow: 0 0 12px #34d399;
    }

    h1 {
      margin: 0 0 16px;
      font-size: clamp(38px, 6vw, 66px);
      line-height: .98;
      letter-spacing: -2px;
    }

    .grad {
      background: linear-gradient(90deg, #fff, #b9a7ff 45%, #6ee7f9);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }

    .lead {
      color: var(--muted);
      font-size: 17px;
      line-height: 1.65;
      max-width: 560px;
      margin: 0 0 26px;
    }

    .hero-actions { display: flex; gap: 12px; flex-wrap: wrap; }

    .hero-card {
      position: relative;
      border: 1px solid var(--stroke);
      background: linear-gradient(180deg, rgba(255,255,255,.09), rgba(255,255,255,.03));
      border-radius: 26px;
      padding: 20px;
      box-shadow: 0 30px 80px rgba(0,0,0,.45);
      overflow: hidden;
    }

    .hero-card::before {
      content: "";
      position: absolute; inset: -2px;
      background: linear-gradient(135deg, rgba(124,92,255,.5), transparent 40%, rgba(34,211,238,.35));
      z-index: -1;
      filter: blur(24px);
    }

    .window-bar {
      display: flex; gap: 8px; margin-bottom: 18px;
    }

    .window-bar i {
      width: 10px; height: 10px; border-radius: 50%;
      background: rgba(255,255,255,.2);
      display: block;
    }

    .window-bar i:nth-child(1) { background: #ff5c7a; }
    .window-bar i:nth-child(2) { background: #fbbf24; }
    .window-bar i:nth-child(3) { background: #34d399; }

    .mock-row {
      display: flex; align-items: center; justify-content: space-between;
      padding: 12px 14px;
      border: 1px solid var(--stroke);
      background: rgba(0,0,0,.18);
      border-radius: 12px;
      margin-bottom: 10px;
      font-size: 14px;
    }

    .mock-row span:last-child {
      color: #34d399;
      font-size: 12px;
      font-weight: 800;
    }

    .mock-row:nth-child(3) span:last-child { color: #fbbf24; }
    .mock-row:nth-child(4) span:last-child { color: #22d3ee; }

    section { padding: 58px 0; }

    .section-head { margin-bottom: 26px; }

    .section-head h2 {
      margin: 0 0 8px;
      font-size: clamp(26px, 4vw, 38px);
      letter-spacing: -1px;
    }

    .section-head p { margin: 0; color: var(--muted); }

    .grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 14px;
    }

    .card {
      border: 1px solid var(--stroke);
      background: var(--card);
      border-radius: var(--radius);
      padding: 20px;
      transition: .22s;
      backdrop-filter: blur(10px);
    }

    .card:hover {
      transform: translateY(-3px);
      border-color: rgba(124,92,255,.45);
      background: rgba(255,255,255,.08);
    }

    .icon {
      width: 42px; height: 42px; border-radius: 14px;
      display: grid; place-items: center;
      background: linear-gradient(135deg, rgba(124,92,255,.25), rgba(34,211,238,.15));
      border: 1px solid var(--stroke);
      margin-bottom: 14px;
      font-size: 19px;
    }

    .card h3 { margin: 0 0 8px; font-size: 16px; }
    .card p { margin: 0; color: var(--muted); font-size: 14px; line-height: 1.55; }

    .tags { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 14px; }

    .tag {
      font-size: 12px;
      color: #cbd5e1;
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,.04);
      border-radius: 999px;
      padding: 5px 9px;
    }

    .download {
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 24px;
      align-items: center;
      border: 1px solid var(--stroke);
      background:
        radial-gradient(500px 180px at 20% 0%, rgba(124,92,255,.22), transparent 60%),
        rgba(255,255,255,.045);
      border-radius: 26px;
      padding: 30px;
      margin-top: 10px;
    }

    .download h2 { margin: 0 0 8px; font-size: 30px; letter-spacing: -1px; }
    .download p { margin: 0; color: var(--muted); line-height: 1.6; }

    .download-actions { display: flex; gap: 12px; flex-wrap: wrap; }

    .file-meta {
      display: flex; gap: 10px; flex-wrap: wrap;
      margin-top: 16px;
      font-size: 12px;
      color: #cbd5e1;
    }

    .file-meta span {
      border: 1px solid var(--stroke);
      background: rgba(0,0,0,.2);
      padding: 6px 10px;
      border-radius: 10px;
    }

    .file-meta b { color: #fff; font-weight: 700; }

    .notice {
      margin-top: 14px;
      font-size: 12px;
      color: #7c8aa5;
    }

    .req {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
      margin-top: 28px;
    }

    .req-item {
      border: 1px solid var(--stroke);
      background: rgba(255,255,255,.035);
      border-radius: 16px;
      padding: 16px;
      font-size: 13px;
      color: var(--muted);
    }

    .req-item b {
      display: block;
      color: var(--text);
      font-size: 13px;
      margin-bottom: 4px;
    }

    footer {
      border-top: 1px solid var(--stroke);
      padding: 26px 0;
      color: var(--muted);
      font-size: 13px;
      display: flex;
      justify-content: space-between;
      gap: 16px;
      flex-wrap: wrap;
    }

    footer a { color: var(--muted); text-decoration: none; }
    footer a:hover { color: var(--text); }

    .toast {
      position: fixed;
      left: 50%; bottom: 24px;
      transform: translateX(-50%) translateY(20px);
      opacity: 0;
      background: rgba(15,23,42,.92);
      border: 1px solid var(--stroke);
      color: var(--text);
      padding: 12px 16px;
      border-radius: 12px;
      font-size: 14px;
      transition: .25s;
      pointer-events: none;
      z-index: 1000;
      backdrop-filter: blur(10px);
    }

    .toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

    @media (max-width: 900px) {
      .hero { grid-template-columns: 1fr; padding-top: 48px; }
      .grid { grid-template-columns: 1fr 1fr; }
      .download { grid-template-columns: 1fr; }
      .nav-links { display: none; }
      .req { grid-template-columns: 1fr 1fr; }
    }

    @media (max-width: 620px) {
      .grid, .req { grid-template-columns: 1fr; }
      h1 { letter-spacing: -1px; }
      .download { padding: 22px; }
    }
  </style>
</head>
<body>
  <div class="noise"></div>

  <header>
    <div class="wrap nav">
      <a class="brand" href="#">
        <span class="logo">L</span>
        <span>Legacy <span style="color:var(--muted);font-weight:600">26.3</span></span>
      </a>
      <nav class="nav-links">
        <a href="#features">Функции</a>
        <a href="#combat">Combat</a>
        <a href="#visual">Visual</a>
        <a href="#download">Скачать Setup</a>
      </nav>
      <button class="btn btn-primary" onclick="toast('Это заглушка. Реального .exe тут нет.')">Скачать .exe</button>
    </div>
  </header>

  <main class="wrap">
    <section class="hero">
      <div>
        <div class="pill"><span class="dot"></span> версия 26.3 · Windows Setup</div>
        <h1>Legacy <span class="grad">26.3</span><br>установщик .exe</h1>
        <p class="lead">
          Тёмный интерфейс, быстрый рендер и модульная архитектура.
          Это только макет сайта: кнопка «Скачать .exe» — заглушка, установщика и файлов здесь нет.
        </p>
        <div class="hero-actions">
          <button class="btn btn-primary" onclick="toast('Заглушка: установщик LegacySetup-26.3.exe не существует.')">Скачать LegacySetup-26.3.exe</button>
          <button class="btn" onclick="toast('Заглушка: раздел с функциями.')">Смотреть функции</button>
        </div>
      </div>

      <div class="hero-card">
        <div class="window-bar"><i></i><i></i><i></i></div>
        <div class="mock-row"><span>LegacySetup-26.3.exe</span><span>SETUP</span></div>
        <div class="mock-row"><span>KillAura</span><span>ON</span></div>
        <div class="mock-row"><span>AutoTotem</span><span>ON</span></div>
        <div class="mock-row"><span>ESP / Chams</span><span>ON</span></div>
        <div class="mock-row"><span>HUD Editor</span><span>READY</span></div>
      </div>
    </section>

    <section id="features">
      <div class="section-head">
        <h2>Модули</h2>
        <p>Категории из твоего списка — в виде карточек.</p>
      </div>
      <div class="grid">
        <article class="card" id="combat">
          <div class="icon">⚔️</div>
          <h3>Combat</h3>
          <p>KillAura, TriggerBot, AutoTotem, AutoArmor, AutoHeal, AutoTool, AutoSwap, AntiTotem, NoFriendDamage.</p>
          <div class="tags"><span class="tag">KillAura</span><span class="tag">TriggerBot</span><span class="tag">AutoTotem</span></div>
        </article>

        <article class="card">
          <div class="icon">🏃</div>
          <h3>Movement</h3>
          <p>Speed, Strafe, Sprint, WaterSpeed, Fly, LongJump, Step, Spider, Jesus, NoSlow, NoFall, AntiVoid, InvMove.</p>
          <div class="tags"><span class="tag">Speed</span><span class="tag">Fly</span><span class="tag">NoFall</span></div>
        </article>

        <article class="card" id="visual">
          <div class="icon">👁️</div>
          <h3>Visual</h3>
          <p>ESP, Chams, Tracers, TargetESP, Trails, NameTags, StorageESP, Freecam, FreeLook, Zoom, NoRender, Fullbright.</p>
          <div class="tags"><span class="tag">ESP</span><span class="tag">Chams</span><span class="tag">Tracers</span></div>
        </article>

        <article class="card">
          <div class="icon">🧭</div>
          <h3>HUD</h3>
          <p>Watermark, ArrayList, FPS, FPSGraph, Coordinates, Keystrokes, Binds, Notifications, TargetHUD, PotionHUD, ArmorHUD.</p>
          <div class="tags"><span class="tag">ArrayList</span><span class="tag">TargetHUD</span><span class="tag">Keystrokes</span></div>
        </article>

        <article class="card">
          <div class="icon">🧩</div>
          <h3>Client</h3>
          <p>Menu, Theme, Accent, Rounded, Glass, Animations, Config, Friends, Enemies, Performance, AutoRespawn, AutoReconnect.</p>
          <div class="tags"><span class="tag">Config</span><span class="tag">Friends</span><span class="tag">Theme</span></div>
        </article>

        <article class="card">
          <div class="icon">🛠️</div>
          <h3>Utils / GUI</h3>
          <p>ClickGuiScreen, HudEditorScreen, ProfilesScreen, FriendsScreen, EnemiesScreen, AccountManagerScreen, ProxyScreen, RconScreen.</p>
          <div class="tags"><span class="tag">ClickGUI</span><span class="tag">Profiles</span><span class="tag">HUD Editor</span></div>
        </article>
      </div>
    </section>

    <section id="download">
      <div class="download">
        <div>
          <h2>Скачать Legacy 26.3 Setup</h2>
          <p>
            Установщик для Windows. В этом макете форма выбора версии, кнопка загрузки и чекбокс с соглашением
            специально оставлены заглушкой — файл не скачивается.
          </p>

          <div class="file-meta">
            <span>Файл: <b>LegacySetup-26.3.exe</b></span>
            <span>Платформа: <b>Windows 10/11 x64</b></span>
            <span>Размер: <b>~84.6 MB</b></span>
            <span>Тип: <b>Installer</b></span>
          </div>

          <div class="notice">Ссылки ведут в никуда. Реальных .exe-файлов и установщиков на странице нет.</div>
        </div>
        <div class="download-actions">
          <button class="btn btn-primary" onclick="toast('Заглушка: скачивание .exe отключено.')">Скачать .exe</button>
          <button class="btn" onclick="toast('Заглушка: профили.')">Профили</button>
        </div>
      </div>

      <div class="req">
        <div class="req-item"><b>ОС</b>Windows 10 / 11 (64-bit)</div>
        <div class="req-item"><b>Память</b>4 GB RAM минимум</div>
        <div class="req-item"><b>Java</b>Не требуется — установщик несёт всё с собой</div>
      </div>
    </section>
  </main>

  <footer class="wrap">
    <span>© 2026 Legacy 26.3 — demo landing.</span>
    <span><a href="#">Docs</a></span>
  </footer>

  <div class="toast" id="toast">Заглушка</div>

  <script>
    let toastTimer;
    function toast(message) {
      const el = document.getElementById('toast');
      el.textContent = message;
      el.classList.add('show');
      clearTimeout(toastTimer);
      toastTimer = setTimeout(() => el.classList.remove('show'), 2200);
    }

    document.querySelectorAll('a[href="#"]').forEach(a => {
      a.addEventListener('click', e => {
        e.preventDefault();
        toast('Это демо-ссылка. Реального перехода нет.');
      });
    });
  </script>
</body>
</html>
