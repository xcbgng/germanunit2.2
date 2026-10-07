<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Тренер словаря - Deutsch Lernwortschatz 2, Teil 2</title>
<style>
:root{--bg:#f5f3ee;--card:#fff;--ink:#1d2433;--mute:#6b7280;--line:#d9d5ca;--acc:#c8102e;--ok:#1d7a46;--bad:#b42318;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#14171f;--card:#1e222d;--ink:#eceef3;--mute:#9aa1b0;--line:#33384a;--acc:#ff5a6e;--ok:#4cc38a;--bad:#ff7b72}}
:root[data-theme="dark"]{--bg:#14171f;--card:#1e222d;--ink:#eceef3;--mute:#9aa1b0;--line:#33384a;--acc:#ff5a6e;--ok:#4cc38a;--bad:#ff7b72}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:Georgia,"Times New Roman",serif;min-height:100vh}
main{max-width:520px;margin:0 auto;padding:20px 16px 40px}
h1{font-size:26px;margin:8px 0 2px}
.sub{color:var(--mute);font-family:system-ui,sans-serif;font-size:14px;margin:0 0 18px}
.tabs{display:flex;gap:8px;margin-bottom:16px;font-family:system-ui,sans-serif}
.tabs button{flex:1;padding:12px;border:1px solid var(--line);background:var(--card);color:var(--ink);border-radius:10px;font-size:16px;cursor:pointer}
.tabs button.on{background:var(--acc);border-color:var(--acc);color:#fff}
.card{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:28px 20px;text-align:center;min-height:230px;display:flex;flex-direction:column;justify-content:center;gap:10px}
.cnt{font-family:system-ui,sans-serif;color:var(--mute);font-size:14px;margin-bottom:10px}
.de{font-size:32px;font-weight:700;line-height:1.2;overflow-wrap:anywhere}
.ex{color:var(--mute);font-family:system-ui,sans-serif;font-size:15px}
.ru{font-size:24px;color:var(--acc)}
.row{display:flex;gap:10px;margin-top:14px;font-family:system-ui,sans-serif}
.row button{flex:1;padding:13px;border-radius:10px;border:1px solid var(--line);background:var(--card);color:var(--ink);font-size:16px;cursor:pointer}
.row button.p{background:var(--acc);border-color:var(--acc);color:#fff}
button:focus-visible,input:focus-visible{outline:3px solid var(--acc);outline-offset:2px}
input{width:100%;padding:14px;font-size:20px;border-radius:10px;border:1px solid var(--line);background:var(--bg);color:var(--ink);margin-top:10px;font-family:inherit;text-align:center}
.fb{min-height:24px;font-family:system-ui,sans-serif;font-size:16px;margin-top:6px}
.fb.ok{color:var(--ok)}.fb.bad{color:var(--bad)}
.res{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin:18px 0;font-family:system-ui,sans-serif}
.res div{background:var(--bg);border-radius:10px;padding:14px 6px}
.res b{display:block;font-size:30px}
.hide{display:none}
</style>
</head>
<body>
<main>
<h1>📚 Тренер словаря</h1>
<p class="sub">Deutsch · Lernwortschatz 2 (Teil 2) — <span id="total"></span> слов</p>
<div class="tabs"><button id="tL" class="on">🎓 Обучение</button><button id="tT">✏️ Тест</button></div>

<section id="learn">
<div class="card"><div class="cnt" id="lc"></div><div class="de" id="lde"></div><div class="ex" id="lex"></div><div class="ru" id="lru"></div></div>
<div class="row"><button id="prev">← Назад</button><button id="next" class="p">Вперёд →</button></div>
</section>

<section id="test" class="hide">
<div class="card" id="tcard">
<div class="cnt" id="tc"></div><div class="ru" id="tru"></div><div class="ex" id="tex"></div>
<input id="inp" type="text" autocomplete="off" autocapitalize="off" spellcheck="false" placeholder="Слово по-немецки">
<div class="fb" id="fb"></div>
</div>
<div class="row"><button id="skip">Пропустить</button><button id="check" class="p">Проверить (Enter)</button></div>
<div id="result" class="card hide">
<h2 style="margin:0">Ваш результат</h2>
<div class="res"><div><b id="rOk">0</b>Правильно</div><div><b id="rBad">0</b>Неправильно</div><div><b id="rSk">0</b>Пропущено</div></div>
<div class="row"><button id="again" class="p">Пройти заново</button></div>
</div>
</section>
</main>
<script>
// [немецкое слово, добавка (мн. число и т.п.), перевод]
var W=[
["der Termin","-e","встреча по записи; назначенное время"],["morgen","","завтра"],["nachts","","ночью"],["meistens","","обычно; чаще всего"],["noch","","ещё"],
["Montag","","понедельник"],["Dienstag","","вторник"],["Mittwoch","","среда"],["Donnerstag","","четверг"],["Freitag","","пятница"],["Samstag","","суббота"],["Sonntag","","воскресенье"],
["die Information","-en","информация"],["der Familienname","-n","фамилия"],["die Adresse","-en","адрес"],["die Straße","-n","улица"],
["die Hausnummer","-n","номер дома"],["die Postleitzahl","-en","почтовый индекс"],["der Wohnort","-e","место жительства"],
["das Geburtsdatum","-daten","дата рождения"],["der Geburtsort","-e","место рождения"],["männlich","","мужской"],["weiblich","","женский"],["das Formular","-e","анкета; бланк"],
["ja","","да"],["nein","","нет"],["die Notiz","-en","заметка"],["das Beispiel","-e","пример"],["der Schlüssel","-","ключ"],["das Wörterbuch","-̈er","словарь"],
["das Zimmer","-","комната"],["haben","er hat","иметь"],["passen","","подходить"],["suchen","","искать"],["warten","","ждать"],["alle","","все"],["hier","","здесь"],
["gern","","охотно; с удовольствием"],["Ich schwimme gern.","","Я люблю плавать."],["gehen","","идти; ходить"],["Es geht so.","","Так себе."],["leider","","к сожалению"],
["Das geht leider nicht.","","К сожалению, так не получится."],["groß","","большой"],["lustig","","весёлый"],["neu","","новый"],["super","","супер; отлично"],
["toll","","классно; здорово"],["viel","","много"],["wirklich","","действительно"]
];
var $=function(i){return document.getElementById(i)};
$("total").textContent=W.length;
var li=0;
function showL(){var w=W[li];$("lc").textContent=(li+1)+" / "+W.length;$("lde").textContent=w[0];$("lex").textContent=w[1]?("("+w[1]+")"):"";$("lru").textContent=w[2]}
$("next").onclick=function(){li=(li+1)%W.length;showL()};
$("prev").onclick=function(){li=(li-1+W.length)%W.length;showL()};
showL();
function norm(s){return s.toLowerCase().replace(/ß/g,"ss").replace(/ä/g,"a").replace(/ö/g,"o").replace(/ü/g,"u").replace(/[….?!,]/g,"").replace(/\s+/g," ").trim()}
function bare(s){return s.replace(/^(der|die|das)\s+/i,"")}
var order,ti,ok,bad,sk,locked;
function startT(){order=W.map(function(_,i){return i});for(var i=order.length-1;i>0;i--){var j=Math.floor(Math.random()*(i+1));var t=order[i];order[i]=order[j];order[j]=t}
ti=0;ok=bad=sk=0;$("result").classList.add("hide");$("tcard").classList.remove("hide");document.querySelector("#test .row").classList.remove("hide");showT()}
function showT(){if(ti>=order.length){return finish()}locked=false;var w=W[order[ti]];$("tc").textContent=(ti+1)+" / "+order.length;$("tru").textContent=w[2];$("tex").textContent=w[1]&&!/^-|^[A-Z][a-z]+n$|^Pl|^Sg/.test(w[1])?"":"";$("inp").value="";$("inp").disabled=false;$("fb").textContent="";$("fb").className="fb";$("inp").focus()}
function advance(){ti++;showT()}
function finish(){$("tcard").classList.add("hide");document.querySelector("#test .row").classList.add("hide");$("result").classList.remove("hide");$("rOk").textContent=ok;$("rBad").textContent=bad;$("rSk").textContent=sk}
function check(){
if(locked){advance();return}
var w=W[order[ti]],v=norm($("inp").value);
if(!v){$("fb").textContent="Введите слово или нажмите «Пропустить»";$("fb").className="fb bad";return}
var good=norm(w[0]);
if(v===good||v===norm(bare(w[0]))){ok++;$("fb").textContent="✓ Верно: "+w[0];$("fb").className="fb ok"}
else{bad++;$("fb").textContent="✗ Правильно: "+w[0];$("fb").className="fb bad"}
locked=true;$("inp").disabled=true;$("check").textContent="Дальше (Enter)"}
$("check").onclick=function(){var was=locked;check();if(was)$("check").textContent="Проверить (Enter)"};
$("skip").onclick=function(){if(locked){return}sk++;$("check").textContent="Проверить (Enter)";advance()};
document.addEventListener("keydown",function(e){if(e.key==="Enter"&&!$("test").classList.contains("hide")&&$("result").classList.contains("hide")){e.preventDefault();var was=locked;check();if(was)$("check").textContent="Проверить (Enter)"}});
$("again").onclick=function(){$("check").textContent="Проверить (Enter)";startT()};
$("tL").onclick=function(){$("tL").classList.add("on");$("tT").classList.remove("on");$("learn").classList.remove("hide");$("test").classList.add("hide")};
$("tT").onclick=function(){$("tT").classList.add("on");$("tL").classList.remove("on");$("test").classList.remove("hide");$("learn").classList.add("hide");$("check").textContent="Проверить (Enter)";startT()};
</script>
</body>
</html>
