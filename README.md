# -
الة حاسبة علمية كاملة بسيطة وسهلة الاستعمال
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>آلة حاسبة علمية</title>
<style>
:root{
  --desk:#d5dbd4;
  --body:#2f3a4a;
  --bezel:#212a36;
  --lcd:#cddbc3;
  --lcd-ink:#1f2d1d;
  --fn:#3d4959;
  --fn-ink:#e9eef4;
  --num:#e8e4da;
  --num-ink:#1c2128;
  --op:#d9922e;
  --op-ink:#1c1405;
  --eq:#2b9486;
  --del:#b9503e;
  --alt:#f2b65f;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;background:var(--desk);color:#1c2128;
  font-family:"Segoe UI",Tahoma,"Noto Sans Arabic",system-ui,sans-serif}
body{min-height:100vh;padding:20px 12px 40px}
.wrap{display:flex;flex-wrap:wrap;gap:20px;justify-content:center;align-items:flex-start}

/* ---------- الجهاز ---------- */
.calc{width:min(400px,100%);background:var(--body);border-radius:22px;padding:16px 16px 18px;
  box-shadow:0 2px 0 #46566b inset,0 18px 30px -12px rgba(20,30,40,.55);direction:ltr}
.head{direction:rtl;display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;color:#dfe6ee}
.head h1{font-size:15px;font-weight:600;margin:0;letter-spacing:.2px}
.head button{font:inherit;font-size:13px;background:transparent;color:var(--alt);border:1px solid #56667c;
  border-radius:999px;padding:4px 12px;cursor:pointer}
.head button:hover{background:#3a475a}

/* ---------- الشاشة ---------- */
.lcd{background:var(--lcd);color:var(--lcd-ink);border-radius:10px;padding:8px 12px 10px;
  box-shadow:inset 0 3px 8px rgba(0,0,0,.35),0 0 0 4px var(--bezel);
  font-family:ui-monospace,"SF Mono",Menlo,Consolas,"Courier New",monospace;min-height:128px}
.ind{display:flex;gap:10px;font-size:10px;font-weight:700;min-height:14px;flex-wrap:wrap}
.ind span{opacity:.18}
.ind span.on{opacity:1}
.expr,.res{text-align:right;white-space:nowrap;overflow-x:auto;scrollbar-width:none}
.expr::-webkit-scrollbar,.res::-webkit-scrollbar{display:none}
.expr{font-size:18px;min-height:28px;margin-top:6px;opacity:.8}
.res{font-size:34px;font-weight:700;min-height:48px;line-height:1.35;margin-top:4px}
.res.dim{opacity:.5}
.res.err{font-size:22px;font-weight:600;direction:rtl;font-family:"Segoe UI",Tahoma,sans-serif;padding-top:8px}

/* ---------- الأزرار ---------- */
.grid{display:grid;grid-template-columns:repeat(5,1fr);gap:8px;margin-top:12px}
.key{appearance:none;border:0;border-radius:9px;min-height:50px;padding:2px 0;cursor:pointer;
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  font-family:inherit;box-shadow:0 3px 0 rgba(0,0,0,.38);transition:transform .05s,box-shadow .05s}
.key:active{transform:translateY(2px);box-shadow:0 1px 0 rgba(0,0,0,.38)}
.key:focus-visible{outline:2px solid var(--alt);outline-offset:2px}
.key .main{font-size:16px;font-weight:600;line-height:1.15}
.key .alt{font-size:10px;font-weight:700;color:var(--alt);line-height:1.1;margin-bottom:1px}
.key .alt:empty{display:block;height:11px}

.fn{background:var(--fn);color:var(--fn-ink)}
.ctl{background:#2a3340;color:#b9c6d6;box-shadow:0 3px 0 rgba(0,0,0,.45)}
.ctl .main{font-size:12px;letter-spacing:.3px}
.ctl .alt{display:none}
.num{background:var(--num);color:var(--num-ink)}
.num .main{font-size:21px;font-weight:600}
.num .alt,.op .alt,.del .alt,.eq .alt{display:none}
.op{background:var(--op);color:var(--op-ink)}
.op .main{font-size:22px}
.del{background:var(--del);color:#fff}
.eq{background:var(--eq);color:#fff}
.eq .main{font-size:24px}

/* وضع SHIFT: الوظيفة الثانوية تصبح هي الأساسية */
.shift .fn .alt{font-size:16px;color:#ffd08a}
.shift .fn .main{font-size:10px;opacity:.55;font-weight:500}
.shift .fn.noalt{opacity:.4}
.shift [data-id="shift"]{background:var(--alt);color:#2a1a00}

/* ---------- شريط الحساب ---------- */
.tape{width:min(300px,100%);background:#f4f2ea;color:#22262b;padding:14px 14px 18px;
  border-radius:4px 4px 14px 14px;border:1px dashed #9aa39a;
  box-shadow:0 10px 20px -14px rgba(20,30,40,.5);max-height:560px;overflow:auto;direction:rtl}
.tape[hidden]{display:none}
.tape header{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px}
.tape h2{font-size:14px;margin:0}
.tape header button{font:inherit;font-size:12px;border:0;background:none;color:#a2412f;cursor:pointer;padding:2px 4px}
.tape ol{list-style:none;margin:0;padding:0}
.tape li{padding:8px 4px;border-bottom:1px dashed #c8c8bc;cursor:pointer;direction:ltr;text-align:right;
  font-family:ui-monospace,"SF Mono",Menlo,Consolas,monospace}
.tape li:hover{background:#ebe8dc}
.tape li small{display:block;font-size:12px;opacity:.7;overflow-wrap:anywhere}
.tape li b{font-size:17px;overflow-wrap:anywhere}
.tape .empty{font-size:13px;opacity:.7;line-height:1.7;padding:6px 2px}

@media (max-width:420px){
  .calc{padding:12px}
  .grid{gap:6px}
  .key{min-height:46px}
  .res{font-size:30px}
}
@media (prefers-reduced-motion:reduce){.key{transition:none}}
</style>
</head>
<body>
<div class="wrap">
  <main class="calc" id="calc">
    <div class="head">
      <h1>آلة حاسبة علمية</h1>
      <button type="button" id="toggleTape">الشريط</button>
    </div>
    <div class="lcd">
      <div class="ind">
        <span id="i-shift">SHIFT</span>
        <span id="i-hyp">HYP</span>
        <span id="i-angle" class="on">DEG</span>
        <span id="i-base" class="on">DEC</span>
        <span id="i-frac">a/b</span>
        <span id="i-mem">M</span>
      </div>
      <div class="expr" id="expr"></div>
      <div class="res" id="res" aria-live="polite">0</div>
    </div>
    <div id="keys"></div>
  </main>

  <aside class="tape" id="tape">
    <header>
      <h2>شريط الحساب</h2>
      <button type="button" id="clearTape">مسح</button>
    </header>
    <ol id="tapeList"></ol>
  </aside>
</div>

<script>
(() => {
'use strict';

const state = {
  expr:'', ans:0, mem:0, hasMem:false,
  shift:false, hyp:false, angle:'DEG', base:'DEC', frac:false,
  justEval:false, lastValue:null, error:null
};
const history = [];
const ANGLES = ['DEG','RAD','GRAD'];
const BASES = [['DEC',10],['HEX',16],['BIN',2],['OCT',8]];

/*ENGINE_START*/
class CalcError extends Error {}
const mathErr = () => new CalcError('خطأ رياضي');
const synErr  = () => new CalcError('خطأ في الصياغة');
const clean = v => Number.isFinite(v) ? parseFloat(v.toPrecision(14)) : v;

const toRad   = x => state.angle==='DEG' ? x*Math.PI/180 : state.angle==='GRAD' ? x*Math.PI/200 : x;
const fromRad = x => state.angle==='DEG' ? x*180/Math.PI : state.angle==='GRAD' ? x*200/Math.PI : x;
const snap = v => Math.abs(v) < 1e-14 ? 0 : v;

function gamma(z){
  if (z < 0.5) return Math.PI / (Math.sin(Math.PI*z) * gamma(1-z));
  z -= 1;
  const c = [0.99999999999980993,676.5203681218851,-1259.1392167224028,771.32342877765313,
    -176.61502916214059,12.507343278686905,-0.13857109526572012,9.9843695780195716e-6,1.5056327351493116e-7];
  let x = c[0];
  for (let i=1;i<9;i++) x += c[i]/(z+i);
  const t = z + 7.5;
  return Math.sqrt(2*Math.PI) * Math.pow(t, z+0.5) * Math.exp(-t) * x;
}
function fact(n){
  if (Number.isInteger(n)){
    if (n < 0 || n > 170) throw mathErr();
    let r = 1; for (let i=2;i<=n;i++) r *= i; return r;
  }
  if (n < -170 || n > 170) throw mathErr();
  return clean(gamma(n+1));
}
function needInt(n){ if (!Number.isInteger(n) || n < 0) throw mathErr(); }
function nPr(n,r){
  needInt(n); needInt(r); if (r > n) throw mathErr();
  let v = 1; for (let i=0;i<r;i++) v *= (n-i);
  if (!Number.isFinite(v)) throw mathErr(); return v;
}
function nCr(n,r){
  needInt(n); needInt(r); if (r > n) throw mathErr();
  r = Math.min(r, n-r);
  let v = 1; for (let i=1;i<=r;i++) v = v*(n-r+i)/i;
  if (!Number.isFinite(v)) throw mathErr(); return Math.round(v);
}
function pow(b,e){
  if (b === 0 && e <= 0) throw mathErr();
  if (b < 0 && !Number.isInteger(e)){
    const k = Math.round(1/e);
    if (Math.abs(1/e - k) < 1e-9 && Math.abs(k) % 2 === 1) return -clean(Math.pow(-b, e));
    throw mathErr();
  }
  const r = Math.pow(b,e);
  if (!Number.isFinite(r)) throw mathErr();
  return clean(r);
}
function root(y,x){
  if (y === 0) throw mathErr();
  if (x < 0){
    if (Number.isInteger(y) && Math.abs(y) % 2 === 1) return -clean(Math.pow(-x, 1/y));
    throw mathErr();
  }
  return pow(x, 1/y);
}
const F = {
  sin:x=>snap(Math.sin(toRad(x))),
  cos:x=>snap(Math.cos(toRad(x))),
  tan:x=>{ const c=Math.cos(toRad(x)); if (Math.abs(c)<1e-14) throw mathErr(); return snap(Math.sin(toRad(x))/c); },
  asin:x=>{ if (Math.abs(x)>1) throw mathErr(); return fromRad(Math.asin(x)); },
  acos:x=>{ if (Math.abs(x)>1) throw mathErr(); return fromRad(Math.acos(x)); },
  atan:x=>fromRad(Math.atan(x)),
  sinh:Math.sinh, cosh:Math.cosh, tanh:Math.tanh, asinh:Math.asinh,
  acosh:x=>{ if (x<1) throw mathErr(); return Math.acosh(x); },
  atanh:x=>{ if (Math.abs(x)>=1) throw mathErr(); return Math.atanh(x); },
  log:x=>{ if (x<=0) throw mathErr(); return Math.log10(x); },
  ln:x=>{ if (x<=0) throw mathErr(); return Math.log(x); },
  abs:Math.abs,
  '√':x=>{ if (x<0) throw mathErr(); return Math.sqrt(x); },
  '∛':Math.cbrt
};

function tokenize(s){
  const out = []; let i = 0;
  while (i < s.length){
    const rest = s.slice(i); let m;
    if ((m = rest.match(/^(\d+\.?\d*|\.\d+)(ᴇ[+-]?\d+)?/))){
      out.push({t:'num', v:parseFloat(m[0].replace('ᴇ','e'))}); i += m[0].length; continue;
    }
    if ((m = rest.match(/^(asinh|acosh|atanh|sinh|cosh|tanh|asin|acos|atan|sin|cos|tan|log|ln|abs)/))){
      out.push({t:'fn', v:m[1]}); i += m[1].length; continue;
    }
    if (rest.startsWith('Ans'))  { out.push({t:'num', v:state.ans}); i += 3; continue; }
    if (rest.startsWith('Rand')) { out.push({t:'num', v:Math.random()}); i += 4; continue; }
    const c = s[i];
    if (c === '√' || c === '∛') { out.push({t:'fn', v:c}); i++; continue; }
    if (c === 'π') { out.push({t:'num', v:Math.PI}); i++; continue; }
    if (c === 'e') { out.push({t:'num', v:Math.E}); i++; continue; }
    if (c === 'M') { out.push({t:'num', v:state.mem}); i++; continue; }
    if (c === 'ʸ' && s[i+1] === '√') { out.push({t:'op', v:'ʸ√'}); i += 2; continue; }
    if ('+-×÷^PC'.includes(c)) { out.push({t:'op', v:c}); i++; continue; }
    if (c === '(') { out.push({t:'lp'}); i++; continue; }
    if (c === ')') { out.push({t:'rp'}); i++; continue; }
    if (c === '!' || c === '%') { out.push({t:'post', v:c}); i++; continue; }
    throw synErr();
  }
  return out;
}

function evaluate(src){
  let open = 0;
  for (const ch of src){ if (ch==='(') open++; else if (ch===')') open--; }
  if (open < 0) throw synErr();
  const T = tokenize(src + ')'.repeat(open));
  let p = 0;
  const isOp = (...v) => T[p] && T[p].t==='op' && v.includes(T[p].v);
  const closeParen = () => { if (!T[p] || T[p].t!=='rp') throw synErr(); p++; };

  function expr(){
    let v = term();
    while (isOp('+','-')){ const o = T[p++].v; const r = term(); v = clean(o==='+' ? v+r : v-r); }
    return v;
  }
  function term(){
    let v = unary();
    for(;;){
      if (isOp('×','÷')){
        const o = T[p++].v; const r = unary();
        if (o==='×') v = clean(v*r);
        else { if (r===0) throw mathErr(); v = clean(v/r); }
      } else if (T[p] && (T[p].t==='num' || T[p].t==='fn' || T[p].t==='lp')){
        v = clean(v*unary());
      } else break;
    }
    return v;
  }
  function unary(){
    if (isOp('-')){ p++; return -unary(); }
    if (isOp('+')){ p++; return unary(); }
    return combin();
  }
  function combin(){
    let v = power();
    while (isOp('P','C','ʸ√')){
      const o = T[p++].v; const r = power();
      v = o==='P' ? nPr(v,r) : o==='C' ? nCr(v,r) : root(v,r);
    }
    return v;
  }
  function power(){
    const b = post();
    if (isOp('^')){ p++; return pow(b, expUnary()); }
    return b;
  }
  function expUnary(){
    if (isOp('-')){ p++; return -expUnary(); }
    if (isOp('+')){ p++; return expUnary(); }
    return power();
  }
  function post(){
    let v = primary();
    while (T[p] && T[p].t==='post'){
      const o = T[p++].v;
      v = o==='!' ? fact(v) : clean(v/100);
    }
    return v;
  }
  function primary(){
    const k = T[p++];
    if (!k) throw synErr();
    if (k.t==='num') return k.v;
    if (k.t==='lp'){ const v = expr(); closeParen(); return v; }
    if (k.t==='fn'){
      let a;
      if (T[p] && T[p].t==='lp'){ p++; a = expr(); closeParen(); }
      else a = post();
      const r = F[k.v](a);
      if (!Number.isFinite(r)) throw mathErr();
      return clean(r);
    }
    throw synErr();
  }

  const v = expr();
  if (p < T.length) throw synErr();
  if (!Number.isFinite(v)) throw mathErr();
  return v;
}
/*ENGINE_END*/

/* ---------- تنسيق النتائج ---------- */
function fmt(v){
  if (v === 0) return '0';
  const a = Math.abs(v);
  if (a >= 1e10 || a < 1e-6){
    const [m,e] = v.toExponential(11).split('e');
    return parseFloat(m).toString() + 'ᴇ' + parseInt(e,10);
  }
  return parseFloat(v.toPrecision(12)).toString();
}
function toFrac(v){
  if (Number.isInteger(v)) return null;
  const neg = v < 0, x = Math.abs(v);
  let h1=1,h0=0,k1=0,k0=1,b=x;
  for (let i=0;i<30;i++){
    const a = Math.floor(b);
    const h2 = a*h1+h0, k2 = a*k1+k0;
    h0=h1; h1=h2; k0=k1; k1=k2;
    if (k1 > 1e6) return null;
    if (Math.abs(x - h1/k1) < 1e-10*Math.max(1,x)) return (neg?'-':'') + h1 + '/' + k1;
    const f = b - a; if (f < 1e-12) break;
    b = 1/f;
  }
  return null;
}
function show(v){
  if (state.base !== 'DEC'){
    const radix = BASES.find(b => b[0]===state.base)[1];
    if (Number.isInteger(v) && Math.abs(v) <= Number.MAX_SAFE_INTEGER)
      return (v<0?'-':'') + Math.abs(v).toString(radix).toUpperCase();
  }
  if (state.frac){ const f = toFrac(v); if (f) return f; }
  return fmt(v);
}

/* ---------- الإدخال ---------- */
const isBinStart = s => /^([+\-×÷^!%PC]|ʸ√)/.test(s);

function add(s){
  state.error = null;
  if (state.justEval){
    state.expr = isBinStart(s) ? 'Ans' : '';
    state.justEval = false;
  }
  if ((s==='+' || s==='×' || s==='÷') && /[+×÷]$/.test(state.expr)){
    state.expr = state.expr.slice(0,-1);
  }
  state.expr += s;
}
function addDecimal(){
  if (!state.justEval){
    const seg = state.expr.match(/[\d.]*$/)[0];
    if (seg.includes('.')) return;
  }
  add('.');
}
function addExp(){
  if (state.expr.endsWith('ᴇ') && !state.justEval) return;
  add(/\d$/.test(state.expr) && !state.justEval ? 'ᴇ' : '1ᴇ');
}
function del(){
  state.error = null; state.justEval = false;
  const m = state.expr.match(/(?:a?(?:sin|cos|tan)h?|log|ln|abs|√|∛)\($|Ans$|Rand$|ʸ√$/);
  state.expr = state.expr.slice(0, m ? -m[0].length : -1);
}
function allClear(){
  state.expr=''; state.error=null; state.justEval=false; state.lastValue=null;
}
function equals(){
  if (!state.expr || state.justEval) return;
  const v = evaluate(state.expr);
  state.ans = v; state.lastValue = v; state.justEval = true; state.error = null;
  history.unshift({expr:state.expr, v});
  if (history.length > 50) history.pop();
  renderTape();
}
function currentValue(){
  if (state.justEval) return state.lastValue;
  if (!state.expr) return state.ans;
  return evaluate(state.expr);
}
function memAdd(sign){
  const v = currentValue();
  state.mem = clean(state.mem + sign*v); state.hasMem = true;
  state.ans = v; state.lastValue = v; state.justEval = true;
}
function memStore(){
  const v = currentValue();
  state.mem = v; state.hasMem = true;
  state.ans = v; state.lastValue = v; state.justEval = true;
}

/* ---------- تعريف الأزرار ---------- */
const trig = name => ({ trig:name, main:name, alt:name+'⁻¹', cls:'fn',
  fn(){ add((state.shift?'a':'') + name + (state.hyp?'h':'') + '('); } });
const ins = (main, alt, a, b) => ({ main, alt, cls:'fn',
  fn(){ add(state.shift && b !== undefined ? b : a); } });
const num = d => ({ main:d, cls:'num', fn(){ add(d); } });
const op  = (label, val) => ({ main:label, cls:'op', fn(){ add(val); } });

const SECTIONS = [
  [ {id:'shift', main:'SHIFT', cls:'ctl', fn(){ state.shift = !state.shift; }},
    {main:'HYP', cls:'ctl', fn(){ state.hyp = !state.hyp; }},
    {main:'DRG', cls:'ctl', fn(){ state.angle = ANGLES[(ANGLES.indexOf(state.angle)+1)%3]; }},
    {main:'S⇄D', cls:'ctl', fn(){ state.frac = !state.frac; }},
    {main:'BASE', cls:'ctl', fn(){ state.base = BASES[(BASES.findIndex(b=>b[0]===state.base)+1)%4][0]; }} ],
  [ trig('sin'), trig('cos'), trig('tan'),
    ins('log','10ˣ','log(','10^('), ins('ln','eˣ','ln(','e^('),
    ins('x²','x³','^2','^3'), ins('xʸ','ʸ√','^','ʸ√'), ins('√','∛','√(','∛('),
    ins('1/x','|x|','^(-1)','abs('), ins('n!','Rand','!','Rand'),
    ins('(','','('), ins(')','',')'), ins('π','e','π','e'),
    {main:'×10ˣ', alt:'', cls:'fn', fn(){ addExp(); }},
    ins('nPr','nCr','P','C') ],
  [ {main:'MC', alt:'', cls:'fn', fn(){ state.mem = 0; state.hasMem = false; }},
    {main:'MR', alt:'', cls:'fn', fn(){ add('M'); }},
    {main:'M+', alt:'MS', cls:'fn', fn(){ state.shift ? memStore() : memAdd(1); }},
    {main:'M−', alt:'', cls:'fn', fn(){ memAdd(-1); }},
    {main:'Ans', alt:'', cls:'fn', fn(){ add('Ans'); }} ],
  [ num('7'), num('8'), num('9'),
    {main:'DEL', cls:'del', fn(){ del(); }}, {main:'AC', cls:'del', fn(){ allClear(); }},
    num('4'), num('5'), num('6'), op('×','×'), op('÷','÷'),
    num('1'), num('2'), num('3'), op('+','+'), op('−','-'),
    num('0'), {main:'.', cls:'num', fn(){ addDecimal(); }},
    {main:'(−)', cls:'fn', alt:'', fn(){ add('-'); }},
    ins('%','','%'),
    {main:'=', cls:'eq', fn(){ equals(); }} ]
];

/* ---------- الواجهة ---------- */
const $ = s => document.querySelector(s);
const calcEl = $('#calc'), exprEl = $('#expr'), resEl = $('#res');

function press(key){
  try { key.fn(); }
  catch (e){ state.error = e instanceof CalcError ? e.message : 'خطأ'; }
  if (key.id !== 'shift') state.shift = false;
  if (key.trig) state.hyp = false;
  refresh();
}

function refresh(){
  calcEl.classList.toggle('shift', state.shift);
  SECTIONS.flat().forEach(k => {
    if (!k.trig) return;
    k.el.querySelector('.main').textContent = k.trig + (state.hyp ? 'h' : '');
    k.el.querySelector('.alt').textContent  = k.trig + (state.hyp ? 'h' : '') + '⁻¹';
  });

  exprEl.textContent = state.expr.replace(/-/g, '−');
  exprEl.scrollLeft = exprEl.scrollWidth;

  resEl.classList.remove('dim','err');
  let txt = '';
  if (state.error){ txt = state.error; resEl.classList.add('err'); }
  else if (state.justEval) txt = show(state.lastValue);
  else if (!state.expr) txt = '0';
  else if (!state.expr.includes('Rand') && /[^\d.]/.test(state.expr)){
    try { txt = show(evaluate(state.expr)); resEl.classList.add('dim'); } catch(e){ txt = ''; }
  }
  resEl.textContent = txt || '\u00a0';
  resEl.scrollLeft = resEl.scrollWidth;

  $('#i-shift').classList.toggle('on', state.shift);
  $('#i-hyp').classList.toggle('on', state.hyp);
  $('#i-mem').classList.toggle('on', state.hasMem);
  $('#i-frac').classList.toggle('on', state.frac);
  $('#i-angle').textContent = state.angle;
  $('#i-base').textContent = state.base;
}

function renderTape(){
  const ol = $('#tapeList');
  ol.innerHTML = '';
  if (!history.length){
    const d = document.createElement('div');
    d.className = 'empty';
    d.textContent = 'لا توجد عمليات بعد. اكتب عملية ثم اضغط =.';
    ol.appendChild(d);
    return;
  }
  history.forEach(h => {
    const li = document.createElement('li');
    const s = document.createElement('small'); s.textContent = h.expr.replace(/-/g,'−');
    const b = document.createElement('b'); b.textContent = '= ' + fmt(h.v);
    li.append(s, b);
    li.title = 'اضغط لاستدعاء العملية';
    li.addEventListener('click', () => {
      state.expr = h.expr; state.justEval = false; state.error = null; refresh();
    });
    ol.appendChild(li);
  });
}

/* بناء لوحة المفاتيح */
const keysEl = $('#keys');
SECTIONS.forEach(sec => {
  const g = document.createElement('div');
  g.className = 'grid';
  sec.forEach(key => {
    const b = document.createElement('button');
    b.type = 'button';
    b.className = 'key ' + key.cls + (key.cls === 'fn' && !key.alt ? ' noalt' : '');
    if (key.id) b.dataset.id = key.id;
    b.setAttribute('aria-label', key.main);
    b.innerHTML = '<span class="alt"></span><span class="main"></span>';
    b.querySelector('.alt').textContent = key.alt || '';
    b.querySelector('.main').textContent = key.main;
    b.addEventListener('click', () => press(key));
    key.el = b;
    g.appendChild(b);
  });
  keysEl.appendChild(g);
});

/* دعم لوحة مفاتيح الكمبيوتر */
const KEYMAP = {
  '+':()=>add('+'), '-':()=>add('-'), '*':()=>add('×'), 'x':()=>add('×'), '/':()=>add('÷'),
  '^':()=>add('^'), '(':()=>add('('), ')':()=>add(')'), '!':()=>add('!'), '%':()=>add('%'),
  '.':()=>addDecimal(), ',':()=>addDecimal(),
  'Enter':()=>equals(), '=':()=>equals(),
  'Backspace':()=>del(), 'Escape':()=>allClear(), 'Delete':()=>allClear(),
  'p':()=>add('π'), 'e':()=>add('e'), 'a':()=>add('Ans'),
  's':()=>add('sin('), 'c':()=>add('cos('), 't':()=>add('tan('),
  'l':()=>add('log('), 'n':()=>add('ln('), 'r':()=>add('√(')
};
document.addEventListener('keydown', e => {
  if (e.ctrlKey || e.metaKey || e.altKey) return;
  let f = null;
  if (/^[0-9]$/.test(e.key)) f = () => add(e.key);
  else if (KEYMAP[e.key]) f = KEYMAP[e.key];
  if (!f) return;
  e.preventDefault();
  try { f(); } catch (err){ state.error = err instanceof CalcError ? err.message : 'خطأ'; }
  refresh();
});

/* الشريط */
const tape = $('#tape');
tape.hidden = !window.matchMedia('(min-width:900px)').matches;
$('#toggleTape').addEventListener('click', () => { tape.hidden = !tape.hidden; });
$('#clearTape').addEventListener('click', () => { history.length = 0; renderTape(); });

renderTape();
refresh();
})();
</script>
</body>
</html>
