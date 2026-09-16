<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Simulado V/F — Parasitologia (Prova Prática)</title>
<style>
:root{
  --bg:#f5f7fa; --card:#ffffff; --ink:#18212b; --muted:#66717d;
  --accent:#315f8a; --accent2:#e8f0f7; --line:#dfe5eb;
  --ok:#287a4b; --ok-bg:#e7f4ec; --ok-line:#287a4b;
  --err:#b3312a; --err-bg:#fbeae8; --err-line:#b3312a;
  --warn:#d97706;
}
*{box-sizing:border-box}
html{scroll-behavior:smooth}
body{
  margin:0;font-family:Arial,Helvetica,sans-serif;
  background:var(--bg);color:var(--ink);line-height:1.55;
}
header{
  background:linear-gradient(135deg,#17324b,#315f8a);
  color:#fff;padding:26px 20px;
}
header .wrap{max-width:840px;margin:auto}
h1{margin:0 0 6px;font-size:24px;letter-spacing:.2px}
header p{margin:0;opacity:.92;font-size:14px}
.wrap{max-width:840px;margin:auto;padding:20px}

.hud{
  position:sticky;top:0;z-index:20;
  background:rgba(255,255,255,.96);
  backdrop-filter:blur(8px);
  border:1px solid var(--line);
  border-radius:14px;
  padding:12px 16px;
  margin-bottom:18px;
  display:flex;align-items:center;gap:12px;flex-wrap:wrap;
  box-shadow:0 6px 18px rgba(20,35,50,.08);
}
.hud .pill{
  background:var(--accent2);color:var(--accent);
  padding:5px 12px;border-radius:999px;
  font-weight:800;font-size:14px;white-space:nowrap;
}
.hud .progress{
  flex:1;min-width:120px;height:9px;
  background:#e9edf1;border-radius:999px;overflow:hidden;
}
.hud .progress > div{
  height:100%;width:0;
  background:linear-gradient(90deg,#315f8a,#4d86b8);
  transition:width .35s ease;
}
.sound-toggle{
  flex-shrink:0;width:40px;height:40px;
  border:1px solid var(--line);background:#fff;
  border-radius:10px;font-size:18px;line-height:1;
  cursor:pointer;display:flex;align-items:center;justify-content:center;
  transition:all .15s ease;font-family:inherit;padding:0;
}
.sound-toggle:hover{border-color:var(--accent);background:var(--accent2);transform:translateY(-1px)}
.sound-toggle.muted{opacity:.5;filter:grayscale(1)}

.card{
  background:var(--card);border:1px solid var(--line);
  border-radius:18px;overflow:hidden;margin-bottom:18px;
  box-shadow:0 5px 18px rgba(20,35,50,.07);transition:box-shadow .3s;
}
.card.flash-ok{animation:flashOk .9s ease}
.card.flash-err{animation:flashErr .9s ease}
@keyframes flashOk{0%,100%{box-shadow:0 5px 18px rgba(20,35,50,.07)}40%{box-shadow:0 0 0 5px rgba(40,122,75,.35)}}
@keyframes flashErr{0%,100%{box-shadow:0 5px 18px rgba(20,35,50,.07)}40%{box-shadow:0 0 0 5px rgba(179,49,42,.35)}}

.photo{height:240px;background:#eef1f3;display:flex;align-items:center;justify-content:center;overflow:hidden;position:relative}
.photo img{width:100%;height:100%;object-fit:contain}
.photo.noimg::after{content:"Imagem indisponível";color:var(--muted);font-weight:700;font-size:14px}

.content{padding:18px 20px 22px}
.num{font-size:12px;color:var(--accent);font-weight:800;text-transform:uppercase;letter-spacing:.1em}
.statement{font-size:16.5px;margin:8px 0 14px;line-height:1.55}
.statement i{color:#2a4a6b}

.timer-display{display:flex;align-items:center;gap:10px;padding:10px 14px;margin-bottom:14px;background:#f7f9fb;border:1px solid var(--line);border-radius:10px}
.timer-display .t-label{font-size:12px;font-weight:800;color:var(--muted);text-transform:uppercase;letter-spacing:.08em;white-space:nowrap}
.timer-display .t-bar{flex:1;min-width:70px;height:8px;background:#e9edf1;border-radius:999px;overflow:hidden}
.timer-display .t-bar > div{height:100%;width:100%;background:var(--ok);transition:width .95s linear, background .3s linear}
.timer-display .t-value{font-weight:800;font-size:22px;color:var(--ok);min-width:52px;text-align:right;font-variant-numeric:tabular-nums}
.timer-display.warn .t-value{color:var(--warn)}
.timer-display.warn .t-bar > div{background:var(--warn)}
.timer-display.danger .t-value{color:var(--err)}
.timer-display.danger .t-bar > div{background:var(--err)}

.vf{display:flex;gap:10px;flex-wrap:wrap}
.vf button{flex:1;min-width:130px;border:2px solid var(--line);background:#fff;color:var(--ink);padding:12px 16px;border-radius:10px;font-weight:800;font-size:15px;cursor:pointer;transition:all .15s ease;font-family:inherit}
.vf button:hover:not(:disabled){border-color:var(--accent);color:var(--accent);transform:translateY(-1px)}
.vf button:disabled{cursor:default;opacity:.95}
.vf button.correct{background:var(--ok-bg);border-color:var(--ok);color:var(--ok)}
.vf button.wrong{background:var(--err-bg);border-color:var(--err);color:var(--err)}

.feedback{display:none;margin-top:14px;padding:14px 16px;border-radius:12px;border-left:5px solid;background:#f7f9fb;font-size:15px}
.feedback.show{display:block;animation:fadeIn .25s ease}
@keyframes fadeIn{from{opacity:0;transform:translateY(-4px)}to{opacity:1;transform:none}}
.feedback.ok{background:var(--ok-bg);border-color:var(--ok-line)}
.feedback.err{background:var(--err-bg);border-color:var(--err-line)}
.fb-head{font-weight:800;margin-bottom:6px;font-size:16px}
.feedback.ok .fb-head{color:var(--ok)}
.feedback.err .fb-head{color:var(--err)}
.fb-body p{margin:6px 0}
.fb-body .resp{font-weight:800;padding:6px 10px;border-radius:8px;background:rgba(255,255,255,.6);display:inline-block;margin-bottom:6px}

.next-wrap{display:none;justify-content:center;margin-top:18px}
.next-wrap.show{display:flex;animation:fadeIn .3s ease}
.next-wrap button{border:0;border-radius:12px;padding:14px 34px;background:var(--accent);color:#fff;font-weight:800;font-size:16px;cursor:pointer;box-shadow:0 6px 18px rgba(49,95,138,.35);transition:transform .15s;font-family:inherit}
.next-wrap button:hover{transform:translateY(-2px)}

.study-overlay{position:fixed;inset:0;z-index:100;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:24px;background:rgba(150,25,20,.9);color:#fff;opacity:0;pointer-events:none;transition:opacity .3s ease}
.study-overlay.show{opacity:1;pointer-events:auto}
.study-overlay h2{margin:0;font-size:clamp(52px,15vw,150px);font-weight:900;letter-spacing:.06em;text-shadow:0 8px 40px rgba(0,0,0,.45);animation:pulseStudy 1.5s ease-in-out infinite;line-height:1}
.study-overlay .sub{margin:16px 0 0;font-size:clamp(15px,3.4vw,20px);opacity:.95;max-width:640px}
.study-overlay .countdown{margin-top:30px;font-size:clamp(30px,7vw,52px);font-weight:800;font-variant-numeric:tabular-nums;padding:8px 26px;border-radius:999px;background:rgba(0,0,0,.22)}
@keyframes pulseStudy{0%,100%{transform:scale(1)}50%{transform:scale(1.06)}}

.results{text-align:center;padding:34px 20px;background:#fff;border:1px solid var(--line);border-radius:18px;box-shadow:0 5px 18px rgba(20,35,50,.07)}
.results h2{font-size:26px;margin:0 0 10px;color:var(--accent)}
.results .big{font-size:56px;font-weight:900;color:var(--ok);margin:10px 0;font-variant-numeric:tabular-nums}
.results p{color:var(--muted);margin:8px 0 22px}
.results button{border:0;border-radius:12px;padding:14px 30px;background:var(--accent);color:#fff;font-weight:800;font-size:16px;cursor:pointer;box-shadow:0 6px 18px rgba(49,95,138,.35);font-family:inherit}

/* ================= TELA DE ABERTURA ================= */
.intro{position:fixed;inset:0;z-index:60;display:flex;align-items:flex-start;justify-content:center;padding:22px;overflow-y:auto;background:#0f2438;transition:opacity .45s ease, visibility .45s ease}
.intro.hide{opacity:0;visibility:hidden;pointer-events:none}

.intro-bg{position:absolute;inset:0;background:url("https://i.pinimg.com/736x/e7/d5/88/e7d588df6145632065c050f0df40c27e.jpg") center/cover no-repeat;filter:blur(9px) brightness(.5) saturate(1.15);transform:scale(1.12)}
.intro::after{content:"";position:absolute;inset:0;background:radial-gradient(circle at 50% 0%,rgba(49,95,138,.5),rgba(9,20,32,.88))}

.intro-card{position:relative;z-index:2;margin:auto;width:100%;max-width:600px;background:var(--card);border-radius:22px;overflow:hidden;box-shadow:0 26px 60px rgba(4,12,20,.6);animation:introUp .65s cubic-bezier(.2,.8,.3,1) both}
@keyframes introUp{from{opacity:0;transform:translateY(22px) scale(.97)}to{opacity:1;transform:none}}

.intro-hero{position:relative;height:220px;background:#17324b}
.intro-hero img{width:100%;height:100%;object-fit:cover;display:block}
.intro-hero::after{content:"";position:absolute;inset:0;background:linear-gradient(180deg,rgba(15,36,56,.10) 25%,rgba(15,36,56,.94))}

.music-badge{position:absolute;top:14px;right:14px;z-index:3;width:38px;height:38px;background:rgba(255,255,255,.22);border:1px solid rgba(255,255,255,.45);border-radius:50%;display:flex;align-items:center;justify-content:center;backdrop-filter:blur(6px);opacity:0;transform:scale(.6);transition:opacity .35s ease, transform .35s ease;pointer-events:none}
.music-badge.show{opacity:1;transform:scale(1)}
.music-badge .note{font-size:18px;color:#fff;animation:musicPulse 1.1s ease-in-out infinite;line-height:1}
@keyframes musicPulse{0%,100%{transform:translateY(0) scale(1)}50%{transform:translateY(-3px) scale(1.18)}}

/* Aviso de autoplay bloqueado */
.autoplay-hint{
  position:absolute;bottom:14px;right:14px;z-index:3;
  background:rgba(0,0,0,.55);
  color:#fff;font-size:12px;font-weight:700;
  padding:7px 12px;border-radius:999px;
  border:1px solid rgba(255,255,255,.35);
  backdrop-filter:blur(6px);
  display:flex;align-items:center;gap:6px;
  opacity:0;transform:translateY(8px);
  transition:opacity .3s ease, transform .3s ease;
  pointer-events:none;
}
.autoplay-hint.show{opacity:1;transform:translateY(0)}
.autoplay-hint .dot{
  width:8px;height:8px;border-radius:50%;
  background:#ffcc4d;
  animation:hintPulse 1.2s ease-in-out infinite;
}
@keyframes hintPulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(.8)}}

.hero-text{position:absolute;left:0;right:0;bottom:0;z-index:2;padding:0 22px 18px;color:#fff}
.hero-tag{display:inline-block;font-size:11px;font-weight:800;letter-spacing:.16em;text-transform:uppercase;background:rgba(255,255,255,.18);border:1px solid rgba(255,255,255,.35);padding:4px 11px;border-radius:999px;backdrop-filter:blur(4px)}
.hero-text h2{margin:9px 0 0;font-size:26px;line-height:1.15;letter-spacing:.4px;text-shadow:0 3px 16px rgba(0,0,0,.55)}

.intro-body{padding:22px 24px 28px;text-align:center}
.intro-lead{margin:0 0 18px;color:var(--muted);font-size:14.5px;line-height:1.6}
.intro-author{display:flex;align-items:center;gap:13px;text-align:left;background:var(--accent2);border:1px solid #d5e3f0;border-radius:14px;padding:12px 14px;margin-bottom:16px}
.avatar{width:46px;height:46px;flex:0 0 46px;border-radius:50%;background:linear-gradient(135deg,#17324b,#4d86b8);color:#fff;font-weight:900;font-size:20px;display:flex;align-items:center;justify-content:center;box-shadow:0 4px 12px rgba(23,50,75,.35)}
.author-txt{display:flex;flex-direction:column;line-height:1.3}
.author-txt span{font-size:11.5px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--muted)}
.author-txt strong{font-size:17px;color:var(--accent)}
.intro-wish{margin:0 0 16px;font-size:15px;font-weight:700;color:var(--ink)}
.intro-rules{list-style:none;margin:0 0 20px;padding:0;text-align:left;display:grid;gap:8px}
.intro-rules li{position:relative;background:#f7f9fb;border:1px solid var(--line);border-radius:10px;padding:9px 12px 9px 34px;font-size:13.5px;color:var(--muted)}
.intro-rules li::before{content:"✓";position:absolute;left:12px;top:50%;transform:translateY(-50%);color:var(--accent);font-weight:900}
.intro-rules li b{color:var(--ink)}

#startBtn{width:100%;border:0;border-radius:13px;padding:15px 26px;background:linear-gradient(135deg,#17324b,#315f8a);color:#fff;font-weight:800;font-size:16.5px;font-family:inherit;cursor:pointer;box-shadow:0 10px 24px rgba(49,95,138,.4);transition:transform .15s ease, box-shadow .2s ease}
#startBtn:hover{transform:translateY(-2px);box-shadow:0 14px 28px rgba(49,95,138,.5)}
#startBtn:active{transform:translateY(0)}

.intro-hint{margin:12px 0 0;font-size:12px;color:var(--muted)}
.intro-hint b{color:var(--accent)}

.actions{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin:6px 0 40px}
.actions button{border:0;border-radius:10px;padding:11px 20px;background:var(--accent);color:#fff;font-weight:800;font-size:14px;cursor:pointer;box-shadow:0 4px 12px rgba(49,95,138,.28);transition:transform .15s;font-family:inherit}
.actions button:hover{transform:translateY(-1px)}
.actions button.ghost{background:#fff;color:var(--accent);border:2px solid var(--accent);box-shadow:none}

footer{color:var(--muted);font-size:12px;padding:24px 20px 40px;text-align:center}
footer b{color:var(--accent)}

@media(max-width:600px){
  h1{font-size:20px}
  header{padding:22px 16px}
  .wrap{padding:14px}
  .photo{height:200px}
  .statement{font-size:15.5px}
  .vf button{min-width:0;padding:11px 12px;font-size:14px}
  .timer-display .t-value{font-size:19px;min-width:44px}
  .sound-toggle{width:36px;height:36px;font-size:16px}
  .intro{padding:14px}
  .intro-hero{height:160px}
  .hero-text{padding:0 18px 14px}
  .hero-text h2{font-size:21px}
  .intro-body{padding:18px 18px 22px}
  .intro-lead{font-size:13.5px}
  .avatar{width:40px;height:40px;flex:0 0 40px;font-size:17px}
  .author-txt strong{font-size:15.5px}
  .music-badge{width:32px;height:32px;top:10px;right:10px}
  .music-badge .note{font-size:15px}
  .autoplay-hint{font-size:11px;padding:6px 10px;bottom:10px;right:10px}
}
</style>
</head>
<body>

<!-- ===================== TELA DE ABERTURA ===================== -->
<section class="intro" id="introScreen">
  <div class="intro-bg" aria-hidden="true"></div>
  <div class="intro-card">
    <div class="intro-hero">
      <img src="https://i.pinimg.com/736x/e7/d5/88/e7d588df6145632065c050f0df40c27e.jpg" alt="Ilustração de estudos e microscopia">
      <div class="music-badge" id="musicBadge" aria-hidden="true"><span class="note">♪</span></div>
      <div class="autoplay-hint" id="autoplayHint" aria-hidden="true">
        <span class="dot"></span>
        <span>Toque para ativar o som</span>
      </div>
      <div class="hero-text">
        <span class="hero-tag">Prova prática</span>
        <h2>Simulado V/F<br>Parasitologia</h2>
      </div>
    </div>
    <div class="intro-body">
      <p class="intro-lead">Imagens de lâminas e estruturas parasitárias para treinar o reconhecimento rápido — do jeito que cai na prova prática.</p>
      <div class="intro-author">
        <div class="avatar" aria-hidden="true">W</div>
        <div class="author-txt">
          <span>Material de reforço desenvolvido por</span>
          <strong>Aluno Wesley</strong>
        </div>
      </div>
      <p class="intro-wish">Bons estudos! Que este material ajude você a fixar cada detalhe. 🍀</p>
      <ul class="intro-rules">
        <li><b>14 questões</b> de Verdadeiro ou Falso</li>
        <li><b>10 s</b> para responder cada uma</li>
        <li>Errou? Overlay <b>“ESTUDE MAIS”</b> por 5 s com correção, <b>som e vibração</b></li>
        <li>Toque em <b>“Iniciar”</b> para ativar o som (necessário no iPhone)</li>
      </ul>
      <button type="button" id="startBtn">Iniciar simulado →</button>
      <p class="intro-hint">🎵 <b>Toque na tela</b> para ativar a vinheta • use <b>V</b> / <b>F</b> para responder</p>
    </div>
  </div>
</section>

<header>
  <div class="wrap">
    <h1>Simulado V/F — Parasitologia</h1>
    <p>Uma questão por vez • 10 s para responder • acerto: +10 s • erro: “ESTUDE MAIS” por 5 s</p>
  </div>
</header>

<main class="wrap">
  <div class="hud">
    <span class="pill" id="scorePill">Acertos: 0 / 0</span>
    <span class="pill" id="progressPill">Progresso: 0 / 0</span>
    <div class="progress"><div id="progressFill"></div></div>
    <button class="sound-toggle" id="soundToggle" type="button" aria-label="Alternar som" title="Ligar/desligar som">🔊</button>
  </div>
  <div id="quiz"></div>
  <div class="actions">
    <button class="ghost" id="resetBtn" type="button">Refazer simulado</button>
  </div>
</main>

<div class="study-overlay" id="studyOverlay" aria-hidden="true">
  <h2>ESTUDE MAIS</h2>
  <p class="sub">Você errou esta. A leitura da correção vem em instantes…</p>
  <div class="countdown" id="studyCountdown">5s</div>
</div>

<footer>
  Material de revisão acadêmica — Parasitologia · Desenvolvido por <b>Aluno Wesley</b>.<br>
  Imagens de fontes educacionais externas.
</footer>

<script>
/* ============================ BANCO DE QUESTÕES ============================ */
const questions = [
  {
    img: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjyh_RmxJYkX01LenvU4zyG0vSXd4MWiolRwxVXb5iqVEIqplMvc46YRGhvdprFZSQ8Zaf5IRArdnZ2f9iqRgyS8afnqPGbq2lcerLfx6ew3k00URvPdyzagqXVbRkuZ2Dm9SqCGb8gODMp/s1600/Tenia_solium_scolex.jpg",
    alt: "Taenia solium — escólex",
    statement: "A imagem mostra um <b>cisticerco de <i>Taenia solium</i></b>, com escólex invaginado contendo 4 ventosas e rostelo armado com acúleos.",
    answer: true,
    explanation: "Correto! O cisticerco de <i>T. solium</i> é uma vesícula translúcida com <b>escólex invaginado</b>, <b>4 ventosas</b> e <b>rostelo com acúleos</b>. É essa presença de acúleos que diferencia <i>T. solium</i> de <i>T. saginata</i> (rostelo inerme, sem acúleos)."
  },
  {
    img: "https://image2.slideserve.com/5137844/giardia-lamblia-l.jpg",
    alt: "Giardia lamblia — trofozoíto",
    statement: "A imagem mostra o <b>trofozoíto de <i>Giardia lamblia</i></b>, com formato piriforme, 2 núcleos e 4 pares de flagelos.",
    answer: true,
    explanation: "Correto! O trofozoíto de <i>Giardia</i> tem forma <b>piriforme</b> (em pera), simetria bilateral, <b>2 núcleos</b> (aspecto de 'rosto'), corpos medianos e <b>4 pares de flagelos</b>."
  },
  {
    img: "https://www.researchgate.net/profile/Dennis-Mans/publication/316191566/figure/fig7/AS:492772266639360@1494460283301/Macrophage-infected-with-Leishmania-spp-clearly-showing-nuclei-and-kinetoplasts.png",
    alt: "Leishmania — amastigotas em macrófago",
    statement: "A imagem mostra <b>tripomastigotas de <i>Trypanosoma cruzi</i></b> no interior de macrófagos.",
    answer: false,
    explanation: "Errado. A imagem mostra <b>amastigotas de <i>Leishmania</i> sp.</b> dentro de macrófagos — formas arredondadas/ovais, com <b>núcleo</b> e <b>cinetoplasto</b> (pequeno ponto). Já <i>T. cruzi</i> na fase <b>tripomastigota</b> tem forma alongada, flagelo e membrana ondulante, e circula no <b>sangue</b>, não dentro de macrófagos."
  },
  {
    img: "https://www.cdc.gov/dpdx/images/ascariasis/Ascaris_egg_fert_embryo.jpg",
    alt: "Ascaris lumbricoides — ovo fértil",
    statement: "A imagem mostra um <b>ovo fértil de <i>Ascaris lumbricoides</i></b>, com casca espessa e camada mamilonada externa.",
    answer: true,
    explanation: "Correto! O ovo fértil de <i>A. lumbricoides</i> tem <b>casca espessa</b> e a característica <b>camada mamilonada</b> (albuminosa) externa, que dá o aspecto rugoso/corrugado. Ovo infértil é mais alongado e tem camada mamilonada irregular ou ausente."
  },
  {
    img: "https://static.mundoeducacao.uol.com.br/mundoeducacao/2021/08/schistosoma-mansoni.jpg",
    alt: "Schistosoma mansoni — vermes adultos",
    statement: "A imagem mostra <b>vermes adultos de <i>Schistosoma mansoni</i></b>, com o macho mais robusto e a fêmea mais fina alojada no canal ginecóforo.",
    answer: true,
    explanation: "Correto! No casal de <i>S. mansoni</i>, o <b>macho é mais largo</b> e apresenta o <b>canal ginecóforo</b>, onde a <b>fêmea</b> (mais fina e longa) fica alojada. Essa morfologia em 'casal abraçado' é a grande pista de prova."
  },
  {
    img: "https://pbs.twimg.com/media/GDvYFusW8AAA8rj.jpg",
    alt: "Entamoeba coli — cisto",
    statement: "A imagem mostra um <b>cisto de <i>Entamoeba histolytica</i></b>, com 4 núcleos, forma infectante clássica dessa espécie.",
    answer: false,
    explanation: "Errado. A imagem mostra um <b>cisto de <i>Entamoeba coli</i></b>, que possui <b>mais de 4 núcleos</b> (geralmente até 8). O cisto de <i>E. histolytica</i> tem <b>no máximo 4 núcleos</b>. Regra de ouro: cisto com mais de 4 núcleos → <i>E. coli</i>."
  },
  {
    img: "https://files.cercomp.ufg.br/weby/up/486/o/P_falciparum_2.jpg",
    alt: "Plasmodium — trofozoítos em anel",
    statement: "A imagem mostra <b>trofozoítos de <i>Plasmodium</i> sp.</b> em forma de anel ('anel de sinete') no interior de hemácias.",
    answer: true,
    explanation: "Correto! As formas em anel são <b>trofozoítos jovens de <i>Plasmodium</i></b>, com a cromatina (núcleo) e o citoplasma formando um anel dentro da hemácia. Pista: primeiro ache a hemácia; depois procure o pequeno anel arroxeado dentro dela."
  },
  {
    img: "https://image2.slideserve.com/5137844/giardia-lamblia-l.jpg",
    alt: "Giardia lamblia — trofozoíto",
    statement: "A imagem mostra o <b>cisto de <i>Giardia lamblia</i></b>, forma oval com parede cística espessa e 4 núcleos.",
    answer: false,
    explanation: "Errado. A imagem é do <b>trofozoíto</b> de <i>Giardia</i> (piriforme, 2 núcleos, flagelos). O <b>cisto</b> de <i>Giardia</i> é <b>oval</b>, com <b>parede cística espessa</b> e <b>4 núcleos</b> — é a forma infectante, eliminada nas fezes."
  },
  {
    img: "https://www.researchgate.net/profile/Dennis-Mans/publication/316191566/figure/fig7/AS:492772266639360@1494460283301/Macrophage-infected-with-Leishmania-spp-clearly-showing-nuclei-and-kinetoplasts.png",
    alt: "Leishmania — amastigotas em macrófago",
    statement: "As formas arredondadas intracelulares apresentam <b>núcleo e cinetoplasto</b>, sendo compatíveis com <b>amastigotas de <i>Leishmania</i> sp.</b>",
    answer: true,
    explanation: "Correto! Amastigotas de <i>Leishmania</i> são formas <b>arredondadas/ovais</b>, <b>intracelulares</b> (dentro de macrófagos), com <b>núcleo</b> e <b>cinetoplasto</b> (pequeno ponto ao lado do núcleo). Esse é o padrão clássico em lâminas de Leishmaniose."
  },
  {
    img: "https://www.cdc.gov/dpdx/images/ascariasis/Ascaris_egg_fert_embryo.jpg",
    alt: "Ascaris lumbricoides — ovo",
    statement: "A imagem mostra um <b>ovo infértil de <i>Ascaris lumbricoides</i></b>, sem camada mamilonada.",
    answer: false,
    explanation: "Errado. A imagem mostra um ovo <b>fértil</b> de <i>A. lumbricoides</i>, com casca espessa e <b>camada mamilonada bem evidente</b>. O ovo <b>infértil</b> é mais alongado e tem camada mamilonada irregular ou ausente."
  },
  {
    img: "https://static.mundoeducacao.uol.com.br/mundoeducacao/2021/08/schistosoma-mansoni.jpg",
    alt: "Schistosoma mansoni — vermes adultos",
    statement: "A imagem mostra o casal de <b><i>Taenia solium</i></b>, com proglotes e escólex.",
    answer: false,
    explanation: "Errado. A imagem mostra <b>vermes adultos de <i>Schistosoma mansoni</i></b> (macho robusto + fêmea fina no canal ginecóforo). <i>Taenia</i> é um <b>cestódeo</b>, com corpo segmentado em <b>proglotes</b> — morfologia completamente diferente."
  },
  {
    img: "https://files.cercomp.ufg.br/weby/up/486/o/P_falciparum_2.jpg",
    alt: "Plasmodium — trofozoítos em anel",
    statement: "Os parasitos visualizados estão no <b>plasma sanguíneo</b>, fora das hemácias.",
    answer: false,
    explanation: "Errado. Os trofozoítos em anel de <i>Plasmodium</i> estão <b>dentro das hemácias</b> (hemácias parasitadas). Na fase eritrocítica do ciclo, o parasito invade o eritrócito e se desenvolve no seu interior — é justamente isso que se procura na lâmina."
  },
  {
    img: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjyh_RmxJYkX01LenvU4zyG0vSXd4MWiolRwxVXb5iqVEIqplMvc46YRGhvdprFZSQ8Zaf5IRArdnZ2f9iqRgyS8afnqPGbq2lcerLfx6ew3k00URvPdyzagqXVbRkuZ2Dm9SqCGb8gODMp/s1600/Tenia_solium_scolex.jpg",
    alt: "Taenia solium — escólex",
    statement: "O escólex mostrado é compatível com <b><i>Taenia solium</i></b>, pois apresenta rostelo armado com acúleos.",
    answer: true,
    explanation: "Correto! A presença de <b>rostelo com acúleos</b> (rostelo armado) é a característica que diferencia <i>T. solium</i> de <i>T. saginata</i> (rostelo <b>inerme</b>, sem acúleos). Se a lâmina mostra acúleos, é <i>T. solium</i>."
  },
  {
    img: "https://pbs.twimg.com/media/GDvYFusW8AAA8rj.jpg",
    alt: "Entamoeba coli — cisto",
    statement: "Cistos com <b>mais de 4 núcleos</b> são sugestivos de <b><i>Entamoeba coli</i></b>.",
    answer: true,
    explanation: "Correto! Cistos com <b>mais de 4 núcleos</b> (até 8) são característicos de <i>E. coli</i>. <i>E. histolytica</i> tem no máximo <b>4 núcleos</b> no cisto maduro. Essa é uma das diferenciações mais cobradas em prova prática."
  }
];

/* ================================ ESTADO ================================ */
const ANSWER_TIME  = 10;
const CORRECT_WAIT = 5;
const WRONG_WAIT   = 5;

const quizEl         = document.getElementById('quiz');
const scorePill      = document.getElementById('scorePill');
const progressPill   = document.getElementById('progressPill');
const progressFill   = document.getElementById('progressFill');
const studyOverlay   = document.getElementById('studyOverlay');
const studyCountdown = document.getElementById('studyCountdown');
const introScreen    = document.getElementById('introScreen');
const startBtn       = document.getElementById('startBtn');
const soundToggle    = document.getElementById('soundToggle');
const musicBadge     = document.getElementById('musicBadge');
const autoplayHint   = document.getElementById('autoplayHint');
const total          = questions.length;

let score = 0, answered = 0, currentIndex = 0, activeTimer = null;

function clearActiveTimer() {
  if (activeTimer) { clearInterval(activeTimer); activeTimer = null; }
}

/* ====================== VIBRAÇÃO (Android) ====================== */
const supportsVibrate = ('vibrate' in navigator);
function vibrate(p) { if (!supportsVibrate) return; try { navigator.vibrate(p); } catch(e){} }
function stopVibrate() { if (!supportsVibrate) return; try { navigator.vibrate(0); } catch(e){} }

/* ====================== ÁUDIO (Web Audio API) ====================== */
let audioCtx = null;
let activeOscillators = [];

const safeStorage = {
  get(k){ try { return localStorage.getItem(k); } catch(e){ return null; } },
  set(k,v){ try { localStorage.setItem(k,v); } catch(e){} }
};

let soundEnabled = safeStorage.get('pq_sound') !== 'off';

function initAudio() {
  try {
    const AC = window.AudioContext || window.webkitAudioContext;
    if (!AC) { audioCtx = null; return; }
    if (!audioCtx) audioCtx = new AC();
    if (audioCtx.state === 'suspended') audioCtx.resume().catch(()=>{});
  } catch (e) { audioCtx = null; }
}

function trackSource(src) {
  activeOscillators.push(src);
  src.onended = () => {
    const i = activeOscillators.indexOf(src);
    if (i >= 0) activeOscillators.splice(i, 1);
  };
}

function stopAllSounds() {
  activeOscillators.forEach(s => { try { s.stop(); } catch(e){} });
  activeOscillators = [];
}

/* ---------- Bateria / Instrumentos ---------- */
let _snareBuf = null, _hihatBuf = null;
function getNoiseBuf(type) {
  if (!audioCtx) return null;
  if (type === 'snare') {
    if (_snareBuf) return _snareBuf;
    const dur = 0.18;
    _snareBuf = audioCtx.createBuffer(1, Math.floor(audioCtx.sampleRate*dur), audioCtx.sampleRate);
    const d = _snareBuf.getChannelData(0);
    for (let i=0;i<d.length;i++) d[i] = (Math.random()*2-1) * (1 - i/d.length);
    return _snareBuf;
  }
  if (type === 'hihat') {
    if (_hihatBuf) return _hihatBuf;
    const dur = 0.045;
    _hihatBuf = audioCtx.createBuffer(1, Math.floor(audioCtx.sampleRate*dur), audioCtx.sampleRate);
    const d = _hihatBuf.getChannelData(0);
    for (let i=0;i<d.length;i++) d[i] = Math.random()*2-1;
    return _hihatBuf;
  }
}

function playKick(t, vol) {
  const osc = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  osc.type = 'sine';
  osc.frequency.setValueAtTime(150, t);
  osc.frequency.exponentialRampToValueAtTime(45, t+0.13);
  g.gain.setValueAtTime(vol, t);
  g.gain.exponentialRampToValueAtTime(0.001, t+0.20);
  osc.connect(g).connect(audioCtx.destination);
  osc.start(t); osc.stop(t+0.24);
  trackSource(osc);
}

function playSnare(t, vol) {
  const buf = getNoiseBuf('snare'); if (!buf) return;
  const src = audioCtx.createBufferSource(); src.buffer = buf;
  const hp = audioCtx.createBiquadFilter(); hp.type='highpass'; hp.frequency.value=1200;
  const g = audioCtx.createGain();
  g.gain.setValueAtTime(vol, t);
  g.gain.exponentialRampToValueAtTime(0.001, t+0.18);
  src.connect(hp).connect(g).connect(audioCtx.destination);
  src.start(t); trackSource(src);
}

function playHihat(t, vol) {
  const buf = getNoiseBuf('hihat'); if (!buf) return;
  const src = audioCtx.createBufferSource(); src.buffer = buf;
  const hp = audioCtx.createBiquadFilter(); hp.type='highpass'; hp.frequency.value=8000;
  const g = audioCtx.createGain();
  g.gain.setValueAtTime(vol, t);
  g.gain.exponentialRampToValueAtTime(0.001, t+0.045);
  src.connect(hp).connect(g).connect(audioCtx.destination);
  src.start(t); trackSource(src);
}

function playBass(t, freq, dur) {
  const osc = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  osc.type = 'triangle';
  osc.frequency.value = freq;
  g.gain.setValueAtTime(0.0001, t);
  g.gain.exponentialRampToValueAtTime(0.16, t+0.012);
  g.gain.setValueAtTime(0.16, t+dur-0.04);
  g.gain.exponentialRampToValueAtTime(0.0001, t+dur);
  osc.connect(g).connect(audioCtx.destination);
  osc.start(t); osc.stop(t+dur+0.05);
  trackSource(osc);
}

function playLead(t, freq, dur, vol) {
  const osc = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  osc.type = 'triangle';
  osc.frequency.value = freq;
  g.gain.setValueAtTime(0.0001, t);
  g.gain.exponentialRampToValueAtTime(vol, t+0.02);
  g.gain.setValueAtTime(vol, t + dur*0.85);
  g.gain.exponentialRampToValueAtTime(0.0001, t+dur);
  osc.connect(g).connect(audioCtx.destination);
  osc.start(t); osc.stop(t+dur+0.05);
  trackSource(osc);
}

function playPad(t, freqs, dur, vol) {
  freqs.forEach(f => {
    const osc = audioCtx.createOscillator();
    const g = audioCtx.createGain();
    osc.type = 'sine';
    osc.frequency.value = f;
    g.gain.setValueAtTime(0.0001, t);
    g.gain.linearRampToValueAtTime(vol, t+0.20);
    g.gain.setValueAtTime(vol, t+dur-0.25);
    g.gain.linearRampToValueAtTime(0.0001, t+dur);
    osc.connect(g).connect(audioCtx.destination);
    osc.start(t); osc.stop(t+dur+0.05);
    trackSource(osc);
  });
}

/* ====================== 🎺 VINHETA (rock instrumental) ====================== */
const INTRO_BPM = 120;
const introBeat = 60 / INTRO_BPM;
const introStep = introBeat / 2;
const INTRO_TOTAL_STEPS = 32;

const INTRO_SEQ = (() => {
  const seq = [];
  const prog = [
    { root: 110.00, triad: [220.00, 261.63, 329.63] }, // Am
    { root:  87.31, triad: [174.61, 220.00, 261.63] }, // F
    { root: 130.81, triad: [261.63, 329.63, 392.00] }, // C
    { root:  98.00, triad: [196.00, 246.94, 293.66] }  // G
  ];
  const melodyPerBar = [
    [[0, 659.25, 2], [2, 880.00, 2], [4, 1046.50, 2], [6, 880.00, 2]],
    [[0, 698.46, 2], [2, 880.00, 2], [4, 1046.50, 2], [6, 880.00, 2]],
    [[0, 783.99, 2], [2, 1046.50, 2], [4, 1318.51, 2], [6, 1046.50, 2]],
    [[0, 587.33, 2], [2, 783.99, 2], [4, 987.77, 2], [6, 1318.51, 3]]
  ];

  prog.forEach((p, barIdx) => {
    const base = barIdx * 8;
    for (let i = 0; i < 8; i++) {
      seq.push({ step: base+i, kind:'hihat', vol: i%2===0 ? 0.11 : 0.055 });
    }
    seq.push({ step: base+0, kind:'kick', vol: 0.55 });
    seq.push({ step: base+4, kind:'kick', vol: 0.55 });
    seq.push({ step: base+2, kind:'snare', vol: 0.35 });
    seq.push({ step: base+6, kind:'snare', vol: 0.35 });
    [0,2,4,6].forEach(s => {
      seq.push({ step: base+s, kind:'bass', freq: p.root, dur: 1.6 });
    });
    seq.push({ step: base+0, kind:'pad', freqs: p.triad, dur: 7.5, vol: 0.04 });
    melodyPerBar[barIdx].forEach(([s,f,d]) => {
      seq.push({ step: base+s, kind:'lead', freq: f, dur: d, vol: 0.13 });
    });
  });

  return seq;
})();

let introMusicPlaying = false;
let introMusicTimeout = null;

function playIntroLoop() {
  if (!introMusicPlaying || !soundEnabled || !audioCtx) return;
  const t0 = audioCtx.currentTime + 0.08;
  INTRO_SEQ.forEach(ev => {
    const t = t0 + ev.step * introStep;
    switch (ev.kind) {
      case 'kick':  playKick(t, ev.vol); break;
      case 'snare': playSnare(t, ev.vol); break;
      case 'hihat': playHihat(t, ev.vol); break;
      case 'bass':  playBass(t, ev.freq, ev.dur * introStep); break;
      case 'lead':  playLead(t, ev.freq, ev.dur * introStep, ev.vol); break;
      case 'pad':   playPad(t, ev.freqs, ev.dur * introStep, ev.vol); break;
    }
  });
  const loopMs = INTRO_TOTAL_STEPS * introStep * 1000;
  introMusicTimeout = setTimeout(() => {
    if (introMusicPlaying) playIntroLoop();
  }, loopMs - 30);
}

function startIntroMusic() {
  if (introMusicPlaying || !soundEnabled) return;
  if (!audioCtx) initAudio();
  if (!audioCtx) return;
  introMusicPlaying = true;
  if (musicBadge) musicBadge.classList.add('show');
  playIntroLoop();
}

function stopIntroMusic() {
  introMusicPlaying = false;
  if (introMusicTimeout) { clearTimeout(introMusicTimeout); introMusicTimeout = null; }
  if (musicBadge) musicBadge.classList.remove('show');
  if (autoplayHint) autoplayHint.classList.remove('show');
  stopAllSounds();
}

/* ---------- SFX do quiz ---------- */
function playTone(opts) {
  if (!soundEnabled || !audioCtx) return;
  const { freq=440, duration=0.15, type='sine', volume=0.15, when=0 } = opts;
  const t0 = audioCtx.currentTime + when;
  const osc = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  osc.type = type;
  osc.frequency.setValueAtTime(freq, t0);
  g.gain.setValueAtTime(0.0001, t0);
  g.gain.exponentialRampToValueAtTime(volume, t0+0.012);
  g.gain.exponentialRampToValueAtTime(0.0001, t0+duration);
  osc.connect(g).connect(audioCtx.destination);
  osc.start(t0); osc.stop(t0+duration+0.05);
  trackSource(osc);
}

function sfxStart() {
  playTone({freq: 523, duration:0.10, type:'triangle', volume:0.14, when:0});
  playTone({freq: 784, duration:0.14, type:'triangle', volume:0.14, when:0.10});
}
function sfxCorrect() {
  playTone({freq: 660, duration:0.10, type:'sine', volume:0.18, when:0});
  playTone({freq: 990, duration:0.18, type:'sine', volume:0.18, when:0.11});
}
function sfxWrongAlarm() {
  const pattern = [
    {f:500,d:0.13},{f:800,d:0.13},{f:500,d:0.13},
    {f:800,d:0.13},{f:500,d:0.13},{f:800,d:0.20}
  ];
  let t = 0;
  pattern.forEach(p => { playTone({freq:p.f, duration:p.d, type:'square', volume:0.16, when:t}); t += p.d+0.02; });
}
function sfxTick() {
  playTone({freq: 1100, duration:0.06, type:'square', volume:0.09});
}
function sfxFinish() {
  playTone({freq:523, duration:0.14, type:'triangle', volume:0.2, when:0});
  playTone({freq:659, duration:0.14, type:'triangle', volume:0.2, when:0.15});
  playTone({freq:784, duration:0.30, type:'triangle', volume:0.2, when:0.30});
}

/* ---------- Botão de som ---------- */
function updateSoundToggle() {
  if (!soundToggle) return;
  soundToggle.textContent = soundEnabled ? '🔊' : '🔇';
  soundToggle.classList.toggle('muted', !soundEnabled);
  soundToggle.setAttribute('aria-pressed', String(!soundEnabled));
}
soundToggle.addEventListener('click', () => {
  soundEnabled = !soundEnabled;
  safeStorage.set('pq_sound', soundEnabled ? 'on' : 'off');
  updateSoundToggle();
  try {
    initAudio();
    if (soundEnabled) {
      playTone({freq:880, duration:0.09, type:'triangle', volume:0.15});
      if (introScreen && !introScreen.classList.contains('hide')) {
        introMusicStarted = false;
        tryStartIntroMusic();
      }
    } else {
      stopIntroMusic();
    }
  } catch(e){}
});
updateSoundToggle();

function updateHUD() {
  scorePill.textContent    = `Acertos: ${score} / ${total}`;
  progressPill.textContent = `Progresso: ${answered} / ${total}`;
  progressFill.style.width = (answered / total * 100) + '%';
}

/* ========================== INÍCIO DO SIMULADO ========================== */
function startQuiz() {
  if (!introScreen || introScreen.classList.contains('hide')) return;
  stopIntroMusic();
  introScreen.classList.add('hide');
  introScreen.setAttribute('aria-hidden', 'true');
  try {
    initAudio();
    if (soundEnabled) sfxStart();
    vibrate(60);
  } catch(e){ console.warn('Áudio/vibração indisponíveis:', e); }
  renderQuestion();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

/* ============================ RENDER ============================ */
function renderQuestion() {
  clearActiveTimer();
  quizEl.innerHTML = '';
  if (currentIndex >= total) { showResults(); return; }

  const q = questions[currentIndex];
  const card = document.createElement('article');
  card.className = 'card';
  card.dataset.idx = currentIndex;
  card.innerHTML = `
    <div class="photo">
      <img src="${q.img}" alt="${q.alt}" loading="lazy"
           onerror="this.style.display='none';this.parentElement.classList.add('noimg');">
    </div>
    <div class="content">
      <div class="num">Questão ${String(currentIndex + 1).padStart(2, '0')} · ${total}</div>
      <p class="statement">${q.statement}</p>
      <div class="timer-display" id="timerDisplay">
        <span class="t-label" id="timerLabel">Responda em</span>
        <div class="t-bar"><div id="timerBarFill"></div></div>
        <span class="t-value" id="timerValue">${ANSWER_TIME}s</span>
      </div>
      <div class="vf">
        <button type="button" data-val="true">Verdadeiro</button>
        <button type="button" data-val="false">Falso</button>
      </div>
      <div class="feedback" aria-live="polite"></div>
      <div class="next-wrap" id="nextWrap">
        <button type="button" id="nextBtn">Próxima questão →</button>
      </div>
    </div>
  `;
  quizEl.appendChild(card);

  const btns = card.querySelectorAll('.vf button');
  btns.forEach(b => b.addEventListener('click', () => handleAnswer(card, q, b, btns)));
  card.querySelector('#nextBtn').addEventListener('click', nextQuestion);
  startAnswerTimer(card, q, btns);
}

function startAnswerTimer(card, q, btns) {
  let timeLeft = ANSWER_TIME;
  paintTimer(card, timeLeft, ANSWER_TIME);
  activeTimer = setInterval(() => {
    if (card.dataset.done === '1') { clearActiveTimer(); return; }
    timeLeft--;
    paintTimer(card, timeLeft, ANSWER_TIME);
    if (timeLeft <= 0) { clearActiveTimer(); handleTimeout(card, q, btns); }
  }, 1000);
}

function paintTimer(card, timeLeft, totalTime) {
  const wrap  = card.querySelector('#timerDisplay');
  const value = card.querySelector('#timerValue');
  const fill  = card.querySelector('#timerBarFill');
  if (!wrap) return;
  const pct = Math.max(0, (timeLeft / totalTime) * 100);
  fill.style.width  = pct + '%';
  value.textContent = Math.max(0, timeLeft) + 's';
  wrap.classList.remove('warn', 'danger');
  if (timeLeft <= 3)      wrap.classList.add('danger');
  else if (timeLeft <= 6) wrap.classList.add('warn');
}

function handleAnswer(card, q, clickedBtn, btns) {
  if (card.dataset.done === '1') return;
  card.dataset.done = '1';
  clearActiveTimer();

  const user = clickedBtn.dataset.val === 'true';
  const correct = user === q.answer;

  btns.forEach(b => {
    b.disabled = true;
    const bVal = b.dataset.val === 'true';
    if (bVal === q.answer) b.classList.add('correct');
    else if (b === clickedBtn) b.classList.add('wrong');
  });
  card.classList.add(correct ? 'flash-ok' : 'flash-err');

  const fb = card.querySelector('.feedback');
  fb.classList.add('show', correct ? 'ok' : 'err');
  fb.innerHTML = `
    <div class="fb-head">${correct ? '✓ Você acertou!' : '✗ Você errou.'}</div>
    <div class="fb-body">
      <span class="resp">Resposta correta: ${q.answer ? 'Verdadeiro' : 'Falso'}.</span>
      <p>${q.explanation}</p>
    </div>
  `;

  answered++;
  if (correct) score++;
  updateHUD();
  if (correct) startCorrectFlow(card);
  else         startWrongFlow(card);
}

function handleTimeout(card, q, btns) {
  if (card.dataset.done === '1') return;
  card.dataset.done = '1';
  btns.forEach(b => {
    b.disabled = true;
    if ((b.dataset.val === 'true') === q.answer) b.classList.add('correct');
  });
  card.classList.add('flash-err');

  const fb = card.querySelector('.feedback');
  fb.classList.add('show', 'err');
  fb.innerHTML = `
    <div class="fb-head">⏱ Tempo esgotado!</div>
    <div class="fb-body">
      <span class="resp">Resposta correta: ${q.answer ? 'Verdadeiro' : 'Falso'}.</span>
      <p>${q.explanation}</p>
    </div>
  `;
  answered++;
  updateHUD();
  startWrongFlow(card);
}

function startCorrectFlow(card) {
  const wrap  = card.querySelector('#timerDisplay');
  const label = card.querySelector('#timerLabel');
  const value = card.querySelector('#timerValue');
  const fill  = card.querySelector('#timerBarFill');
  label.textContent = 'Próxima em';
  wrap.classList.remove('warn', 'danger');
  if (soundEnabled) sfxCorrect();
  vibrate(80);

  let timeLeft = CORRECT_WAIT;
  paintWait(wrap, value, fill, timeLeft, CORRECT_WAIT);
  activeTimer = setInterval(() => {
    timeLeft--;
    paintWait(wrap, value, fill, timeLeft, CORRECT_WAIT);
    if (timeLeft <= 0) { clearActiveTimer(); showNextButton(card); }
  }, 1000);
}

function startWrongFlow(card) {
  studyCountdown.textContent = WRONG_WAIT + 's';
  studyOverlay.classList.add('show');
  studyOverlay.setAttribute('aria-hidden', 'false');

  if (soundEnabled) sfxWrongAlarm();
  vibrate([400, 120, 400, 120, 400, 120, 400, 120, 400]);

  const wrap  = card.querySelector('#timerDisplay');
  const label = card.querySelector('#timerLabel');
  const value = card.querySelector('#timerValue');
  const fill  = card.querySelector('#timerBarFill');
  label.textContent = 'Estude mais por';
  wrap.classList.remove('warn', 'danger');

  let timeLeft = WRONG_WAIT;
  paintWait(wrap, value, fill, timeLeft, WRONG_WAIT);
  activeTimer = setInterval(() => {
    timeLeft--;
    studyCountdown.textContent = Math.max(0, timeLeft) + 's';
    paintWait(wrap, value, fill, timeLeft, WRONG_WAIT);
    if (timeLeft > 0) {
      if (soundEnabled) sfxTick();
      vibrate(60);
    }
    if (timeLeft <= 0) {
      clearActiveTimer();
      stopVibrate();
      stopAllSounds();
      studyOverlay.classList.remove('show');
      studyOverlay.setAttribute('aria-hidden', 'true');
      showNextButton(card);
    }
  }, 1000);
}

function paintWait(wrap, value, fill, timeLeft, totalTime) {
  const pct = Math.max(0, (timeLeft / totalTime) * 100);
  fill.style.width  = pct + '%';
  value.textContent = Math.max(0, timeLeft) + 's';
  wrap.classList.remove('warn', 'danger');
  if (totalTime === WRONG_WAIT) wrap.classList.add('danger');
  else if (timeLeft <= 3) wrap.classList.add('danger');
}

function showNextButton(card) {
  const nextWrap = card.querySelector('#nextWrap');
  const timer    = card.querySelector('#timerDisplay');
  if (timer) timer.style.display = 'none';
  if (nextWrap) nextWrap.classList.add('show');
}

function nextQuestion() {
  clearActiveTimer();
  stopVibrate();
  stopAllSounds();
  studyOverlay.classList.remove('show');
  studyOverlay.setAttribute('aria-hidden', 'true');
  currentIndex++;
  renderQuestion();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function reset() {
  clearActiveTimer();
  stopVibrate();
  stopAllSounds();
  stopIntroMusic();
  studyOverlay.classList.remove('show');
  studyOverlay.setAttribute('aria-hidden', 'true');
  introScreen.classList.add('hide');
  introScreen.setAttribute('aria-hidden', 'true');
  score = 0; answered = 0; currentIndex = 0;
  updateHUD();
  renderQuestion();
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function showResults() {
  const pct = Math.round((score / total) * 100);
  let msg = 'Bom começo — revise o material e tente novamente.';
  if (score === total) msg = 'Excelente! Você domina o conteúdo.';
  else if (pct >= 80)  msg = 'Muito bom! Revise só os erros.';
  else if (pct >= 60)  msg = 'Razoável — foque nos pontos que errou.';

  if (soundEnabled) sfxFinish();
  vibrate([120, 80, 120, 80, 250]);

  quizEl.innerHTML = `
    <div class="results">
      <h2>Simulado concluído!</h2>
      <div class="big">${score} / ${total}</div>
      <p>${msg}</p>
      <button type="button" id="restartBtn">Refazer simulado</button>
    </div>
  `;
  document.getElementById('restartBtn').addEventListener('click', reset);
}

document.addEventListener('keydown', (e) => {
  if (introScreen && !introScreen.classList.contains('hide')) {
    if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); startQuiz(); }
    return;
  }
  if (studyOverlay.classList.contains('show')) return;
  const card = document.querySelector('.card');
  if (!card) return;

  if (card.dataset.done !== '1') {
    if (e.key === 'v' || e.key === 'V') card.querySelector('[data-val="true"]')?.click();
    if (e.key === 'f' || e.key === 'F') card.querySelector('[data-val="false"]')?.click();
  } else {
    const nextBtn = card.querySelector('#nextBtn');
    const nextWrap = card.querySelector('#nextWrap');
    if (nextBtn && nextWrap.classList.contains('show') && (e.key === 'Enter' || e.key === ' ')) {
      e.preventDefault(); nextBtn.click();
    }
  }
});

document.getElementById('resetBtn').addEventListener('click', reset);
startBtn.addEventListener('click', startQuiz);

/* ======================================================================
   🎵 AUTOPLAY — tenta ao máximo, mas depende do browser permitir.
   Regra dos navegadores: só toca som após UM gesto do usuário.
   Aqui escutamos TODOS os gestos possíveis e disparamos na hora.
   ====================================================================== */
let introMusicStarted = false;
let hintShown = false;

function showAutoplayHint() {
  if (hintShown || !autoplayHint) return;
  if (introScreen && introScreen.classList.contains('hide')) return;
  hintShown = true;
  autoplayHint.classList.add('show');
}
function hideAutoplayHint() {
  if (!autoplayHint) return;
  autoplayHint.classList.remove('show');
}

function tryStartIntroMusic() {
  if (introMusicStarted) return;
  if (!soundEnabled) return;
  if (introScreen && introScreen.classList.contains('hide')) return;

  try {
    initAudio();
    if (audioCtx && audioCtx.state === 'suspended') {
      audioCtx.resume().then(() => {
        if (audioCtx.state === 'running') {
          introMusicStarted = true;
          hideAutoplayHint();
          startIntroMusic();
        }
      }).catch(()=>{});
    } else if (audioCtx && audioCtx.state === 'running') {
      introMusicStarted = true;
      hideAutoplayHint();
      startIntroMusic();
    }
  } catch(e){}
}

/* Tenta após o load — funciona em alguns desktops com permissão */
window.addEventListener('load', () => {
  setTimeout(() => {
    tryStartIntroMusic();
    setTimeout(() => {
      if (!introMusicStarted) showAutoplayHint();
    }, 500);
  }, 60);
});

/* Escuta TODOS os gestos possíveis e dispara no primeiro */
const GESTOS = ['pointerdown','mousedown','touchstart','touchend','keydown','click','scroll','wheel'];
GESTOS.forEach(evt => {
  window.addEventListener(evt, () => {
    if (!introMusicStarted) tryStartIntroMusic();
  }, {passive: true});
});

document.addEventListener('click', () => {
  if (audioCtx && audioCtx.state === 'suspended') audioCtx.resume().catch(()=>{});
}, {passive: true});

document.addEventListener('visibilitychange', () => {
  if (document.hidden) {
    stopVibrate();
    stopAllSounds();
  }
});

updateHUD();
</script>
</body>
</html>
