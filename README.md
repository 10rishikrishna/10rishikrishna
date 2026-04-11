
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');
  :root { --neon:#00f5ff; --neon2:#bf00ff; --neon3:#ff2d78; --neon4:#00ff88; --neon5:#ffcc00; }
  *{box-sizing:border-box;margin:0;padding:0;}
  @keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
  @keyframes scanline{0%{top:-8%}100%{top:110%}}
  @keyframes matrixFall{0%{transform:translateY(-60px);opacity:0}10%{opacity:.6}90%{opacity:.4}100%{transform:translateY(520px);opacity:0}}
  @keyframes borderRun{0%{background-position:0% 50%}100%{background-position:200% 50%}}
  @keyframes pulseGlow{0%,100%{opacity:.5}50%{opacity:1}}
  @keyframes statBar{from{width:0}to{width:var(--w)}}
  @keyframes neonFlicker{0%,100%{opacity:1}92%{opacity:.9}94%{opacity:.4}96%{opacity:.95}}

  /* Role flash — 5 roles, each shown for ~2s in a 10s loop */
  @keyframes flash1{0%,16%{opacity:1;transform:translateY(0)}18%,100%{opacity:0;transform:translateY(-20px)}}
  @keyframes flash2{0%,17%{opacity:0;transform:translateY(20px)}19%,36%{opacity:1;transform:translateY(0)}38%,100%{opacity:0;transform:translateY(-20px)}}
  @keyframes flash3{0%,37%{opacity:0;transform:translateY(20px)}39%,56%{opacity:1;transform:translateY(0)}58%,100%{opacity:0;transform:translateY(-20px)}}
  @keyframes flash4{0%,57%{opacity:0;transform:translateY(20px)}59%,76%{opacity:1;transform:translateY(0)}78%,100%{opacity:0;transform:translateY(-20px)}}
  @keyframes flash5{0%,77%{opacity:0;transform:translateY(20px)}79%,96%{opacity:1;transform:translateY(0)}98%,100%{opacity:0;transform:translateY(-20px)}}

  .card{background:#07090f;border-radius:18px;overflow:hidden;position:relative;border:1.5px solid #151c2a;font-family:'Share Tech Mono','Courier New',monospace;}
  .card::before{content:'';position:absolute;inset:0;border-radius:18px;padding:1.5px;background:linear-gradient(135deg,#00f5ff55,#bf00ff44,#ff2d7833,#00ff8833,#ffcc0033,#00f5ff55);background-size:300% 300%;animation:borderRun 5s linear infinite;-webkit-mask:linear-gradient(#fff 0 0) content-box,linear-gradient(#fff 0 0);-webkit-mask-composite:xor;mask-composite:exclude;pointer-events:none;}
  .scanline{position:absolute;left:0;right:0;height:10px;background:linear-gradient(to bottom,transparent,#00f5ff12,transparent);animation:scanline 4s linear infinite;pointer-events:none;z-index:10;}
  .matrix-col{position:absolute;top:0;font-size:10px;color:#00f5ff;opacity:.11;user-select:none;pointer-events:none;font-family:'Share Tech Mono',monospace;animation:matrixFall linear infinite;white-space:pre;}
  .inner{padding:26px 26px 20px;position:relative;z-index:2;}

  /* Header */
  .header{display:flex;align-items:flex-start;gap:18px;margin-bottom:20px;animation:fadeUp .5s ease both;}
  .avatar{width:76px;height:76px;border-radius:50%;background:radial-gradient(circle at 35% 35%,#1a2540,#07090f);border:2px solid #00f5ff44;display:flex;align-items:center;justify-content:center;font-size:22px;color:var(--neon);font-weight:700;position:relative;box-shadow:0 0 24px #00f5ff22;animation:neonFlicker 7s ease-in-out infinite;flex-shrink:0;letter-spacing:1px;}
  .avatar::after{content:'';position:absolute;inset:-5px;border-radius:50%;border:1px solid #00f5ff22;animation:pulseGlow 2.8s ease-in-out infinite;}
  .name-block{flex:1;min-width:0;}
  .name{font-size:21px;font-weight:700;color:#e8f4ff;letter-spacing:3px;text-transform:uppercase;}

  /* Flash role slot */
  .role-slot{height:24px;position:relative;overflow:hidden;margin-top:6px;}
  .role-flash{position:absolute;left:0;top:0;font-size:12px;letter-spacing:1px;white-space:nowrap;line-height:24px;opacity:0;}
  .role-flash .pfx{color:#4a5568;margin-right:5px;}
  .rf1{color:var(--neon);  animation:flash1 10s ease-in-out infinite;}
  .rf2{color:var(--neon2); animation:flash2 10s ease-in-out infinite;}
  .rf3{color:var(--neon3); animation:flash3 10s ease-in-out infinite;}
  .rf4{color:var(--neon4); animation:flash4 10s ease-in-out infinite;}
  .rf5{color:var(--neon5); animation:flash5 10s ease-in-out infinite;}

  .tag-row{display:flex;flex-wrap:wrap;gap:5px;margin-top:10px;}
  .tag{font-size:9px;padding:2px 9px;border-radius:20px;background:#0b0f1a;border:1px solid;letter-spacing:.8px;text-transform:uppercase;cursor:default;}
  .tag.c{color:var(--neon);border-color:#00f5ff33;}
  .tag.p{color:var(--neon2);border-color:#bf00ff33;}
  .tag.r{color:var(--neon3);border-color:#ff2d7833;}
  .tag.g{color:var(--neon4);border-color:#00ff8833;}
  .tag.y{color:var(--neon5);border-color:#ffcc0033;}

  .div{height:1px;background:linear-gradient(90deg,transparent,#00f5ff33,#bf00ff33,#ff2d7822,#ffcc0022,transparent);margin:15px 0;}

  .bio{font-size:11.5px;color:#7a8fa8;line-height:1.75;animation:fadeUp .7s ease .2s both;}
  .bio span{color:#a8c8e8;}
  .bio .hi{color:var(--neon4);}

  .sec-label{font-size:9px;color:#3a5070;letter-spacing:2px;text-transform:uppercase;margin-bottom:11px;}

  /* Stats */
  .stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;animation:fadeUp .8s ease .3s both;}
  .stat-card{background:#0b0f1a;border:1px solid #151c2a;border-radius:10px;padding:9px 8px;text-align:center;}
  .stat-num{font-size:19px;font-weight:700;}
  .stat-num.c{color:var(--neon);}
  .stat-num.p{color:var(--neon2);}
  .stat-num.r{color:var(--neon3);}
  .stat-num.g{color:var(--neon4);}
  .stat-lbl{font-size:8px;color:#3a5070;letter-spacing:1px;text-transform:uppercase;margin-top:2px;}

  /* Domain cards — now 3 columns */
  .domain-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;animation:fadeUp .9s ease .4s both;}
  .domain-card{background:#0b0f1a;border:1px solid #151c2a;border-radius:10px;padding:11px 12px;}
  .d-title{font-size:10px;letter-spacing:1.2px;text-transform:uppercase;margin-bottom:6px;display:flex;align-items:center;gap:7px;}
  .d-dot{width:6px;height:6px;border-radius:50%;flex-shrink:0;}
  .d-skills{font-size:9px;color:#4a6080;line-height:1.85;}

  /* Skill bars */
  .skill-list{display:flex;flex-direction:column;gap:8px;animation:fadeUp 1s ease .5s both;}
  .skill-row{display:flex;align-items:center;gap:10px;}
  .skill-name{font-size:10px;color:#7a8fa8;min-width:88px;}
  .skill-bar-bg{flex:1;height:3px;background:#0d1117;border-radius:2px;overflow:hidden;}
  .skill-bar{height:100%;border-radius:2px;width:0;}
  .skill-bar.go{animation:statBar .9s cubic-bezier(.4,0,.2,1) forwards;}
  .skill-pct{font-size:9px;color:#3a5070;min-width:28px;text-align:right;}

  /* Tech */
  .tech-grid{display:flex;flex-wrap:wrap;gap:5px;animation:fadeUp 1s ease .6s both;}
  .tech{font-size:9px;padding:3px 9px;border-radius:6px;background:#0d1117;border:1px solid #151c2a;color:#5a7890;letter-spacing:.4px;transition:border-color .2s,color .2s;cursor:default;}
  .tech:hover{border-color:#00f5ff55;color:var(--neon);}
  .tech.y:hover{border-color:#ffcc0055;color:var(--neon5);}

  /* Footer */
  .footer{display:flex;justify-content:space-between;align-items:center;margin-top:14px;animation:fadeUp 1s ease .7s both;}
  .links{display:flex;gap:12px;}
  .flink{font-size:9px;color:#3a5070;letter-spacing:1px;text-decoration:none;text-transform:uppercase;border-bottom:1px solid transparent;transition:color .2s,border-color .2s;}
  .flink:hover{color:var(--neon);border-color:var(--neon);}
  .status-row{display:flex;align-items:center;gap:5px;font-size:9px;color:#3a5070;}
  .dot{width:5px;height:5px;border-radius:50%;background:#00ff88;box-shadow:0 0 6px #00ff88;animation:pulseGlow 1.8s ease-in-out infinite;}
</style>

<div class="card">
  <div class="scanline"></div>
  <div id="mx"></div>
  <div class="inner">

    <!-- HEADER -->
    <div class="header">
      <div class="avatar">RK</div>
      <div class="name-block">
        <div class="name">Rishi Krishna</div>

        <!-- ALL 5 ROLES FLASHING -->
        <div class="role-slot">
          <div class="role-flash rf1"><span class="pfx">&gt;_</span>Backend Developer</div>
          <div class="role-flash rf2"><span class="pfx">&gt;_</span>Web Developer</div>
          <div class="role-flash rf3"><span class="pfx">&gt;_</span>Cybersecurity Enthusiast</div>
          <div class="role-flash rf4"><span class="pfx">&gt;_</span>Data Analytics</div>
          <div class="role-flash rf5"><span class="pfx">&gt;_</span>🎹 Pianist</div>
        </div>

        <div class="tag-row">
          <span class="tag c">Backend</span>
          <span class="tag p">Web Dev</span>
          <span class="tag r">Cybersecurity</span>
          <span class="tag g">Data Analytics</span>
          <span class="tag y">🎹 Pianist</span>
        </div>
      </div>
    </div>

    <div class="div"></div>

    <!-- BIO -->
    <div class="bio">
      <span class="hi">// 360 contributions</span> · <span>97% commits</span> · <span>18+ repositories</span><br>
      Engineer by day, <span>pianist</span> by soul — building scalable systems,<br>
      securing stacks, turning data into insight, and composing melodies.
    </div>

    <div class="div"></div>

    <!-- GITHUB STATS -->
    <div class="sec-label">// GitHub Activity</div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-num c" id="s1">0</div><div class="stat-lbl">Contributions</div></div>
      <div class="stat-card"><div class="stat-num p" id="s2">0</div><div class="stat-lbl">Repos</div></div>
      <div class="stat-card"><div class="stat-num r" id="s3">0%</div><div class="stat-lbl">Commit Rate</div></div>
      <div class="stat-card"><div class="stat-num g" id="s4">0</div><div class="stat-lbl">PRs & Issues</div></div>
    </div>

    <div class="div"></div>

    <!-- DOMAIN CARDS — 5 domains + pianist -->
    <div class="sec-label">// Domains</div>
    <div class="domain-grid">
      <div class="domain-card">
        <div class="d-title"><div class="d-dot" style="background:var(--neon);box-shadow:0 0 5px var(--neon)"></div><span style="color:var(--neon)">Backend Dev</span></div>
        <div class="d-skills">FastAPI · Node.js · gRPC<br>REST APIs · RabbitMQ<br>PostgreSQL · Redis · AWS</div>
      </div>
      <div class="domain-card">
        <div class="d-title"><div class="d-dot" style="background:var(--neon2);box-shadow:0 0 5px var(--neon2)"></div><span style="color:var(--neon2)">Web Dev</span></div>
        <div class="d-skills">React · HTML · CSS<br>Tailwind · JavaScript<br>Nginx · Vercel · CI/CD</div>
      </div>
      <div class="domain-card">
        <div class="d-title"><div class="d-dot" style="background:var(--neon3);box-shadow:0 0 5px var(--neon3)"></div><span style="color:var(--neon3)">Cybersecurity</span></div>
        <div class="d-skills">Pentesting · OWASP<br>Kali Linux · Wireshark<br>CTF · Network Security</div>
      </div>
      <div class="domain-card">
        <div class="d-title"><div class="d-dot" style="background:var(--neon4);box-shadow:0 0 5px var(--neon4)"></div><span style="color:var(--neon4)">Data Analytics</span></div>
        <div class="d-skills">Pandas · NumPy<br>Matplotlib · Jupyter<br>SQL · Dashboards</div>
      </div>
      <div class="domain-card">
        <div class="d-title"><div class="d-dot" style="background:#4a8f60;box-shadow:0 0 5px #4a8f60"></div><span style="color:#3a7050">DevOps / Cloud</span></div>
        <div class="d-skills">Docker · Kubernetes<br>AWS · Linux · Git<br>CI/CD · Nginx</div>
      </div>
      <div class="domain-card" style="border-color:#ffcc0022;">
        <div class="d-title"><div class="d-dot" style="background:var(--neon5);box-shadow:0 0 5px var(--neon5)"></div><span style="color:var(--neon5)">🎹 Pianist</span></div>
        <div class="d-skills">Classical · Jazz<br>Music Theory · Improvisation<br>Composition · Ear Training</div>
      </div>
    </div>

    <div class="div"></div>

    <!-- SKILL BARS — all 6 -->
    <div class="sec-label">// Proficiency</div>
    <div class="skill-list">
      <div class="skill-row"><span class="skill-name">Backend / APIs</span><div class="skill-bar-bg"><div class="skill-bar" style="--w:92%;background:linear-gradient(90deg,#00f5ff,#0088cc)"></div></div><span class="skill-pct">92%</span></div>
      <div class="skill-row"><span class="skill-name">Web Dev</span><div class="skill-bar-bg"><div class="skill-bar" style="--w:80%;background:linear-gradient(90deg,#bf00ff,#6600cc)"></div></div><span class="skill-pct">80%</span></div>
      <div class="skill-row"><span class="skill-name">Cybersecurity</span><div class="skill-bar-bg"><div class="skill-bar" style="--w:72%;background:linear-gradient(90deg,#ff2d78,#cc0044)"></div></div><span class="skill-pct">72%</span></div>
      <div class="skill-row"><span class="skill-name">Data Analytics</span><div class="skill-bar-bg"><div class="skill-bar" style="--w:76%;background:linear-gradient(90deg,#00ff88,#009955)"></div></div><span class="skill-pct">76%</span></div>
      <div class="skill-row"><span class="skill-name">DevOps / Cloud</span><div class="skill-bar-bg"><div class="skill-bar" style="--w:78%;background:linear-gradient(90deg,#00f5ff,#bf00ff)"></div></div><span class="skill-pct">78%</span></div>
      <div class="skill-row"><span class="skill-name">🎹 Piano</span><div class="skill-bar-bg"><div class="skill-bar" style="--w:85%;background:linear-gradient(90deg,#ffcc00,#ff8800)"></div></div><span class="skill-pct">85%</span></div>
    </div>

    <div class="div"></div>

    <!-- TECH STACK -->
    <div class="sec-label">// Full Stack</div>
    <div class="tech-grid">
      <span class="tech">Python</span><span class="tech">FastAPI</span><span class="tech">Node.js</span><span class="tech">Express</span>
      <span class="tech">React</span><span class="tech">JavaScript</span><span class="tech">HTML/CSS</span><span class="tech">Tailwind</span>
      <span class="tech">PostgreSQL</span><span class="tech">MongoDB</span><span class="tech">Redis</span>
      <span class="tech">Docker</span><span class="tech">Kubernetes</span><span class="tech">AWS</span><span class="tech">Linux</span>
      <span class="tech">Kali Linux</span><span class="tech">Wireshark</span><span class="tech">OWASP</span>
      <span class="tech">Pandas</span><span class="tech">NumPy</span><span class="tech">Matplotlib</span><span class="tech">Jupyter</span>
      <span class="tech">Git</span><span class="tech">Nginx</span><span class="tech">RabbitMQ</span><span class="tech">GraphQL</span>
      <span class="tech y" style="border-color:#ffcc0033;color:#aa8800;">🎹 Piano</span>
      <span class="tech y" style="border-color:#ffcc0033;color:#aa8800;">Music Theory</span>
      <span class="tech y" style="border-color:#ffcc0033;color:#aa8800;">Composition</span>
    </div>

    <!-- FOOTER -->
    <div class="footer">
      <div class="links">
        <a class="flink" href="#">GitHub</a>
        <a class="flink" href="#">LinkedIn</a>
        <a class="flink" href="#">Portfolio</a>
        <a class="flink" href="#">Email</a>
      </div>
      <div class="status-row"><div class="dot"></div>Open to Opportunities</div>
    </div>

  </div>
</div>

<script>
// Matrix rain
const mc=document.getElementById('mx');
const chars='01アイウエカキΩλ∑∂∇♩♪♫♬'.split('');
for(let i=0;i<16;i++){
  const c=document.createElement('div');
  c.className='matrix-col';
  c.style.cssText=`left:${2+i*6.2}%;animation-duration:${2.2+Math.random()*3.5}s;animation-delay:${-Math.random()*5}s;font-size:${9+Math.random()*3}px`;
  c.textContent=Array.from({length:24},()=>chars[Math.floor(Math.random()*chars.length)]).join('\n');
  mc.appendChild(c);
}
// Count-up
function countUp(el,target,suffix,dur){
  dur=dur||1300;let cur=0;const inc=target/(dur/16);
  const t=setInterval(()=>{cur=Math.min(cur+inc,target);el.textContent=Math.floor(cur)+(suffix||'');if(cur>=target)clearInterval(t);},16);
}
setTimeout(()=>{
  countUp(document.getElementById('s1'),360);
  countUp(document.getElementById('s2'),18);
  countUp(document.getElementById('s3'),97,'%');
  countUp(document.getElementById('s4'),21);
},500);
// Skill bars
setTimeout(()=>{document.querySelectorAll('.skill-bar').forEach(b=>b.classList.add('go'));},700);
</script>
