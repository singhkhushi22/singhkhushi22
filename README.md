<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Khushi Singh — Neon Industrial Dev Profile</title>
  <style>
    /* ---------- Base + Neon Industrial Palette ---------- */
    :root{
      --bg:#0b0f12; /* near-black */
      --panel:#0f1720; /* deep grey-blue */
      --metal-1:#8893a7; /* steel highlight */
      --metal-2:#6b7686; /* darker metal */
      --neon-1:#00f0ff; /* cyan neon */
      --neon-2:#9b59ff; /* purple neon */
      --accent:#7efc6b; /* green accent */
      --warn:#ffb86b; /* industrial warning */
      --glass:rgba(255,255,255,0.03);
      --bolt:#2b2f33;
      --text:#dbe9ff;
      font-family:Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial;
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;background:radial-gradient(1200px 600px at 10% 10%, rgba(11,15,18,0.6), transparent), var(--bg);color:var(--text)}

    /* ---------- Layout ---------- */
    .wrap{max-width:1100px;margin:32px auto;padding:28px;display:grid;grid-template-columns:360px 1fr;gap:24px}

    /* ---------- Metal Panel (HMI) ---------- */
    .panel{background:linear-gradient(180deg,var(--panel),#091014);border:1px solid rgba(255,255,255,0.03);padding:18px;border-radius:12px;position:relative;box-shadow:0 8px 30px rgba(0,0,0,0.6);overflow:hidden}
    .panel:before,.panel:after{content:'';position:absolute;pointer-events:none}
    /* bolts in corners */
    .panel .bolt{position:absolute;width:20px;height:20px;background:var(--bolt);border-radius:3px;box-shadow:inset -2px -2px 4px rgba(255,255,255,0.03),inset 2px 2px 6px rgba(0,0,0,0.6)}
    .panel .bolt:after{content:'';position:absolute;inset:4px;border-radius:2px;background:linear-gradient(180deg,rgba(255,255,255,0.06),rgba(0,0,0,0.5))}
    .bolt.tl{left:8px;top:8px}
    .bolt.tr{right:8px;top:8px}
    .bolt.bl{left:8px;bottom:8px}
    .bolt.br{right:8px;bottom:8px}

    /* header */
    .header{display:flex;gap:12px;align-items:center}
    .avatar{width:72px;height:72px;border-radius:10px;background:linear-gradient(135deg,var(--metal-1),var(--metal-2));display:flex;align-items:center;justify-content:center;font-weight:700;color:var(--bg);box-shadow:0 6px 20px rgba(0,0,0,0.6)}
    .title{line-height:1}
    .title h1{margin:0;font-size:20px}
    .title p{margin:2px 0 0;font-size:13px;opacity:0.9}

    /* badges row */
    .badges{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px}
    .badge{display:inline-flex;align-items:center;gap:8px;padding:6px 10px;border-radius:8px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);border:1px solid rgba(255,255,255,0.03);font-size:13px}
    .badge svg{width:18px;height:18px;filter:drop-shadow(0 2px 6px rgba(0,0,0,0.6))}

    /* ---------- Robotic Arm Canvas ---------- */
    .arm-stage{background:linear-gradient(180deg,transparent,rgba(255,255,255,0.02));border-radius:8px;padding:12px;margin-top:14px;display:flex;align-items:center;justify-content:center;position:relative}
    svg.arm{width:100%;height:240px;max-height:260px}

    /* joints animation */
    .joint{transform-origin:50% 18%;}
    .joint-1{animation:joint1 3.6s ease-in-out infinite}
    .joint-2{animation:joint2 2.8s ease-in-out infinite}
    .joint-3{animation:joint3 2.2s ease-in-out infinite}
    @keyframes joint1{0%,100%{transform:rotate(0deg)}50%{transform:rotate(-12deg)}}
    @keyframes joint2{0%,100%{transform:rotate(6deg)}50%{transform:rotate(-22deg)}}
    @keyframes joint3{0%,100%{transform:rotate(-6deg)}50%{transform:rotate(28deg)}}

    /* gear */
    .gear{width:52px;height:52px}
    .gear.spin{animation:spin 3s linear infinite}
    @keyframes spin{from{transform:rotate(0)}to{transform:rotate(360deg)}}

    /* terminal-style box */
    .terminal{background:linear-gradient(180deg,rgba(0,0,0,0.6),rgba(255,255,255,0.02));padding:14px;border-radius:8px;font-family:monospace;font-size:13px;color:#9ae6ff;min-height:86px}
    .typewriter{display:inline-block;white-space:pre;overflow:hidden}
    .cursor{display:inline-block;width:8px;height:1.1em;background:var(--neon-1);margin-left:6px;animation:blink 1s steps(2) infinite}
    @keyframes blink{50%{opacity:0}}

    /* PLC indicators */
    .plc{display:flex;gap:8px;align-items:center;margin-top:12px}
    .plc .led{width:14px;height:14px;border-radius:4px;background:#111;border:1px solid rgba(255,255,255,0.04);box-shadow:inset 0 -4px 8px rgba(0,0,0,0.6)}
    .led.run{box-shadow:0 0 8px rgba(126,252,107,0.6);background:linear-gradient(180deg,var(--accent),#2b8e3d)}
    .led.fault{animation:flicker 2s linear infinite;background:linear-gradient(180deg,var(--warn),#ff6b00);box-shadow:0 0 8px rgba(255,184,107,0.6)}
    .led.emg{background:linear-gradient(180deg,#ff4666,#bb2233);box-shadow:0 0 8px rgba(255,70,102,0.6)}
    @keyframes flicker{0%,100%{opacity:1}50%{opacity:0.25}}

    /* separator */
    .separator{height:28px;margin:20px 0;display:flex;align-items:center}
    .separator svg{width:100%;height:100%}

    /* right column content */
    .right{display:grid;grid-template-rows:auto 1fr;gap:14px}
    .panel h2{margin:0 0 8px;font-size:16px}
    .projects{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .project{padding:12px;border-radius:8px;background:linear-gradient(180deg,rgba(255,255,255,0.015),transparent);border:1px solid rgba(255,255,255,0.02)}
    .project h3{margin:0 0 8px;font-size:14px}
    .project p{margin:0;font-size:13px;opacity:0.9}

    /* metal divider (animated stripes) */
    .metal-divider{height:8px;background:linear-gradient(90deg,rgba(0,0,0,0.3),rgba(255,255,255,0.03));position:relative;overflow:hidden;border-radius:6px}
    .metal-divider:after{content:'';position:absolute;left:-50%;top:0;bottom:0;width:50%;background:repeating-linear-gradient(45deg,rgba(255,255,255,0.03) 0 6px, transparent 6px 12px);transform:skewX(-25deg);animation:slide 3.5s linear infinite}
    @keyframes slide{to{left:100%}}

    /* footer */
    footer{margin-top:14px;text-align:center;font-size:12px;opacity:0.8}

    /* responsive */
    @media (max-width:900px){.wrap{grid-template-columns:1fr}.arm-stage{order:3}}
  </style>
</head>
<body>
  <div class="wrap">
    <!-- LEFT: HMI PANEL -->
    <div class="panel">
      <div class="bolt tl"></div>
      <div class="bolt tr"></div>
      <div class="bolt bl"></div>
      <div class="bolt br"></div>

      <div class="header">
        <div class="avatar">KS</div>
        <div class="title">
          <h1>Hi, I’m Khushi Singh <span style="opacity:0.6;font-size:12px">| Robotics & ROS2</span></h1>
          <p>Robotics & Automation Engineer • ROS2, Gazebo, SLAM, C++</p>
          <div class="badges">
            <!-- Example badges (SVG icons + label) -->
            <span class="badge"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" stroke-width="2"/></svg> ROS2</span>
            <span class="badge"><svg viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="16" rx="2"/></svg> Gazebo</span>
            <span class="badge"><svg viewBox="0 0 24 24"><path d="M2 12h20"/></svg> C++</span>
            <span class="badge"><svg viewBox="0 0 24 24"><path d="M4 6h16v12H4z"/></svg> SLAM</span>
          </div>
        </div>
      </div>

      <div class="arm-stage" aria-hidden="true">
        <!-- Simplified SVG robotic arm with joints -->
        <svg class="arm" viewBox="0 0 800 300" preserveAspectRatio="xMidYMid meet">
          <!-- background grid subtle -->
          <defs>
            <linearGradient id="metal" x1="0" x2="1"><stop offset="0" stop-color="#6b7686" stop-opacity="0.95"/><stop offset="1" stop-color="#3a4752"/></linearGradient>
          </defs>
          <g transform="translate(120,40)">
            <!-- base -->
            <g>
              <rect x="-20" y="220" width="120" height="36" rx="8" fill="url(#metal)" stroke="#071014" stroke-width="2"/>
              <circle cx="30" cy="230" r="18" fill="#111" stroke="#0f1b22" stroke-width="3"/>
            </g>
            <!-- joint1 -->
            <g class="joint joint-1" transform="translate(30,220)">
              <rect x="-8" y="-10" width="16" height="-80" rx="6" fill="#2b3640"/>
              <!-- joint cap -->
              <circle cx="0" cy="-82" r="12" fill="#0b1116" stroke="#9198a6" stroke-width="4"/>
              <!-- arm segment 1 -->
              <g transform="translate(0,-82)">
                <rect x="0" y="-8" width="200" height="16" rx="6" fill="url(#metal)"/>
              </g>
            </g>
            <!-- joint2 -->
            <g class="joint joint-2" transform="translate(230,120)">
              <circle cx="0" cy="0" r="14" fill="#0b1116" stroke="#91a0b1" stroke-width="4"/>
              <g transform="translate(0,0)">
                <rect x="0" y="-8" width="160" height="16" rx="6" fill="url(#metal)"/>
              </g>
            </g>
            <!-- joint3 / wrist -->
            <g class="joint joint-3" transform="translate(390,120)">
              <circle cx="0" cy="0" r="12" fill="#0b1116" stroke="#a1b0c3" stroke-width="3"/>
              <g transform="translate(0,0)">
                <!-- gripper -->
                <g transform="translate(24,-2)">
                  <rect x="0" y="-20" width="12" height="40" rx="3" fill="#1a2228"/>
                  <rect x="40" y="-20" width="12" height="40" rx="3" fill="#1a2228"/>
                  <line x1="12" y1="0" x2="40" y2="0" stroke="#789" stroke-width="4" />
                </g>
                <!-- neon indicator at wrist -->
                <circle cx="-8" cy="-8" r="6" fill="var(--neon-1)" opacity="0.9" />
              </g>
            </g>
          </g>
        </svg>
      </div>

      <div class="metal-divider" style="margin-top:14px"></div>

      <div style="display:flex;gap:12px;align-items:flex-start;flex-wrap:wrap;margin-top:12px">
        <div style="flex:1;min-width:180px">
          <div class="terminal" id="terminal">&gt; <span class="typewriter" id="typer">Initializing ROS2 nodes... </span><span class="cursor"></span></div>
          <div class="plc">
            <div style="display:flex;align-items:center;gap:8px"><div class="led run"></div><div style="font-size:13px">RUN</div></div>
            <div style="display:flex;align-items:center;gap:8px"><div class="led fault"></div><div style="font-size:13px">FAULT</div></div>
            <div style="display:flex;align-items:center;gap:8px"><div class="led emg"></div><div style="font-size:13px">EMG</div></div>
          </div>
        </div>
        <div style="width:120px;display:flex;flex-direction:column;gap:10px">
          <!-- little gear + status -->
          <div style="display:flex;align-items:center;gap:8px">
            <svg class="gear spin" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><g fill="#b9c8d8"><path d="M81 58l8-8-11-11-8 8c-3-2-6-3-10-3l-2-11H43l-2 11c-4 0-7 1-10 3l-8-8-11 11 8 8c-2 3-3 6-3 10l-11 2v14l11 2c0 4 1 7 3 10l-8 8 11 11 8-8c3 3 6 4 10 4l2 11h16l2-11c4 0 7-1 10-4l8 8 11-11-8-8c2-3 3-6 3-10l11-2V68l-11-2c0-4-1-7-3-10zM50 68a18 18 0 110-36 18 18 0 010 36z"/></g></svg>
            <div style="font-size:13px">Motor PID: <strong style="color:var(--neon-1)">OK</strong></div>
          </div>
          <div style="display:flex;align-items:center;gap:8px">
            <svg viewBox="0 0 24 24" width="42" height="42"><rect x="2" y="4" width="20" height="16" rx="2" fill="#223" stroke="#334"/></svg>
            <div style="font-size:13px">Gazebo sim <br><strong style="color:var(--neon-2)">v2025.11</strong></div>
          </div>
        </div>
      </div>

      <div style="margin-top:12px;display:flex;gap:10px;align-items:center;flex-wrap:wrap">
        <a href="https://www.linkedin.com/in/khushi-singh-a17932320" target="_blank" class="badge">🔗 LinkedIn</a>
        <a href="https://github.com/singhkhushi22" target="_blank" class="badge">🐙 GitHub</a>
        <a href="mailto:ksingh22052003@gmail.com" class="badge">✉️ Email</a>
      </div>

    </div>

    <!-- RIGHT: PROJECTS + DETAILS -->
    <div class="right">
      <div class="panel">
        <h2>Selected Projects</h2>
        <div class="projects">
          <div class="project">
            <h3>Mobile Robot Simulation (ROS2 + Gazebo)</h3>
            <p>URDF-based differential drive robot, LiDAR+IMU integration, SLAM mapping, obstacle avoidance, RViz visualizations.</p>
          </div>
          <div class="project">
            <h3>JAKA Cobot Workflow</h3>
            <p>Kinematics, pick-and-place demos, ROS interfacing, and safety checks for collaborative automation tasks.</p>
          </div>
          <div class="project">
            <h3>SCARA Modbus Integration</h3>
            <p>Real-time Modbus TCP/RTU communication, register mapping, and motion command sequences for SCARA control.</p>
          </div>
          <div class="project">
            <h3>Robot Mechanics Tutorials</h3>
            <p>Course materials, assignments and demo notebooks for mechanical principles & robotics labs.</p>
          </div>
        </div>

        <div class="separator">
          <!-- metallic SVG separator -->
          <svg viewBox="0 0 1200 40" preserveAspectRatio="none"><defs><linearGradient id="sep" x1="0" x2="1"><stop offset="0" stop-color="#0f1720"/><stop offset="0.5" stop-color="#14202a"/><stop offset="1" stop-color="#0f1720"/></linearGradient></defs>
            <rect width="1200" height="40" fill="url(#sep)"/>
            <g fill="none" stroke="#1c2730" stroke-width="2">
              <path d="M0 20 C150 0 350 40 600 20 C850 0 1050 40 1200 20" opacity="0.4"/>
            </g>
          </svg>
        </div>

        <h2>Skills & Tools</h2>
        <div style="display:flex;flex-wrap:wrap;gap:8px;margin-top:10px">
          <span class="badge">ROS2</span>
          <span class="badge">Gazebo</span>
          <span class="badge">C++</span>
          <span class="badge">SLAM</span>
          <span class="badge">LiDAR</span>
          <span class="badge">RViz</span>
          <span class="badge">Python</span>
        </div>
      </div>

      <div class="panel">
        <h2>About Me</h2>
        <p style="margin-top:6px">I’m a Robotics & Automation Engineer focused on bringing industrial robotic workflows into reliable simulation and production. I build ROS2 nodes, design URDFs, integrate sensors (LiDAR/IMU) and create control loops for real-world robots.</p>
        <div style="margin-top:12px;display:flex;gap:8px;align-items:center;flex-wrap:wrap">
          <a class="badge" href="#">📄 Resume</a>
          <a class="badge" href="#">📂 Projects</a>
          <a class="badge" href="#">📺 Demos</a>
        </div>
      </div>

    </div>

  </div>

  <footer>&copy; Khushi Singh — Robotics & Automation | Crafted: Neon Robot Mode • Industrial UI</footer>

  <script>
    // Simple typewriter sequence for terminal box
    const lines = [
      'Initializing ROS2 nodes...',
      'Spawning Gazebo world: robot_lab.world',
      'Starting SLAM -> lidar_scan -> odom',
      'Controller: PID position controller engaged',
      'Simulation heartbeat: OK'
    ];
    let i=0, j=0; const el = document.getElementById('typer');
    function typeNext(){
      if(i>=lines.length)i=0;
      const line = lines[i];
      el.textContent = line.slice(0,j);
      j++;
      if(j>line.length){j=0;i++;setTimeout(typeNext,900)}else setTimeout(typeNext,40);
    }
    typeNext();

    // small accessibility: make PLС LEDs cycle state every few seconds
    (function cyclePLCs(){
      const leds = document.querySelectorAll('.plc .led');
      let idx = 0;
      setInterval(()=>{
        leds.forEach((l,ii)=>{ l.style.opacity = (ii===idx?1:0.35) });
        idx = (idx+1)%leds.length;
      },2300);
    })();
  </script>
</body>
</html>
