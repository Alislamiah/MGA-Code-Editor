<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#07111f">
<title>MGA Code</title>
<link rel="icon" href="icon.png">

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/material-darker.min.css">

<style>
*{box-sizing:border-box}
:root{
 --bg:#060d18;
 --panel:#0d1929;
 --panel2:#111f32;
 --border:#20334b;
 --blue:#2684ff;
 --cyan:#39c8ee;
 --text:#edf4ff;
 --muted:#91a5bd;
 --red:#ff5268;
 --green:#30d69a;
}
body{
 margin:0;background:var(--bg);color:var(--text);
 font-family:Arial,sans-serif;min-height:100vh;
}
button,input,textarea{font:inherit}
button{cursor:pointer}
.hidden{display:none!important}
#accountScreen{
 min-height:100vh;display:flex;align-items:center;
 justify-content:center;padding:20px;
 background:radial-gradient(circle at 50% 15%,#12325a 0,transparent 45%),var(--bg);
}
.account-card{
 width:100%;max-width:430px;background:var(--panel);
 border:1px solid var(--border);border-radius:24px;
 padding:28px;box-shadow:0 20px 70px #0008;
}
.logo{
 width:58px;height:58px;border-radius:18px;
 display:grid;place-items:center;
 background:linear-gradient(135deg,#1675ff,#26c7e8);
 font-size:25px;font-weight:bold;color:white;
 margin-bottom:20px;
}
h1,h2,h3,p{margin-top:0}
.account-card h1{font-size:25px;margin-bottom:8px}
.muted{color:var(--muted);font-size:14px;line-height:1.6}
.account-option{
 margin:24px 0 14px;padding:16px;border:1px solid var(--border);
 background:#101f32;border-radius:15px;display:flex;
 align-items:center;gap:12px;
}
.avatar{
 width:42px;height:42px;border-radius:50%;
 background:#1e5790;display:grid;place-items:center;font-weight:bold;
}
.account-info{min-width:0;flex:1}
.account-info strong,.account-info small{
 display:block;overflow:hidden;text-overflow:ellipsis;white-space:nowrap
}
.account-info small{color:var(--muted);margin-top:5px}
.btn{
 border:0;border-radius:12px;padding:12px 17px;
 color:white;background:var(--blue);font-weight:700;
}
.btn.secondary{background:#192b42;border:1px solid var(--border)}
.btn.danger{background:#7d2635}
.btn.green{background:#087b5a}
.btn.full{width:100%}
.btn:disabled{opacity:.5;cursor:not-allowed}
.topbar{
 height:65px;border-bottom:1px solid var(--border);
 display:flex;align-items:center;justify-content:space-between;
 padding:0 18px;background:#081321;position:sticky;top:0;z-index:5;
}
.brand{display:flex;align-items:center;gap:10px;font-weight:bold}
.brand-icon{
 width:35px;height:35px;border-radius:11px;
 display:grid;place-items:center;background:linear-gradient(135deg,#1675ff,#25c7e8)
}
.top-actions{display:flex;gap:8px;align-items:center}
.user-pill{
 border:1px solid var(--border);border-radius:20px;
 padding:8px 11px;color:var(--muted);font-size:12px;
 max-width:150px;overflow:hidden;text-overflow:ellipsis;
}
main{max-width:1100px;margin:auto;padding:28px 18px 70px}
.welcome{
 padding:25px;border-radius:20px;border:1px solid var(--border);
 background:linear-gradient(120deg,#102743,#0c1929 75%);
 margin-bottom:25px;
}
.welcome h1{font-size:26px;margin-bottom:9px}
.section-head{
 display:flex;align-items:center;justify-content:space-between;
 gap:12px;margin:25px 0 15px;
}
.section-head h2{font-size:18px;margin:0}
.project-grid{
 display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
 gap:14px;
}
.project-card{
 background:var(--panel);border:1px solid var(--border);
 border-radius:16px;padding:17px;min-height:130px;
 cursor:pointer;user-select:none;touch-action:pan-y;
}
.project-card:active{border-color:var(--blue)}
.project-card h3{font-size:16px;margin:0 0 9px}
.project-card p{font-size:12px;color:var(--muted);margin:0}
.project-card .project-icon{font-size:22px;margin-bottom:13px}
.empty{
 padding:30px;text-align:center;color:var(--muted);
 border:1px dashed var(--border);border-radius:16px;
}
#editorScreen{
 position:fixed;inset:0;background:var(--bg);z-index:20;
 display:flex;flex-direction:column;
}
.editor-top{
 min-height:62px;display:flex;align-items:center;
 justify-content:space-between;gap:8px;padding:9px 12px;
 background:#091524;border-bottom:1px solid var(--border);
}
.editor-title{font-size:14px;font-weight:bold;overflow:hidden;text-overflow:ellipsis}
.editor-buttons{display:flex;gap:7px}
.editor-buttons .btn{padding:10px 12px;font-size:12px}
.editor-tabs{
 display:flex;gap:5px;padding:9px 12px;
 border-bottom:1px solid var(--border);background:#0a1523;
}
.tab{
 padding:9px 15px;border:1px solid transparent;
 border-radius:9px;background:transparent;color:var(--muted);
}
.tab.active{background:#142b46;color:white;border-color:#24527d}
.editors{flex:1;min-height:0;position:relative}
.editor-pane{height:100%;display:none}
.editor-pane.active{display:block}
.CodeMirror{
 height:100%;font-size:14px;line-height:1.6;
 font-family:Consolas,monospace;
}
.CodeMirror-gutters{background:#101b2a;border-right:1px solid #26384c}
.CodeMirror-linenumber{color:#71869d}
.CodeMirror .error-line{background:rgba(255,65,85,.13)}
.CodeMirror .error-gutter{
 color:#ff5368;font-weight:bold;font-size:17px;
}
.bottom-panel{
 max-height:190px;overflow:auto;background:#0b1725;
 border-top:1px solid var(--border);padding:12px 15px;
}
.bottom-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:9px}
.bottom-head strong{font-size:13px}
.status{font-size:12px;color:var(--muted)}
.error-item{
 padding:9px 10px;margin:6px 0;border-radius:9px;
 background:#241923;border:1px solid #63303d;
 color:#ff9eaa;font-size:12px;line-height:1.5;
}
.success-item{
 padding:9px 10px;border-radius:9px;
 background:#102a25;border:1px solid #205e4c;
 color:#6ce3b6;font-size:12px;
}
#contextMenu{
 position:fixed;z-index:50;width:220px;
 background:#101e30;border:1px solid #29415e;
 border-radius:14px;padding:7px;box-shadow:0 15px 45px #000a;
}
#contextMenu button{
 display:block;width:100%;text-align:left;padding:12px;
 color:var(--text);background:transparent;border:0;border-radius:8px;
 font-size:13px;
}
#contextMenu button:hover{background:#1c3551}
#contextMenu .danger-text{color:#ff8290}
#modalBackdrop{
 position:fixed;inset:0;background:#0009;z-index:60;
 display:flex;align-items:center;justify-content:center;padding:20px;
}
.modal{
 width:100%;max-width:420px;background:var(--panel);
 border:1px solid var(--border);border-radius:18px;padding:22px;
}
.modal input{
 width:100%;padding:13px;border-radius:10px;
 border:1px solid var(--border);background:#071321;color:white;
 margin:12px 0;
}
.modal-actions{display:flex;gap:8px;justify-content:flex-end;margin-top:15px}
@media(max-width:600px){
 main{padding:18px 13px}
 .welcome{padding:19px}
 .welcome h1{font-size:22px}
 .editor-top{flex-wrap:wrap}
 .editor-title{max-width:100px}
 .editor-buttons .btn{padding:9px;font-size:11px}
 .user-pill{display:none}
}
</style>
</head>

<body>

<!-- SELECT ACCOUNT -->
<section id="accountScreen">
 <div class="account-card">
  <div class="logo">M</div>
  <h1>Select Account</h1>
  <p class="muted">Choose your Alislamiah AI account to continue to MGA Code.</p>

  <div id="accountLoading" class="muted">Checking your account...</div>

  <div id="accountContent" class="hidden">
   <div class="account-option">
    <div class="avatar" id="accountAvatar">A</div>
    <div class="account-info">
     <strong id="accountName">Account</strong>
     <small id="accountEmail"></small>
    </div>
   </div>
   <button class="btn full" id="continueBtn">Continue</button>
   <button class="btn secondary full" id="changeAccountBtn" style="margin-top:9px">Change account</button>
  </div>

  <div id="noAccount" class="hidden">
   <p class="muted">No active Alislamiah AI session was found.</p>
   <button class="btn full" id="loginBtn">Open Alislamiah AI</button>
  </div>
 </div>
</section>

<!-- MAIN APP -->
<section id="appScreen" class="hidden">
 <header class="topbar">
  <div class="brand">
   <div class="brand-icon">M</div>
   <span>MGA Code</span>
  </div>
  <div class="top-actions">
   <span class="user-pill" id="userEmail"></span>
   <button class="btn secondary" id="signOutBtn">Sign out</button>
  </div>
 </header>

 <main>
  <section class="welcome">
   <h1>Build something amazing.</h1>
   <p class="muted">Write, manage, verify and correct your code in one workspace.</p>
   <button class="btn" id="startWritingBtn">＋ Start Writing</button>
  </section>

  <div class="section-head">
   <h2>Your Last Writings</h2>
   <span class="status" id="projectCount">0 projects</span>
  </div>
  <div id="projectsList" class="project-grid"></div>
 </main>
</section>

<!-- FULL SCREEN EDITOR -->
<section id="editorScreen" class="hidden">
 <header class="editor-top">
  <div>
   <div class="editor-title" id="editorProjectName">New Project</div>
   <div class="status" id="saveStatus">Not committed</div>
  </div>
  <div class="editor-buttons">
   <button class="btn secondary" id="verifyBtn">Verify Errors</button>
   <button class="btn green" id="correctBtn">Correct Errors</button>
   <button class="btn" id="commitBtn">Commit</button>
   <button class="btn secondary" id="closeEditorBtn">✕</button>
  </div>
 </header>

 <nav class="editor-tabs">
  <button class="tab active" data-file="html">HTML</button>
  <button class="tab" data-file="css">CSS</button>
  <button class="tab" data-file="js">JavaScript</button>
 </nav>

 <div class="editors">
  <div class="editor-pane active" id="pane-html"><textarea id="code-html"></textarea></div>
  <div class="editor-pane" id="pane-css"><textarea id="code-css"></textarea></div>
  <div class="editor-pane" id="pane-js"><textarea id="code-js"></textarea></div>
 </div>

 <div class="bottom-panel">
  <div class="bottom-head">
   <strong>Code Diagnostics</strong>
   <span class="status" id="diagnosticCount">Not checked</span>
  </div>
  <div id="diagnostics">
   <div class="status">Press Verify Errors to inspect your project.</div>
  </div>
 </div>
</section>

<!-- PROJECT ACTIONS -->
<div id="contextMenu" class="hidden">
 <button data-action="open">Open Project</button>
 <button data-action="share">Share</button>
 <button data-action="download">Download Code</button>
 <button data-action="verify">Verify Errors</button>
 <button data-action="correct">Correct Errors</button>
 <button data-action="gemalot">Ask Gemalot (Add-on)</button>
 <button data-action="delete" class="danger-text">Delete Project</button>
</div>

<!-- NEW PROJECT MODAL -->
<div id="modalBackdrop" class="hidden">
 <div class="modal">
  <h3>Start Writing</h3>
  <p class="muted">Enter a name for your new project.</p>
  <input id="newProjectName" placeholder="My awesome project">
  <div class="modal-actions">
   <button class="btn secondary" id="cancelNewProject">Cancel</button>
   <button class="btn" id="createProjectBtn">Create</button>
  </div>
 </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/xml/xml.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/javascript/javascript.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/css/css.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/htmlmixed/htmlmixed.min.js"></script>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/13.0.0/firebase-app.js";
import {
 getAuth,
 onAuthStateChanged,
 setPersistence,
 browserLocalPersistence,
 signOut
} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-auth.js";

/* FIREBASE CONFIG */
const firebaseConfig = {
 apiKey: "AIzaSyBrv1ky0Br5nLb68uvdXE0o6QdzTKpIU4g",
 authDomain: "alislamiah-ai-34202.firebaseapp.com",
 projectId: "alislamiah-ai-34202",
 storageBucket: "alislamiah-ai-34202.firebasestorage.app",
 messagingSenderId: "683051452829",
 appId: "1:683051452829:web:e96e40422c7f31e563c774",
 measurementId: "G-LFQLND010S"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);

const $ = id => document.getElementById(id);

let currentUser = null;
let currentProject = null;
let selectedProjectId = null;
let editors = {};
let diagnostics = [];

const LOGIN_URL = "https://alislamiah.github.io/Alislamiah-AI/";
const GEMALOT_URL = "https://alislamiah.github.io/Gemalot/";

function storageKey(){
 return "mga_code_projects_" + currentUser.uid;
}

function loadProjects(){
 try{
  return JSON.parse(localStorage.getItem(storageKey()) || "[]");
 }catch(e){
  return [];
 }
}

function saveProjects(projects){
 localStorage.setItem(storageKey(),JSON.stringify(projects));
}

function makeId(){
 return "mga_" + Date.now() + "_" + Math.random().toString(36).slice(2,8);
}

/* AUTH SESSION */
await setPersistence(auth,browserLocalPersistence);

onAuthStateChanged(auth,user=>{
 currentUser = user;

 $("accountLoading").classList.add("hidden");
 $("accountContent").classList.add("hidden");
 $("noAccount").classList.add("hidden");

 if(!user){
  $("accountScreen").classList.remove("hidden");
  $("appScreen").classList.add("hidden");
  $("editorScreen").classList.add("hidden");
  $("noAccount").classList.remove("hidden");
  return;
 }

 $("accountScreen").classList.remove("hidden");
 $("appScreen").classList.add("hidden");
 $("accountContent").classList.remove("hidden");

 const email = user.email || "Alislamiah account";
 $("accountName").textContent = user.displayName || "Alislamiah Account";
 $("accountEmail").textContent = email;
 $("accountAvatar").textContent = (user.displayName || email || "A").charAt(0).toUpperCase();
});

$("loginBtn").onclick = ()=>location.href=LOGIN_URL;
$("changeAccountBtn").onclick = async ()=>{
 await signOut(auth);
 location.href=LOGIN_URL;
};

$("continueBtn").onclick = ()=>{
 if(!currentUser){
  location.href=LOGIN_URL;
  return;
 }
 $("accountScreen").classList.add("hidden");
 $("appScreen").classList.remove("hidden");
 $("userEmail").textContent=currentUser.email || "Account";
 renderProjects();
};

$("signOutBtn").onclick=async()=>{
 await signOut(auth);
 location.href=LOGIN_URL;
};

/* EDITORS */
function initializeEditors(){
 if(Object.keys(editors).length) return;

 editors.html=CodeMirror.fromTextArea($("code-html"),{
  mode:"htmlmixed",theme:"material-darker",lineNumbers:true,
  lineWrapping:true,indentUnit:2,tabSize:2
 });
 editors.css=CodeMirror.fromTextArea($("code-css"),{
  mode:"css",theme:"material-darker",lineNumbers:true,
  lineWrapping:true,indentUnit:2,tabSize:2
 });
 editors.js=CodeMirror.fromTextArea($("code-js"),{
  mode:"javascript",theme:"material-darker",lineNumbers:true,
  lineWrapping:true,indentUnit:2,tabSize:2
 });

 Object.values(editors).forEach(editor=>{
  editor.on("change",()=>{
   $("saveStatus").textContent="Unsaved changes";
  });
 });
}

function getProjectCode(){
 return {
  html:editors.html.getValue(),
  css:editors.css.getValue(),
  js:editors.js.getValue()
 };
}

function setProjectCode(code={}){
 editors.html.setValue(code.html || "");
 editors.css.setValue(code.css || "");
 editors.js.setValue(code.js || "");
 Object.values(editors).forEach(e=>e.refresh());
}

function openEditor(project){
 initializeEditors();
 currentProject=project;
 $("editorProjectName").textContent=project.name;
 setProjectCode(project.code || {});
 $("saveStatus").textContent="Ready";
 $("diagnostics").innerHTML='<div class="status">Press Verify Errors to inspect your project.</div>';
 $("diagnosticCount").textContent="Not checked";
 clearAllMarks();

 $("appScreen").classList.add("hidden");
 $("editorScreen").classList.remove("hidden");
 switchTab("html");
}

function closeEditor(){
 $("editorScreen").classList.add("hidden");
 $("appScreen").classList.remove("hidden");
 renderProjects();
}

$("closeEditorBtn").onclick=closeEditor;

function switchTab(file){
 document.querySelectorAll(".tab").forEach(t=>{
  t.classList.toggle("active",t.dataset.file===file);
 });
 document.querySelectorAll(".editor-pane").forEach(p=>p.classList.remove("active"));
 $("pane-"+file).classList.add("active");
 if(editors[file]) editors[file].refresh();
}

document.querySelectorAll(".tab").forEach(tab=>{
 tab.onclick=()=>switchTab(tab.dataset.file);
});

/* CREATE PROJECT */
$("startWritingBtn").onclick=()=>{
 $("newProjectName").value="";
 $("modalBackdrop").classList.remove("hidden");
 $("newProjectName").focus();
};
$("cancelNewProject").onclick=()=>$("modalBackdrop").classList.add("hidden");

$("createProjectBtn").onclick=()=>{
 const name=$("newProjectName").value.trim() || "Untitled Project";
 const project={
  id:makeId(),
  name,
  code:{html:"<!DOCTYPE html>\n<html>\n<head>\n  <meta charset=\"UTF-8\">\n  <title>"+name+"</title>\n</head>\n<body>\n  <h1>Hello World</h1>\n</body>\n</html>",css:"",js:""},
  createdAt:Date.now(),
  updatedAt:Date.now()
 };
 const projects=loadProjects();
 projects.unshift(project);
 saveProjects(projects);
 $("modalBackdrop").classList.add("hidden");
 openEditor(project);
};

/* COMMIT */
$("commitBtn").onclick=()=>{
 if(!currentProject)return;

 const projects=loadProjects();
 const code=getProjectCode();
 const index=projects.findIndex(p=>p.id===currentProject.id);

 currentProject.code=code;
 currentProject.updatedAt=Date.now();

 if(index>=0) projects[index]=currentProject;
 else projects.unshift(currentProject);

 saveProjects(projects);
 $("saveStatus").textContent="Committed successfully";
 $("saveStatus").style.color="var(--green)";
 setTimeout(()=>$("saveStatus").style.color="",1600);
};

/* PROJECT LIST */
function renderProjects(){
 const projects=loadProjects();
 $("projectCount").textContent=projects.length+" projects";
 const container=$("projectsList");
 container.innerHTML="";

 if(!projects.length){
  container.innerHTML='<div class="empty">No projects yet. Press Start Writing to create your first project.</div>';
  return;
 }

 projects.sort((a,b)=>(b.updatedAt||0)-(a.updatedAt||0));

 projects.forEach(project=>{
  const card=document.createElement("div");
  card.className="project-card";
  card.innerHTML=`
   <div class="project-icon">〈/〉</div>
   <h3></h3>
   <p></p>
  `;
  card.querySelector("h3").textContent=project.name;
  card.querySelector("p").textContent="Last edited: "+new Date(project.updatedAt||project.createdAt).toLocaleString();
  card.onclick=()=>openEditor(project);

  let pressTimer;
  let longPressed=false;

  card.addEventListener("pointerdown",()=>{
   longPressed=false;
   pressTimer=setTimeout(()=>{
    longPressed=true;
    showContextMenu(project,card);
   },600);
  });
  ["pointerup","pointerleave","pointercancel"].forEach(ev=>{
   card.addEventListener(ev,()=>clearTimeout(pressTimer));
  });
  card.addEventListener("click",()=>{
   if(longPressed)return;
   openEditor(project);
  });

  container.appendChild(card);
 });
}

/* LONG PRESS MENU */
function showContextMenu(project,element){
 selectedProjectId=project.id;
 const menu=$("contextMenu");
 const rect=element.getBoundingClientRect();
 menu.style.left=Math.min(rect.left,window.innerWidth-230)+"px";
 menu.style.top=Math.min(rect.bottom+5,window.innerHeight-330)+"px";
 menu.classList.remove("hidden");
}

document.addEventListener("click",e=>{
 if(!e.target.closest("#contextMenu") && !e.target.closest(".project-card")){
  $("contextMenu").classList.add("hidden");
 }
});

$("contextMenu").addEventListener("click",e=>{
 const action=e.target.dataset.action;
 if(!action)return;
 $("contextMenu").classList.add("hidden");

 const project=loadProjects().find(p=>p.id===selectedProjectId);
 if(!project)return;

 if(action==="open")openEditor(project);
 if(action==="share")shareProject(project);
 if(action==="download")downloadProject(project);
 if(action==="verify"){
  openEditor(project);
  setTimeout(verifyErrors,250);
 }
 if(action==="correct"){
  openEditor(project);
   setTimeout(correctErrors,250);
 }
 if(action==="gemalot"){
  openEditor(project);
  sendToGemalot(project);
 }
 if(action==="delete"){
  if(confirm("Delete this project permanently?")){
   saveProjects(loadProjects().filter(p=>p.id!==project.id));
   renderProjects();
  }
 }
});

/* SHARE */
async function shareProject(project){
 const source=buildHTML(project.code);
 try{
  if(navigator.share){
   await navigator.share({title:project.name,text:source});
  }else{
   await navigator.clipboard.writeText(source);
   alert("Project code copied.");
  }
 }catch(e){
  try{
   await navigator.clipboard.writeText(source);
   alert("Project code copied.");
  }catch(_){
   alert("Unable to share this project on this browser.");
  }
 }
}

/* DOWNLOAD */
function buildHTML(code){
 const html=code.html || "<!DOCTYPE html><html><head></head><body></body></html>";
 const style=code.css ? "\n<style>\n"+code.css+"\n</style>\n" : "";
 const script=code.js ? "\n<script>\n"+code.js.replace(/<\/script/gi,"<\\/script")+"\n<\/script>\n" : "";

 if(/<\/head>/i.test(html)){
  return html.replace(/<\/head>/i,style+"</head>").replace(/<\/body>/i,script+"</body>");
 }

 const withStyle=html.replace(/<html[^>]*>/i,match=>match+"\n<head>"+style+"</head>");
 return withStyle.replace(/<\/body>/i,script+"</body>");
}

function downloadProject(project){
 const source=buildHTML(project.code||{});
 const blob=new Blob([source],{type:"text/html;charset=utf-8"});
 const url=URL.createObjectURL(blob);
 const a=document.createElement("a");
 a.href=url;
 a.download=(project.name||"MGA-project").replace(/[^\w\-]+/g,"_")+".html";
 a.click();
 URL.revokeObjectURL(url);
}

/* ERROR MARKERS */
function clearAllMarks(){
 Object.values(editors).forEach(editor=>{
  for(let i=0;i<editor.lineCount();i++){
   editor.removeLineClass(i,"background","error-line");
   editor.setGutterMarker(i,"mga-errors",null);
  }
 });
}

function markError(file,line,message){
 const editor=editors[file];
 if(!editor)return;

 const lineIndex=Math.max(0,Math.min((line||1)-1,editor.lineCount()-1));
 editor.addLineClass(lineIndex,"background","error-line");

 const marker=document.createElement("span");
 marker.className="error-gutter";
 marker.textContent="●";
 marker.title=message;

 editor.setGutterMarker(lineIndex,"mga-errors",marker);
}

/* ADD ERROR GUTTER */
function installGutters(){
 Object.values(editors).forEach(editor=>{
  editor.setOption("gutters",["CodeMirror-linenumbers","mga-errors"]);
 });
}

/* BASIC LOCAL DIAGNOSTICS */
function checkJavaScript(source){
 if(!source.trim())return [];

 try{
  new Function(source);
  return [];
 }catch(error){
  const match=String(error.stack||"").match(/<anonymous>:(\d+):(\d+)/);

  return [{
   file:"js",
   line:match?Number(match[1]):1,
   message:error.message || "JavaScript syntax error",
   type:"syntax"
  }];
 }
}

function checkCSS(source){
 if(!source.trim())return [];

 const errors=[];
 let depth=0;
 let quote=null;
 let comment=false;
 let line=1;
 let startLine=1;

 for(let i=0;i<source.length;i++){
  const c=source[i],n=source[i+1];

  if(c==="\n")line++;

  if(comment){
   if(c==="*"&&n==="/"){
    comment=false;
    i++;
   }
   continue;
  }

  if(!quote&&c==="/"&&n==="*"){
   comment=true;
   i++;
   continue;
  }

  if(quote){
   if(c==="\\"){
    i++;
    continue;
   }
   if(c===quote)quote=null;
   continue;
  }

  if(c==="'"||c==='"'){
   quote=c;
   continue;
  }

  if(c==="{"){
   depth++;
   startLine=line;
  }

  if(c==="}"){
   depth--;

   if(depth<0){
    errors.push({
     file:"css",
     line,
     message:"Unexpected closing brace }"
    });
    depth=0;
   }
  }
 }

 if(depth>0){
  errors.push({
   file:"css",
   line:startLine,
   message:"Missing closing brace }"
  });
 }

 if(quote){
  errors.push({
   file:"css",
   line,
   message:"Unclosed string"
  });
 }

 return errors;
}

function checkHTML(source){
 if(!source.trim())return [];

 const errors=[];
 const doc=new DOMParser().parseFromString(source,"text/html");
 const parserError=doc.querySelector("parsererror");

 if(parserError){
  errors.push({
   file:"html",
   line:1,
   message:"HTML parsing issue: "+parserError.textContent.slice(0,150)
  });
 }

 return errors;
}

function verifyErrors(){
 if(!currentProject)return;

 clearAllMarks();
 diagnostics=[];

 const code=getProjectCode();

 diagnostics.push(...checkJavaScript(code.js));
 diagnostics.push(...checkCSS(code.css));
 diagnostics.push(...checkHTML(code.html));

 diagnostics.forEach(error=>{
  markError(error.file,error.line,error.message);
 });

 $("diagnosticCount").textContent=diagnostics.length+" issue(s) found";

 const box=$("diagnostics");

 if(!diagnostics.length){
  box.innerHTML='<div class="success-item">✓ No detectable syntax errors found in the current checks.</div>';
  return;
 }

 box.innerHTML="";

 diagnostics.forEach((error,index)=>{
  const item=document.createElement("div");
  item.className="error-item";
  item.textContent=(index+1)+". "+error.file.toUpperCase()+" — Line "+error.line+": "+error.message;

  item.onclick=()=>{
   switchTab(error.file);
   editors[error.file].setCursor({
    line:Math.max(0,error.line-1),
    ch:0
   });
   editors[error.file].focus();
  };

  box.appendChild(item);
 });
}

/* SAFE LOCAL REPAIR ENGINE */
function repairJavaScript(source){
 let stack=[];
 let quote=null;
 let lineComment=false;
 let blockComment=false;
 let escaped=false;

 for(let i=0;i<source.length;i++){
  const c=source[i],n=source[i+1];

  if(lineComment){
   if(c==="\n")lineComment=false;
   continue;
  }

  if(blockComment){
   if(c==="*"&&n==="/"){
    blockComment=false;
    i++;
   }
   continue;
  }

  if(quote){
   if(escaped){
    escaped=false;
    continue;
   }

   if(c==="\\"){
    escaped=true;
    continue;
   }

   if(c===quote)quote=null;
   continue;
  }

  if(c==="/"&&n==="/"){
   lineComment=true;
   i++;
   continue;
  }

  if(c==="/"&&n==="*"){
   blockComment=true;
   i++;
   continue;
  }

  if(c==="'"||c==='"'||c==="`"){
   quote=c;
   continue;
  }

  if(c==="("||c==="["||c==="{"){
   stack.push(c);
  }

  if(c===")"||c==="]"||c==="}"){
   const expected={
    ")":"(",
    "]":"[",
    "}":"{"
   }[c];

   if(stack[stack.length-1]===expected){
    stack.pop();
   }else{
    return {
     code:source,
     changed:false,
     notes:["A mismatched bracket was found. Automatic repair was skipped to avoid damaging your code."]
    };
   }
  }
 }

 if(quote||blockComment){
  return {
   code:source,
   changed:false,
   notes:["An unfinished string or comment was found. Manual review is required."]
  };
 }

 if(!stack.length){
  return {
   code:source,
   changed:false,
   notes:["No safe automatic JavaScript structural correction was found."]
  };
 }

 const closers=stack.reverse().map(open=>({
  "(":")",
  "[":"]",
  "{":"}"
 }[open])).join("");

 return {
  code:source+"\n"+closers,
  changed:true,
  notes:["Added missing closing brackets at the end of the JavaScript file."]
 };
}

function repairCSS(source){
 let result=source;
 let changed=false;

 result=result.replace(/([^;{}\s])\s*}/g,(whole,last,index)=>{
  const before=result.slice(0,index);
  const line=before.slice(before.lastIndexOf("{")+1);

  if(line.includes(":")&&!line.trim().startsWith("@")){
   changed=true;
   return last+";}";
  }

  return whole;
 });

 let depth=0;
 let quote=null;
 let comment=false;

 for(let i=0;i<result.length;i++){
  const c=result[i],n=result[i+1];

  if(comment){
   if(c==="*"&&n==="/"){
    comment=false;
    i++;
   }
   continue;
  }

  if(!quote&&c==="/"&&n==="*"){
   comment=true;
   i++;
   continue;
  }

  if(quote){
   if(c==="\\"){
    i++;
    continue;
   }
   if(c===quote)quote=null;
   continue;
  }

  if(c==="'"||c==='"'){
   quote=c;
   continue;
  }

  if(c==="{")depth++;
  if(c==="}")depth=Math.max(0,depth-1);
 }

 if(depth>0){
  result+="\n"+"}".repeat(depth);
  changed=true;
 }

 return {
  code:result,
  changed,
  notes:changed
   ?["Applied limited CSS structural corrections."]
   :["No safe automatic CSS correction was found."]
 };
}

function repairHTML(source){
 return {
  code:source,
  changed:false,
  notes:["HTML was left unchanged. Review the reported markup manually."]
 };
}

function correctErrors(){
 if(!currentProject)return;

 const before=getProjectCode();

 const jsFix=repairJavaScript(before.js);
 const cssFix=repairCSS(before.css);
 const htmlFix=repairHTML(before.html);

 const repaired={
  html:htmlFix.code,
  css:cssFix.code,
  js:jsFix.code
 };

 const changed=
  repaired.html!==before.html||
  repaired.css!==before.css||
  repaired.js!==before.js;

 if(!changed){
  $("diagnostics").innerHTML="";

  [...jsFix.notes,...cssFix.notes,...htmlFix.notes].forEach(note=>{
   const div=document.createElement("div");
   div.className="error-item";
   div.textContent=note;
   $("diagnostics").appendChild(div);
  });

  $("diagnosticCount").textContent="No safe fixes applied";
  return;
 }

 setProjectCode(repaired);
 currentProject.code=repaired;

 $("saveStatus").textContent="Corrections applied — press Commit to save";

 $("diagnostics").innerHTML="";

 [...jsFix.notes,...cssFix.notes,...htmlFix.notes].forEach(note=>{
  const div=document.createElement("div");
  div.className="success-item";
  div.textContent="✓ "+note;
  $("diagnostics").appendChild(div);
 });

 $("diagnosticCount").textContent="Corrections applied";
 clearAllMarks();
}

$("verifyBtn").onclick=()=>{
 initializeEditors();
 installGutters();
 verifyErrors();
};

$("correctBtn").onclick=()=>{
 initializeEditors();
 installGutters();
 correctErrors();
};

/* GEMALOT OPTIONAL ADD-ON */
function sendToGemalot(project){
 const request={
  source:"MGA Code",
  projectId:project.id,
  projectName:project.name,
  code:project.code||{},
  returnUrl:location.href,
  createdAt:Date.now()
 };

 localStorage.setItem(
  "mga_gemalot_addon_request",
  JSON.stringify(request)
 );

 window.open(GEMALOT_URL,"_blank");
}

/* INITIALIZATION */
initializeEditors();
installGutters();

</script>
</body>
</html>