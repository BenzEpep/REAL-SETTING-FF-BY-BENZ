<!DOCTYPE html>
<html>
<head>
<title>FF RealSetting Sensi – One List</title>
<style>
body{
  background:#0b0b0b;
  color:#fff;
  font-family:Arial;
}
h1{text-align:center}
ul{
  list-style:none;
  padding:0;
  max-width:400px;
  margin:auto;
}
li{
  background:#1a1a1a;
  margin:10px 0;
  padding:15px;
  border-radius:12px;
}
input,select{
  width:100%;
  margin-top:6px;
}
input[type=range]{margin:8px 0}
button{
  width:48%;
  padding:10px;
  margin-top:10px;
}
.small{font-size:12px;color:#aaa}
.center{text-align:center}
</style>
</head>

<body>

<h1>🔥 FF REALSETTING SENSI 🔥</h1>
<p class="center small">Manual Tool • Anti‑Ban • Pro Analysis</p>

<ul>

<!-- DEVICE PROFILE -->
<li>
<b>📱 Device Profile</b><br>
RAM
<select id="ram">
  <option value="low">2‑3GB</option>
  <option value="mid">4‑6GB</option>
  <option value="high">8GB+</option>
  <option value="ultra">12GB+</option>
</select>

GPU / Chipset
<select id="gpu">
  <option value="low">Low</option>
  <option value="mid">Mid</option>
  <option value="high">High</option>
  <option value="ultra">Ultra</option>
</select>

FPS
<select id="fps">
  <option value="30">30 FPS</option>
  <option value="60">60 FPS</option>
  <option value="90">90 FPS</option>
  <option value="120">120 FPS</option>
</select>

DPI
<select id="dpi">
  <option value="low">Low</option>
  <option value="mid">Medium</option>
  <option value="high">High</option>
</select>

<button onclick="autoTune()" style="width:100%">⚙ Auto Tune</button>
<p id="deviceMsg" class="small"></p>
</li>

<!-- SENSITIVITY -->
<li>
<b>🎯 Sensitivity</b><br>

General
<input type="range" id="general" min="0" max="200" value="100">
<span id="g">100</span>

Red Dot
<input type="range" id="reddot" min="0" max="200" value="90">
<span id="r">90</span>

Scope
<input type="range" id="scope" min="0" max="200" value="80">
<span id="s">80</span>

AWM
<input type="range" id="awm" min="0" max="200" value="60">
<span id="a">60</span>
</li>

<!-- ANALYZER -->
<li>
<b>🧠 Aim Analyzer (Teori)</b>
<p id="analyze">—</p>
</li>

<!-- ACTION -->
<li class="center">
<button onclick="save()">💾 Save</button>
<button onclick="reset()">♻ Reset</button>
</li>

</ul>

<script>
const sliders=["general","reddot","scope","awm"];
sliders.forEach(id=>{
  document.getElementById(id).oninput=()=>{
    document.getElementById(id[0]).innerText=
      document.getElementById(id).value;
    analyze();
  }
});

// AUTO TUNE SESUAI DEVICE LENGKAP
function autoTune(){
  let base=90;

  // RAM influence
  if(ram.value==="mid") base+=5;
  if(ram.value==="high") base+=10;
  if(ram.value==="ultra") base+=15;

  // GPU influence
  if(gpu.value==="mid") base+=5;
  if(gpu.value==="high") base+=10;
  if(gpu.value==="ultra") base+=15;

  // FPS influence
  if(fps.value==="60") base+=5;
  if(fps.value==="90") base+=10;
  if(fps.value==="120") base+=15;

  // DPI influence
  if(dpi.value==="mid") base+=0;
  if(dpi.value==="high") base-=5;

  // Apply to sliders
  general.value = base+20;
  reddot.value = base+10;
  scope.value = base;
  awm.value = base-20;

  g.innerText = general.value;
  r.innerText = reddot.value;
  s.innerText = scope.value;
  a.innerText = awm.value;

  deviceMsg.innerText = "✅ Auto tuning siap (manual set di FF)";
  analyze();
}

function analyze(){
  let score=
    general.value*0.4+
    reddot.value*0.3+
    scope.value*0.2+
    awm.value*0.1;

  let style="Stable";
  if(score>110) style="Aggressive 🔥";
  if(score<80) style="Precise 🎯";

  analyze.innerText=
    "Aim Style: "+style+
    " | Score: "+Math.round(score);
}

function save(){
  localStorage.setItem("ffsensi",JSON.stringify({
    g:general.value,r:reddot.value,
    s:scope.value,a:awm.value
  }));
  alert("Preset disimpan!");
}

function reset(){
  general.value=100;reddot.value=90;
  scope.value=80;awm.value=60;
  g.innerText=100;r.innerText=90;
  s.innerText=80;a.innerText=60;
  analyze();
}

// LOAD PRESET
const saved=JSON.parse(localStorage.getItem("ffsensi"));
if(saved){
  general.value=saved.g;
  reddot.value=saved.r;
  scope.value=saved.s;
  awm.value=saved.a;
  g.innerText=saved.g;
  r.innerText=saved.r;
  s.innerText=saved.s;
  a.innerText=saved.a;
}
analyze();
</script>

</body>
</html>
