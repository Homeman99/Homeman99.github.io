# Homeman99.github.io
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>CodeForge — Editor</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet"/>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.css"/>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/dracula.min.css"/>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/fold/foldgutter.min.css"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/htmlmixed/htmlmixed.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/css/css.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/javascript/javascript.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/mode/xml/xml.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/edit/closebrackets.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/edit/closetag.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/edit/matchbrackets.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/comment/comment.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/selection/active-line.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/search/searchcursor.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/fold/foldcode.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/fold/foldgutter.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/fold/brace-fold.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/fold/xml-fold.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/hint/show-hint.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/hint/html-hint.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/hint/css-hint.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/hint/javascript-hint.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/hint/show-hint.min.css"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0d0e14;
  --surface:#13151f;
  --surface2:#1a1d2a;
  --surface3:#20243a;
  --border:#252840;
  --accent:#ff6b35;
  --accent2:#7c5cfc;
  --green:#2dce89;
  --red:#f75f6e;
  --yellow:#ffd060;
  --text:#e4e6f0;
  --text-dim:#7a7f9a;
  --font-mono:'JetBrains Mono',monospace;
  --font-ui:'Syne',sans-serif;
}
html,body{height:100%;overflow:hidden;background:var(--bg);color:var(--text)}
body{display:flex;flex-direction:column;font-family:var(--font-ui)}

/* TOP BAR */
#topbar{
display:flex;align-items:center;gap:0;
height:48px;background:var(–surface);
border-bottom:1px solid var(–border);
padding:0 12px;gap:8px;
position:relative;z-index:100;
}
#logo{
font-family:var(–font-ui);font-weight:800;font-size:17px;
color:var(–accent);letter-spacing:-0.5px;margin-right:12px;
white-space:nowrap;
}
#logo span{color:var(–accent2)}

.tab-bar{display:flex;flex:1;gap:2px;overflow-x:auto;align-items:center}
.tab-bar::-webkit-scrollbar{height:3px}
.tab-bar::-webkit-scrollbar-track{background:transparent}
.tab-bar::-webkit-scrollbar-thumb{background:var(–border)}

.tab{
display:flex;align-items:center;gap:6px;
padding:6px 14px;border-radius:6px 6px 0 0;
font-size:12px;font-family:var(–font-mono);
cursor:pointer;white-space:nowrap;
color:var(–text-dim);background:transparent;
border:1px solid transparent;border-bottom:none;
transition:all .15s;position:relative;top:1px;
user-select:none;
}
.tab:hover{color:var(–text);background:var(–surface2)}
.tab.active{
color:var(–text);background:var(–surface2);
border-color:var(–border);
}
.tab .tab-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.tab .tab-dot.html{background:#e44d26}
.tab .tab-dot.css{background:#264de4}
.tab .tab-dot.js{background:#f7df1e}
.tab .tab-close{
opacity:0;font-size:14px;line-height:1;
color:var(–text-dim);transition:opacity .15s;
padding:1px 3px;border-radius:3px;
}
.tab:hover .tab-close,.tab.active .tab-close{opacity:1}
.tab .tab-close:hover{color:var(–red);background:rgba(247,95,110,.15)}

.new-tab-btn{
padding:4px 10px;border-radius:5px;font-size:18px;
color:var(–text-dim);cursor:pointer;flex-shrink:0;
transition:color .15s;
}
.new-tab-btn:hover{color:var(–accent)}

.topbar-actions{display:flex;gap:6px;margin-left:auto;flex-shrink:0}
.tb-btn{
display:flex;align-items:center;gap:5px;
padding:5px 12px;border-radius:6px;font-size:12px;
font-family:var(–font-ui);font-weight:600;
cursor:pointer;border:none;transition:all .15s;
white-space:nowrap;
}
.tb-btn.primary{background:var(–accent);color:#fff}
.tb-btn.primary:hover{background:#e55a25}
.tb-btn.secondary{background:var(–surface3);color:var(–text);border:1px solid var(–border)}
.tb-btn.secondary:hover{background:var(–border)}
.tb-btn.run{background:var(–green);color:#fff}
.tb-btn.run:hover{background:#25b876}

/* MAIN LAYOUT */
#main{display:flex;flex:1;overflow:hidden}

/* SIDEBAR */
#sidebar{
width:220px;flex-shrink:0;
background:var(–surface);
border-right:1px solid var(–border);
display:flex;flex-direction:column;
overflow:hidden;
transition:width .2s;
}
#sidebar.collapsed{width:0}
.sidebar-section{border-bottom:1px solid var(–border)}
.sidebar-header{
padding:8px 12px;font-size:11px;font-weight:600;
color:var(–text-dim);letter-spacing:.8px;text-transform:uppercase;
display:flex;align-items:center;justify-content:space-between;
}
.file-tree{padding:4px 0}
.file-item{
display:flex;align-items:center;gap:7px;
padding:5px 12px;font-family:var(–font-mono);font-size:12px;
cursor:pointer;color:var(–text-dim);
transition:all .12s;
user-select:none;
}
.file-item:hover{background:var(–surface2);color:var(–text)}
.file-item.active{background:var(–surface3);color:var(–text);border-left:2px solid var(–accent)}
.file-icon{font-size:13px}

.sidebar-tools{display:flex;flex-direction:column;padding:8px 0}
.side-tool{
display:flex;align-items:center;gap:8px;
padding:8px 12px;font-size:12px;
cursor:pointer;color:var(–text-dim);
transition:all .12s;
}
.side-tool:hover{background:var(–surface2);color:var(–text)}
.side-tool .sticon{font-size:15px}

/* EDITOR AREA */
#editor-area{
flex:1;display:flex;flex-direction:column;overflow:hidden;
position:relative;
}
.editor-wrapper{
flex:1;display:none;overflow:hidden;position:relative;
}
.editor-wrapper.active{display:flex;flex-direction:column}

.CodeMirror{
height:100%!important;
font-family:var(–font-mono)!important;
font-size:14px!important;
line-height:1.7!important;
background:#0d0e14!important;
}
.CodeMirror-scroll{padding-bottom:20px}
.CodeMirror-gutters{background:#11121a!important;border-right:1px solid var(–border)!important}
.CodeMirror-linenumber{color:#3d4260!important;padding:0 10px!important}
.CodeMirror-activeline-background{background:rgba(255,255,255,.03)!important}
.CodeMirror-selected{background:rgba(124,92,252,.3)!important}
.CodeMirror-cursor{border-left:2px solid var(–accent)!important}
.CodeMirror-foldgutter-open,.CodeMirror-foldgutter-folded{color:var(–accent2)!important}

/* SPLIT / PREVIEW */
#workspace{display:flex;flex:1;overflow:hidden}
#editor-panel{flex:1;display:flex;flex-direction:column;overflow:hidden;position:relative}
#divider{
width:5px;background:var(–border);cursor:col-resize;flex-shrink:0;
transition:background .15s;position:relative;
}
#divider:hover,#divider.dragging{background:var(–accent2)}
#divider::after{
content:‘⋮’;position:absolute;top:50%;left:50%;
transform:translate(-50%,-50%);color:var(–text-dim);font-size:14px;
}
#preview-panel{
width:40%;flex-shrink:0;display:flex;flex-direction:column;overflow:hidden;
background:var(–surface);border-left:1px solid var(–border);
}
#preview-panel.hidden{width:0;border:none}

.panel-header{
height:36px;background:var(–surface2);
border-bottom:1px solid var(–border);
display:flex;align-items:center;justify-content:space-between;
padding:0 12px;flex-shrink:0;
}
.panel-title{font-size:11px;font-weight:600;color:var(–text-dim);letter-spacing:.5px;text-transform:uppercase}
.panel-actions{display:flex;gap:4px}
.icon-btn{
padding:3px 7px;border-radius:4px;font-size:12px;
cursor:pointer;color:var(–text-dim);border:1px solid transparent;
transition:all .12s;
}
.icon-btn:hover{color:var(–text);background:var(–surface3);border-color:var(–border)}

#preview-frame{
flex:1;border:none;background:#fff;
}

/* STATUS BAR */
#statusbar{
height:24px;background:var(–surface);border-top:1px solid var(–border);
display:flex;align-items:center;padding:0 12px;gap:16px;
font-family:var(–font-mono);font-size:11px;color:var(–text-dim);
flex-shrink:0;
}
.status-item{display:flex;align-items:center;gap:4px}
.status-dot{width:6px;height:6px;border-radius:50%;background:var(–green)}
#cursor-pos{margin-left:auto}

/* NOTIFICATIONS */
#notif{
position:fixed;bottom:36px;right:16px;z-index:999;
display:flex;flex-direction:column;gap:6px;pointer-events:none;
}
.notif-item{
padding:8px 16px;border-radius:8px;font-size:12px;font-family:var(–font-mono);
color:#fff;pointer-events:none;
animation:notifIn .25s ease forwards;
max-width:280px;
}
.notif-item.success{background:var(–green)}
.notif-item.error{background:var(–red)}
.notif-item.info{background:var(–accent2)}
@keyframes notifIn{from{opacity:0;transform:translateX(20px)}to{opacity:1;transform:none}}

/* SEARCH BAR */
#search-bar{
display:none;padding:8px 12px;background:var(–surface2);
border-bottom:1px solid var(–border);
gap:8px;align-items:center;
}
#search-bar.visible{display:flex}
#search-input{
flex:1;background:var(–surface3);border:1px solid var(–border);
color:var(–text);padding:4px 8px;border-radius:5px;
font-family:var(–font-mono);font-size:12px;outline:none;
}
#search-input:focus{border-color:var(–accent2)}

/* MODAL */
#modal-overlay{
display:none;position:fixed;inset:0;
background:rgba(0,0,0,.7);backdrop-filter:blur(4px);
z-index:500;align-items:center;justify-content:center;
}
#modal-overlay.visible{display:flex}
#modal{
background:var(–surface);border:1px solid var(–border);
border-radius:12px;padding:24px;width:400px;max-width:90vw;
}
#modal h2{font-size:16px;font-weight:600;margin-bottom:16px;color:var(–text)}
.modal-input{
width:100%;background:var(–surface2);border:1px solid var(–border);
color:var(–text);padding:8px 12px;border-radius:6px;
font-family:var(–font-mono);font-size:13px;outline:none;margin-bottom:12px;
}
.modal-input:focus{border-color:var(–accent2)}
.modal-actions{display:flex;justify-content:flex-end;gap:8px;margin-top:8px}

/* CONTEXT MENU */
#ctx-menu{
display:none;position:fixed;z-index:600;
background:var(–surface2);border:1px solid var(–border);
border-radius:8px;padding:4px;min-width:160px;
box-shadow:0 8px 32px rgba(0,0,0,.5);
}
#ctx-menu.visible{display:block}
.ctx-item{
padding:7px 12px;font-size:12px;cursor:pointer;
border-radius:5px;color:var(–text-dim);
transition:all .1s;display:flex;align-items:center;gap:8px;
}
.ctx-item:hover{background:var(–surface3);color:var(–text)}
.ctx-sep{height:1px;background:var(–border);margin:3px 0}

/* SCROLLBAR */
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(–border);border-radius:3px}
::-webkit-scrollbar-thumb:hover{background:#363b58}

/* RESIZABLE */
.CodeMirror-hints{
background:var(–surface2)!important;border:1px solid var(–border)!important;
font-family:var(–font-mono)!important;font-size:12px!important;
border-radius:6px!important;
}
.CodeMirror-hint{color:var(–text)!important;padding:4px 12px!important}
.CodeMirror-hint-active{background:var(–accent2)!important;color:#fff!important}

/* TOOLBAR */
#editor-toolbar{
height:36px;background:var(–surface2);border-bottom:1px solid var(–border);
display:flex;align-items:center;padding:0 8px;gap:2px;flex-shrink:0;
}
.et-btn{
padding:4px 8px;border-radius:4px;font-size:11px;font-weight:600;
cursor:pointer;color:var(–text-dim);
font-family:var(–font-mono);transition:all .12s;
border:1px solid transparent;
}
.et-btn:hover{color:var(–text);background:var(–surface3)}
.et-sep{width:1px;height:16px;background:var(–border);margin:0 4px}
.et-lang{
margin-left:auto;font-size:10px;
background:var(–surface3);padding:2px 8px;
border-radius:4px;color:var(–text-dim);letter-spacing:.5px;
}

/* Minimap */
#minimap{
width:60px;background:#0a0b10;border-left:1px solid var(–border);
overflow:hidden;cursor:pointer;flex-shrink:0;display:none;
position:relative;
}
#minimap.visible{display:block}
#minimap canvas{width:100%;height:100%}

/* FIND/REPLACE */
#findreplace{
display:none;position:absolute;right:12px;top:44px;z-index:50;
background:var(–surface2);border:1px solid var(–border);
border-radius:8px;padding:10px;width:320px;
box-shadow:0 4px 24px rgba(0,0,0,.4);
}
#findreplace.visible{display:block}
.fr-row{display:flex;gap:6px;margin-bottom:6px;align-items:center}
.fr-input{
flex:1;background:var(–surface3);border:1px solid var(–border);
color:var(–text);padding:4px 8px;border-radius:4px;
font-family:var(–font-mono);font-size:12px;outline:none;
}
.fr-input:focus{border-color:var(–accent2)}
.fr-btn{
padding:4px 8px;border-radius:4px;font-size:11px;cursor:pointer;
background:var(–surface3);color:var(–text-dim);border:1px solid var(–border);
transition:all .1s;white-space:nowrap;
}
.fr-btn:hover{color:var(–text);border-color:var(–accent2)}

/* ANIMATIONS */
@keyframes fadeIn{from{opacity:0;transform:translateY(-4px)}to{opacity:1;transform:none}}
#topbar,#editor-toolbar,#statusbar{animation:fadeIn .3s ease}

.kb-badge{
display:inline-flex;align-items:center;gap:2px;
background:var(–surface3);border:1px solid var(–border);
border-radius:3px;padding:1px 5px;font-size:10px;font-family:var(–font-mono);
color:var(–text-dim);
}
</style>

</head>
<body>

<!-- TOP BAR -->

<div id="topbar">
  <div id="logo">Code<span>Forge</span></div>
  <div class="tab-bar" id="tab-bar"></div>
  <span class="new-tab-btn" id="new-tab-btn" title="New File">＋</span>
  <div class="topbar-actions">
    <button class="tb-btn secondary" id="btn-format" title="Format Code (Alt+Shift+F)">⚡ Format</button>
    <button class="tb-btn secondary" id="btn-save" title="Save (Ctrl+S)">💾 Save</button>
    <button class="tb-btn run" id="btn-run" title="Run Preview (Ctrl+Enter)">▶ Run</button>
    <button class="tb-btn primary" id="btn-export" title="Export files">⬇ Export</button>
  </div>
</div>

<!-- MAIN -->

<div id="main">
  <!-- SIDEBAR -->
  <div id="sidebar">
    <div class="sidebar-section">
      <div class="sidebar-header">
        Explorer
        <span class="icon-btn" id="btn-add-file" title="New File">+</span>
      </div>
      <div class="file-tree" id="file-tree"></div>
    </div>
    <div class="sidebar-section">
      <div class="sidebar-header">Quick Tools</div>
      <div class="sidebar-tools">
        <div class="side-tool" id="st-beautify"><span class="sticon">✨</span> Beautify Code</div>
        <div class="side-tool" id="st-minify"><span class="sticon">🗜</span> Minify JS/CSS</div>
        <div class="side-tool" id="st-copy"><span class="sticon">📋</span> Copy All</div>
        <div class="side-tool" id="st-clear"><span class="sticon">🗑</span> Clear Editor</div>
        <div class="side-tool" id="st-word-wrap"><span class="sticon">↩</span> Toggle Wrap</div>
        <div class="side-tool" id="st-fullscreen"><span class="sticon">⛶</span> Fullscreen</div>
        <div class="side-tool" id="st-find"><span class="sticon">🔍</span> Find & Replace</div>
      </div>
    </div>
    <div class="sidebar-section">
      <div class="sidebar-header">Themes</div>
      <div class="sidebar-tools" id="theme-list"></div>
    </div>
    <div class="sidebar-section">
      <div class="sidebar-header">Font Size</div>
      <div style="display:flex;align-items:center;gap:8px;padding:8px 12px">
        <button class="icon-btn" id="fs-dec">−</button>
        <span id="fs-val" style="font-size:12px;font-family:var(--font-mono);min-width:28px;text-align:center">14</span>
        <button class="icon-btn" id="fs-inc">+</button>
      </div>
    </div>
  </div>

  <!-- WORKSPACE -->

  <div id="workspace">
    <div id="editor-panel">
      <!-- FIND/REPLACE -->
      <div id="findreplace">
        <div class="fr-row">
          <input class="fr-input" id="find-input" placeholder="Find…"/>
          <button class="fr-btn" id="find-prev">↑</button>
          <button class="fr-btn" id="find-next">↓</button>
          <button class="fr-btn" id="findreplace-close">✕</button>
        </div>
        <div class="fr-row">
          <input class="fr-input" id="replace-input" placeholder="Replace…"/>
          <button class="fr-btn" id="replace-one">Replace</button>
          <button class="fr-btn" id="replace-all">All</button>
        </div>
        <div style="font-size:10px;color:var(--text-dim);font-family:var(--font-mono)" id="find-status"></div>
      </div>

```
  <!-- EDITOR TOOLBAR -->
  <div id="editor-toolbar">
    <button class="et-btn" id="et-undo" title="Undo">↩</button>
    <button class="et-btn" id="et-redo" title="Redo">↪</button>
    <div class="et-sep"></div>
    <button class="et-btn" id="et-bold" title="Bold / Comment">//</button>
    <button class="et-btn" id="et-indent" title="Indent">→|</button>
    <button class="et-btn" id="et-dedent" title="Dedent">|←</button>
    <div class="et-sep"></div>
    <button class="et-btn" id="et-snippet-div" title="Insert div">DIV</button>
    <button class="et-btn" id="et-snippet-fn" title="Insert function">FN</button>
    <button class="et-btn" id="et-snippet-loop" title="Insert loop">FOR</button>
    <div class="et-sep"></div>
    <button class="et-btn" id="et-toggle-preview" title="Toggle Preview">⊡</button>
    <span class="et-lang" id="et-lang">HTML</span>
  </div>

  <!-- EDITORS -->
  <div id="editors-container" style="flex:1;display:flex;overflow:hidden;position:relative">
  </div>
</div>

<!-- DIVIDER -->
<div id="divider"></div>

<!-- PREVIEW -->
<div id="preview-panel">
  <div class="panel-header">
    <span class="panel-title">🌐 Preview</span>
    <div class="panel-actions">
      <span class="icon-btn" id="btn-refresh-preview" title="Refresh">↻</span>
      <span class="icon-btn" id="btn-open-tab" title="Open in new tab">⧉</span>
      <span class="icon-btn" id="btn-close-preview" title="Close Preview">✕</span>
    </div>
  </div>
  <iframe id="preview-frame" sandbox="allow-scripts allow-same-origin allow-forms allow-popups"></iframe>
</div>
```

  </div>
</div>

<!-- STATUS BAR -->

<div id="statusbar">
  <div class="status-item"><span class="status-dot"></span><span id="st-lang">HTML</span></div>
  <div class="status-item" id="st-chars">0 chars</div>
  <div class="status-item" id="st-lines">1 line</div>
  <div class="status-item" id="st-encoding">UTF-8</div>
  <span id="cursor-pos">Ln 1, Col 1</span>
</div>

<!-- NOTIFICATIONS -->

<div id="notif"></div>

<!-- CONTEXT MENU -->

<div id="ctx-menu">
  <div class="ctx-item" data-action="copy">📋 Copy</div>
  <div class="ctx-item" data-action="cut">✂ Cut</div>
  <div class="ctx-item" data-action="paste">📌 Paste</div>
  <div class="ctx-sep"></div>
  <div class="ctx-item" data-action="selectall">☰ Select All</div>
  <div class="ctx-item" data-action="comment">// Toggle Comment</div>
  <div class="ctx-sep"></div>
  <div class="ctx-item" data-action="format">⚡ Format Code</div>
  <div class="ctx-item" data-action="duplicate">⊕ Duplicate Line</div>
</div>

<!-- MODAL -->

<div id="modal-overlay">
  <div id="modal">
    <h2 id="modal-title">New File</h2>
    <input class="modal-input" id="modal-input" placeholder="filename.html"/>
    <div style="font-size:11px;color:var(--text-dim);margin-bottom:8px" id="modal-hint">Supported: .html, .css, .js</div>
    <div class="modal-actions">
      <button class="tb-btn secondary" id="modal-cancel">Cancel</button>
      <button class="tb-btn primary" id="modal-confirm">Create</button>
    </div>
  </div>
</div>

<script>
// ============================================================
//  STATE
// ============================================================
const state = {
  files: {},          // {name: {content, mode, editor}}
  activeFile: null,
  wordWrap: false,
  fontSize: 14,
  previewVisible: true,
  currentTheme: 'dracula',
  searchCursor: null,
};

const themes = {
  dracula:    {cm:'dracula',     url:'https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/dracula.min.css'},
  monokai:    {cm:'monokai',     url:'https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/monokai.min.css'},
  'one-dark': {cm:'one-dark',    url:'https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/one-dark.min.css'},
  material:   {cm:'material',    url:'https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/material.min.css'},
  twilight:   {cm:'twilight',    url:'https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/twilight.min.css'},
  nord:       {cm:'nord',        url:'https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/nord.min.css'},
  eclipse:    {cm:'eclipse',     url:'https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/theme/eclipse.min.css'},
};

// ============================================================
//  DEFAULT CONTENT
// ============================================================
const DEFAULT_HTML = `<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My Website</title>
  <link rel="stylesheet" href="style.css"/>
</head>
<body>
  <header>
    <nav>
      <div class="logo">My Site</div>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section class="hero">
      <h1>Welcome to My Website</h1>
      <p>Built with CodeForge — your free code editor on GitHub Pages.</p>
      <button onclick="greet()">Click Me</button>
    </section>
  </main>

  <script src="app.js"><\/script>
</body>
</html>`;

const DEFAULT_CSS = `/* ===== Base Reset ===== */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Segoe UI', sans-serif;
  background: #0f0f17;
  color: #e4e6f0;
  min-height: 100vh;
}

/* ===== Navigation ===== */
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 32px;
  background: rgba(255,255,255,0.04);
  backdrop-filter: blur(10px);
  position: sticky;
  top: 0;
  z-index: 10;
  border-bottom: 1px solid rgba(255,255,255,0.08);
}

.logo {
  font-size: 20px;
  font-weight: 700;
  color: #ff6b35;
}

nav ul {
  list-style: none;
  display: flex;
  gap: 24px;
}

nav a {
  color: #aab;
  text-decoration: none;
  font-size: 14px;
  transition: color 0.2s;
}

nav a:hover { color: #fff; }

/* ===== Hero ===== */
.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 80px 32px;
  text-align: center;
  gap: 20px;
}

h1 {
  font-size: clamp(2rem, 5vw, 3.5rem);
  background: linear-gradient(135deg, #ff6b35, #7c5cfc);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero p {
  color: #7a7f9a;
  font-size: 16px;
  max-width: 480px;
}

button {
  padding: 12px 32px;
  background: #ff6b35;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 15px;
  cursor: pointer;
  transition: transform 0.15s, background 0.15s;
}

button:hover {
  background: #e55a25;
  transform: translateY(-2px);
}`;

const DEFAULT_JS = `// ===== App Logic =====
function greet() {
  const messages = [
    "Hello, World! 👋",
    "Welcome to CodeForge!",
    "Keep building amazing things! 🚀",
    "You're doing great! ✨"
  ];
  const msg = messages[Math.floor(Math.random() * messages.length)];
  alert(msg);
}

// ===== DOM Ready =====
document.addEventListener('DOMContentLoaded', () => {
  console.log('App initialized');
  animateHero();
});

function animateHero() {
  const hero = document.querySelector('.hero');
  if (!hero) return;
  hero.style.opacity = '0';
  hero.style.transform = 'translateY(20px)';
  hero.style.transition = 'all 0.6s ease';
  requestAnimationFrame(() => {
    requestAnimationFrame(() => {
      hero.style.opacity = '1';
      hero.style.transform = 'translateY(0)';
    });
  });
}`;

// ============================================================
//  HELPERS
// ============================================================
function getMode(filename) {
  if (filename.endsWith('.html') || filename.endsWith('.htm')) return {mode:'htmlmixed', hint:'html', label:'HTML'};
  if (filename.endsWith('.css')) return {mode:'css', hint:'css', label:'CSS'};
  if (filename.endsWith('.js')) return {mode:'javascript', hint:'javascript', label:'JS'};
  return {mode:'htmlmixed', hint:'html', label:'HTML'};
}

function getFileIcon(filename) {
  if (filename.endsWith('.html') || filename.endsWith('.htm')) return '🌐';
  if (filename.endsWith('.css')) return '🎨';
  if (filename.endsWith('.js')) return '⚙️';
  return '📄';
}

function getDotClass(filename) {
  if (filename.endsWith('.html')) return 'html';
  if (filename.endsWith('.css')) return 'css';
  if (filename.endsWith('.js')) return 'js';
  return '';
}

function notify(msg, type='info') {
  const el = document.createElement('div');
  el.className = `notif-item ${type}`;
  el.textContent = msg;
  document.getElementById('notif').appendChild(el);
  setTimeout(() => { el.style.transition='opacity .3s'; el.style.opacity='0'; setTimeout(()=>el.remove(),300); }, 2200);
}

function loadThemeCSS(theme) {
  const id = 'cm-theme-' + theme;
  if (!document.getElementById(id) && themes[theme]) {
    const link = document.createElement('link');
    link.rel='stylesheet'; link.id=id; link.href=themes[theme].url;
    document.head.appendChild(link);
  }
}

// ============================================================
//  FILE / EDITOR MANAGEMENT
// ============================================================
function createEditor(filename, content) {
  const modeInfo = getMode(filename);
  const wrapper = document.createElement('div');
  wrapper.className = 'editor-wrapper';
  wrapper.dataset.file = filename;

  const textArea = document.createElement('textarea');
  wrapper.appendChild(textArea);
  document.getElementById('editors-container').appendChild(wrapper);

  const editor = CodeMirror.fromTextArea(textArea, {
    mode: modeInfo.mode,
    theme: state.currentTheme,
    lineNumbers: true,
    autoCloseBrackets: true,
    autoCloseTags: true,
    matchBrackets: true,
    styleActiveLine: true,
    lineWrapping: state.wordWrap,
    foldGutter: true,
    gutters: ['CodeMirror-linenumbers','CodeMirror-foldgutter'],
    extraKeys: {
      'Ctrl-Space': 'autocomplete',
      'Ctrl-/': (cm) => cm.execCommand('toggleComment'),
      'Ctrl-S': saveToBrowser,
      'Ctrl-Enter': runPreview,
      'Alt-Shift-F': formatCode,
      'Ctrl-D': duplicateLine,
      'Ctrl-H': toggleFindReplace,
      'Tab': (cm) => {
        if (cm.somethingSelected()) cm.indentSelection('add');
        else cm.replaceSelection('  ');
      },
    },
    hintOptions: {completeSingle: false},
    value: content,
  });

  editor.on('cursorActivity', updateStatusBar);
  editor.on('change', updateStatusBar);
  editor.setSize('100%','100%');

  return editor;
}

function addFile(filename, content='') {
  if (state.files[filename]) { switchToFile(filename); return; }
  const editor = createEditor(filename, content);
  state.files[filename] = {content, editor};
  addTab(filename);
  addToFileTree(filename);
  switchToFile(filename);
  saveToBrowser();
}

function switchToFile(filename) {
  state.activeFile = filename;

  // Tabs
  document.querySelectorAll('.tab').forEach(t => t.classList.toggle('active', t.dataset.file===filename));
  // Editors
  document.querySelectorAll('.editor-wrapper').forEach(w => w.classList.toggle('active', w.dataset.file===filename));
  // File tree
  document.querySelectorAll('.file-item').forEach(f => f.classList.toggle('active', f.dataset.file===filename));

  const modeInfo = getMode(filename);
  document.getElementById('et-lang').textContent = modeInfo.label;
  document.getElementById('st-lang').textContent = modeInfo.label;

  setTimeout(() => { if (state.files[filename]) state.files[filename].editor.refresh(); }, 10);
  updateStatusBar();
}

function closeFile(filename) {
  const keys = Object.keys(state.files);
  if (keys.length === 1) { notify('Keep at least one file open.','error'); return; }
  
  const idx = keys.indexOf(filename);
  delete state.files[filename];
  
  // Remove tab
  const tab = document.querySelector(`.tab[data-file="${filename}"]`);
  if (tab) tab.remove();
  // Remove editor
  const wrapper = document.querySelector(`.editor-wrapper[data-file="${filename}"]`);
  if (wrapper) wrapper.remove();
  // Remove from tree
  const fi = document.querySelector(`.file-item[data-file="${filename}"]`);
  if (fi) fi.remove();
  
  if (state.activeFile === filename) {
    const remaining = Object.keys(state.files);
    switchToFile(remaining[Math.min(idx, remaining.length-1)]);
  }
  saveToBrowser();
}

function addTab(filename) {
  const tab = document.createElement('div');
  tab.className = 'tab';
  tab.dataset.file = filename;
  tab.innerHTML = `<span class="tab-dot ${getDotClass(filename)}"></span>${filename}<span class="tab-close" data-file="${filename}">✕</span>`;
  tab.addEventListener('click', (e) => {
    if (e.target.classList.contains('tab-close')) return;
    switchToFile(filename);
  });
  tab.querySelector('.tab-close').addEventListener('click', (e) => {
    e.stopPropagation();
    closeFile(filename);
  });
  document.getElementById('tab-bar').appendChild(tab);
}

function addToFileTree(filename) {
  const fi = document.createElement('div');
  fi.className = 'file-item';
  fi.dataset.file = filename;
  fi.innerHTML = `<span class="file-icon">${getFileIcon(filename)}</span>${filename}`;
  fi.addEventListener('click', () => switchToFile(filename));
  document.getElementById('file-tree').appendChild(fi);
}

// ============================================================
//  EDITOR ACTIONS
// ============================================================
function getCurrentEditor() {
  if (!state.activeFile) return null;
  return state.files[state.activeFile]?.editor;
}

function formatCode() {
  const cm = getCurrentEditor();
  if (!cm) return;
  const val = cm.getValue();
  try {
    let formatted = val;
    // Basic JS formatter
    if (state.activeFile.endsWith('.js')) {
      formatted = jsBeautify(val);
    } else if (state.activeFile.endsWith('.html')) {
      formatted = htmlBeautify(val);
    } else if (state.activeFile.endsWith('.css')) {
      formatted = cssBeautify(val);
    }
    cm.setValue(formatted);
    notify('Code formatted ✨', 'success');
  } catch(e) { notify('Format failed', 'error'); }
}

function jsBeautify(code) {
  // Simple indentation-based beautifier
  let result = '';
  let indent = 0;
  const lines = code.split('\n').map(l=>l.trim()).filter(l=>l);
  for (const line of lines) {
    if (line.startsWith('}') || line.startsWith(']') || line.startsWith(')')) indent = Math.max(0,indent-1);
    result += '  '.repeat(indent) + line + '\n';
    if (line.endsWith('{') || line.endsWith('[') || line.endsWith('(')) indent++;
  }
  return result.trim();
}

function htmlBeautify(code) {
  const voidTags = /^(area|base|br|col|embed|hr|img|input|link|meta|param|source|track|wbr)/i;
  let result = '';
  let indent = 0;
  const tagRe = /<\/?[a-z][^>]*>/gi;
  let last = 0;
  let m;
  while ((m = tagRe.exec(code)) !== null) {
    const between = code.slice(last, m.index).trim();
    if (between) result += '  '.repeat(indent) + between + '\n';
    const tag = m[0];
    const isClose = tag.startsWith('</');
    const tagName = tag.replace(/<\/?([a-z]+).*/i,'$1');
    if (isClose && !voidTags.test(tagName)) indent = Math.max(0,indent-1);
    result += '  '.repeat(indent) + tag + '\n';
    if (!isClose && !tag.endsWith('/>') && !voidTags.test(tagName)) indent++;
    last = m.index + m[0].length;
  }
  const tail = code.slice(last).trim();
  if (tail) result += '  '.repeat(indent) + tail + '\n';
  return result.trim();
}

function cssBeautify(code) {
  return code
    .replace(/\s*{\s*/g,' {\n  ')
    .replace(/;\s*/g,';\n  ')
    .replace(/\s*}\s*/g,'\n}\n')
    .split('\n').map(l=>l.trimEnd()).join('\n')
    .replace(/\n{3,}/g,'\n\n').trim();
}

function duplicateLine(cm) {
  const cur = cm.getCursor();
  const line = cm.getLine(cur.line);
  cm.replaceRange('\n'+line, {line:cur.line, ch:line.length});
  notify('Line duplicated','info');
}

function saveToBrowser() {
  try {
    const data = {};
    for (const [name, f] of Object.entries(state.files)) {
      data[name] = f.editor.getValue();
    }
    localStorage.setItem('codeforge_files', JSON.stringify(data));
    notify('Saved locally 💾','success');
  } catch(e) { notify('Save failed','error'); }
}

function loadFromBrowser() {
  try {
    const raw = localStorage.getItem('codeforge_files');
    if (!raw) return false;
    const data = JSON.parse(raw);
    for (const [name, content] of Object.entries(data)) {
      addFile(name, content);
    }
    return true;
  } catch(e) { return false; }
}

// ============================================================
//  PREVIEW
// ============================================================
function runPreview() {
  // Collect all files
  const files = {};
  for (const [name, f] of Object.entries(state.files)) {
    files[name] = f.editor.getValue();
  }
  
  // Find HTML file
  let html = files['index.html'] || Object.values(files).find((_,i)=>Object.keys(files)[i].endsWith('.html')) || '';

  // Inline CSS
  let css = '';
  for (const [name, content] of Object.entries(files)) {
    if (name.endsWith('.css')) css += content + '\n';
  }

  // Inline JS
  let js = '';
  for (const [name, content] of Object.entries(files)) {
    if (name.endsWith('.js')) js += content + '\n';
  }

  // Replace link/script tags with inline versions
  let result = html;
  result = result.replace(/<link[^>]+rel="stylesheet"[^>]*>/gi, '');
  result = result.replace(/<script[^>]+src="[^"]*\.js"[^>]*><\/script>/gi, '');
  
  // Inject CSS before </head>
  if (css) result = result.replace('</head>', `<style>\n${css}\n</style>\n</head>`);

// Inject JS before </body>
if (js) result = result.replace(’</body>’, `<script>\n${js}\n<\/script>\n</body>`);

const frame = document.getElementById(‘preview-frame’);
frame.srcdoc = result;

// Show preview panel
if (!state.previewVisible) togglePreview();
notify(‘Preview updated ▶’,‘success’);
}

function togglePreview() {
const panel = document.getElementById(‘preview-panel’);
const divider = document.getElementById(‘divider’);
state.previewVisible = !state.previewVisible;
panel.classList.toggle(‘hidden’, !state.previewVisible);
divider.style.display = state.previewVisible ? ‘’ : ‘none’;
}

// ============================================================
//  EXPORT
// ============================================================
function exportFiles() {
// Export as single ZIP-like approach: download each file
for (const [name, f] of Object.entries(state.files)) {
const content = f.editor.getValue();
const blob = new Blob([content], {type:‘text/plain’});
const a = document.createElement(‘a’);
a.href = URL.createObjectURL(blob);
a.download = name;
a.click();
URL.revokeObjectURL(a.href);
}
notify(‘Files exported ⬇’,‘success’);
}

// ============================================================
//  FIND & REPLACE
// ============================================================
let searchCursors = [];
let searchIdx = 0;

function doSearch(dir=‘next’) {
const cm = getCurrentEditor();
if (!cm) return;
const query = document.getElementById(‘find-input’).value;
if (!query) return;
const cursor = cm.getSearchCursor(query, dir===‘next’ ? cm.getCursor(‘to’) : cm.getCursor(‘from’), false);
const found = dir===‘next’ ? cursor.findNext() : cursor.findPrevious();
if (found) {
cm.setSelection(cursor.from(), cursor.to());
cm.scrollIntoView({from:cursor.from(),to:cursor.to()}, 100);
document.getElementById(‘find-status’).textContent = ‘✓ Found’;
} else {
document.getElementById(‘find-status’).textContent = ‘✕ Not found’;
}
state.searchCursor = cursor;
}

function doReplace() {
if (!state.searchCursor || !state.searchCursor.from()) { doSearch(); return; }
const rep = document.getElementById(‘replace-input’).value;
state.searchCursor.replace(rep);
doSearch();
}

function doReplaceAll() {
const cm = getCurrentEditor();
if (!cm) return;
const query = document.getElementById(‘find-input’).value;
const rep = document.getElementById(‘replace-input’).value;
if (!query) return;
let count = 0;
cm.operation(() => {
const cursor = cm.getSearchCursor(query, CodeMirror.Pos(cm.firstLine(),0), false);
while (cursor.findNext()) { cursor.replace(rep); count++; }
});
notify(`Replaced ${count} occurrences`,‘success’);
}

function toggleFindReplace() {
const fr = document.getElementById(‘findreplace’);
fr.classList.toggle(‘visible’);
if (fr.classList.contains(‘visible’)) document.getElementById(‘find-input’).focus();
}

// ============================================================
//  STATUS BAR
// ============================================================
function updateStatusBar() {
const cm = getCurrentEditor();
if (!cm) return;
const val = cm.getValue();
const cur = cm.getCursor();
document.getElementById(‘st-chars’).textContent = val.length + ’ chars’;
document.getElementById(‘st-lines’).textContent = cm.lineCount() + ’ lines’;
document.getElementById(‘cursor-pos’).textContent = `Ln ${cur.line+1}, Col ${cur.ch+1}`;
}

// ============================================================
//  THEME
// ============================================================
function setTheme(theme) {
loadThemeCSS(theme);
state.currentTheme = theme;
for (const f of Object.values(state.files)) {
f.editor.setOption(‘theme’, theme);
}
// Update theme list
document.querySelectorAll(’.theme-item’).forEach(el => {
el.style.color = el.dataset.theme===theme ? ‘var(–accent)’ : ‘’;
});
notify(’Theme: ’ + theme, ‘info’);
}

function buildThemeList() {
const container = document.getElementById(‘theme-list’);
for (const name of Object.keys(themes)) {
const el = document.createElement(‘div’);
el.className = ‘side-tool theme-item’;
el.dataset.theme = name;
el.innerHTML = `<span class="sticon">🎨</span>${name}`;
if (name===state.currentTheme) el.style.color=‘var(–accent)’;
el.addEventListener(‘click’, () => setTheme(name));
container.appendChild(el);
}
}

// ============================================================
//  FONT SIZE
// ============================================================
function setFontSize(size) {
state.fontSize = Math.min(24, Math.max(10, size));
document.getElementById(‘fs-val’).textContent = state.fontSize;
document.querySelectorAll(’.CodeMirror’).forEach(el => {
el.style.fontSize = state.fontSize + ‘px’;
});
}

// ============================================================
//  WORD WRAP
// ============================================================
function toggleWordWrap() {
state.wordWrap = !state.wordWrap;
for (const f of Object.values(state.files)) {
f.editor.setOption(‘lineWrapping’, state.wordWrap);
}
notify(’Word wrap: ’ + (state.wordWrap?‘ON’:‘OFF’),‘info’);
}

// ============================================================
//  DIVIDER DRAG
// ============================================================
function initDivider() {
const divider = document.getElementById(‘divider’);
const workspace = document.getElementById(‘workspace’);
let dragging = false, startX, startW;

divider.addEventListener(‘mousedown’, (e) => {
dragging = true;
startX = e.clientX;
const preview = document.getElementById(‘preview-panel’);
startW = preview.offsetWidth;
divider.classList.add(‘dragging’);
e.preventDefault();
});

document.addEventListener(‘mousemove’, (e) => {
if (!dragging) return;
const delta = startX - e.clientX;
const newW = Math.max(200, Math.min(window.innerWidth*0.7, startW + delta));
document.getElementById(‘preview-panel’).style.width = newW + ‘px’;
});

document.addEventListener(‘mouseup’, () => {
dragging = false;
divider.classList.remove(‘dragging’);
});
}

// ============================================================
//  CONTEXT MENU
// ============================================================
document.addEventListener(‘contextmenu’, (e) => {
const cm = e.target.closest(’.CodeMirror’);
if (!cm) return;
e.preventDefault();
const menu = document.getElementById(‘ctx-menu’);
menu.style.left = Math.min(e.clientX, window.innerWidth-180) + ‘px’;
menu.style.top = Math.min(e.clientY, window.innerHeight-200) + ‘px’;
menu.classList.add(‘visible’);
});

document.addEventListener(‘click’, () => {
document.getElementById(‘ctx-menu’).classList.remove(‘visible’);
});

document.querySelectorAll(’.ctx-item’).forEach(item => {
item.addEventListener(‘click’, () => {
const cm = getCurrentEditor();
if (!cm) return;
switch(item.dataset.action) {
case ‘copy’:       document.execCommand(‘copy’); break;
case ‘cut’:        document.execCommand(‘cut’); break;
case ‘selectall’:  cm.execCommand(‘selectAll’); break;
case ‘comment’:    cm.execCommand(‘toggleComment’); break;
case ‘format’:     formatCode(); break;
case ‘duplicate’:  duplicateLine(cm); break;
}
});
});

// ============================================================
//  MODAL
// ============================================================
function openModal() {
document.getElementById(‘modal-overlay’).classList.add(‘visible’);
document.getElementById(‘modal-input’).value = ‘’;
document.getElementById(‘modal-input’).focus();
}
function closeModal() {
document.getElementById(‘modal-overlay’).classList.remove(‘visible’);
}

document.getElementById(‘modal-confirm’).addEventListener(‘click’, () => {
const name = document.getElementById(‘modal-input’).value.trim();
if (!name) { notify(‘Enter a filename’,‘error’); return; }
if (!name.match(/.(html?|css|js)$/i)) { notify(‘Use .html, .css, or .js extension’,‘error’); return; }
addFile(name, ‘’);
closeModal();
});

document.getElementById(‘modal-cancel’).addEventListener(‘click’, closeModal);
document.getElementById(‘modal-overlay’).addEventListener(‘click’, (e) => {
if (e.target === document.getElementById(‘modal-overlay’)) closeModal();
});
document.getElementById(‘modal-input’).addEventListener(‘keydown’, (e) => {
if (e.key===‘Enter’) document.getElementById(‘modal-confirm’).click();
if (e.key===‘Escape’) closeModal();
});

// ============================================================
//  TOOLBAR BUTTONS
// ============================================================
document.getElementById(‘btn-run’).addEventListener(‘click’, runPreview);
document.getElementById(‘btn-save’).addEventListener(‘click’, saveToBrowser);
document.getElementById(‘btn-format’).addEventListener(‘click’, formatCode);
document.getElementById(‘btn-export’).addEventListener(‘click’, exportFiles);
document.getElementById(‘new-tab-btn’).addEventListener(‘click’, openModal);
document.getElementById(‘btn-add-file’).addEventListener(‘click’, openModal);
document.getElementById(‘btn-close-preview’).addEventListener(‘click’, togglePreview);
document.getElementById(‘btn-refresh-preview’).addEventListener(‘click’, runPreview);
document.getElementById(‘btn-open-tab’).addEventListener(‘click’, () => {
const frame = document.getElementById(‘preview-frame’);
const w = window.open();
w.document.write(frame.srcdoc || ‘’);
w.document.close();
});

document.getElementById(‘et-undo’).addEventListener(‘click’, ()=> getCurrentEditor()?.execCommand(‘undo’));
document.getElementById(‘et-redo’).addEventListener(‘click’, ()=> getCurrentEditor()?.execCommand(‘redo’));
document.getElementById(‘et-bold’).addEventListener(‘click’, ()=> getCurrentEditor()?.execCommand(‘toggleComment’));
document.getElementById(‘et-indent’).addEventListener(‘click’, ()=> getCurrentEditor()?.execCommand(‘indentMore’));
document.getElementById(‘et-dedent’).addEventListener(‘click’, ()=> getCurrentEditor()?.execCommand(‘indentLess’));
document.getElementById(‘et-toggle-preview’).addEventListener(‘click’, togglePreview);

document.getElementById(‘et-snippet-div’).addEventListener(‘click’, () => {
const cm = getCurrentEditor(); if(!cm) return;
cm.replaceSelection(’<div class="">\n  \n</div>’);
});
document.getElementById(‘et-snippet-fn’).addEventListener(‘click’, () => {
const cm = getCurrentEditor(); if(!cm) return;
cm.replaceSelection(‘function myFunction() {\n  \n}’);
});
document.getElementById(‘et-snippet-loop’).addEventListener(‘click’, () => {
const cm = getCurrentEditor(); if(!cm) return;
cm.replaceSelection(‘for (let i = 0; i < array.length; i++) {\n  \n}’);
});

document.getElementById(‘st-beautify’).addEventListener(‘click’, formatCode);
document.getElementById(‘st-minify’).addEventListener(‘click’, () => {
const cm = getCurrentEditor(); if(!cm) return;
const val = cm.getValue().replace(/\s+/g,’ ‘).replace(/\s*([{};:,>~+])\s*/g,’$1’).trim();
cm.setValue(val);
notify(‘Minified ✓’,‘success’);
});
document.getElementById(‘st-copy’).addEventListener(‘click’, () => {
const cm = getCurrentEditor(); if(!cm) return;
navigator.clipboard.writeText(cm.getValue()).then(()=>notify(‘Copied to clipboard 📋’,‘success’));
});
document.getElementById(‘st-clear’).addEventListener(‘click’, () => {
const cm = getCurrentEditor(); if(!cm) return;
if(confirm(‘Clear the editor?’)) { cm.setValue(’’); notify(‘Cleared’,‘info’); }
});
document.getElementById(‘st-word-wrap’).addEventListener(‘click’, toggleWordWrap);
document.getElementById(‘st-fullscreen’).addEventListener(‘click’, () => {
if(!document.fullscreenElement) document.documentElement.requestFullscreen();
else document.exitFullscreen();
});
document.getElementById(‘st-find’).addEventListener(‘click’, toggleFindReplace);

document.getElementById(‘find-next’).addEventListener(‘click’, ()=>doSearch(‘next’));
document.getElementById(‘find-prev’).addEventListener(‘click’, ()=>doSearch(‘prev’));
document.getElementById(‘replace-one’).addEventListener(‘click’, doReplace);
document.getElementById(‘replace-all’).addEventListener(‘click’, doReplaceAll);
document.getElementById(‘findreplace-close’).addEventListener(‘click’, ()=>document.getElementById(‘findreplace’).classList.remove(‘visible’));
document.getElementById(‘find-input’).addEventListener(‘keydown’, (e)=>{ if(e.key===‘Enter’) doSearch(‘next’); });

document.getElementById(‘fs-inc’).addEventListener(‘click’, ()=>setFontSize(state.fontSize+1));
document.getElementById(‘fs-dec’).addEventListener(‘click’, ()=>setFontSize(state.fontSize-1));

// ============================================================
//  KEYBOARD SHORTCUTS
// ============================================================
document.addEventListener(‘keydown’, (e) => {
if (e.ctrlKey && e.key===‘s’) { e.preventDefault(); saveToBrowser(); }
if (e.ctrlKey && e.key===‘Enter’) { e.preventDefault(); runPreview(); }
if (e.ctrlKey && e.key===‘h’) { e.preventDefault(); toggleFindReplace(); }
if (e.key===‘Escape’) { document.getElementById(‘findreplace’).classList.remove(‘visible’); }
});

// ============================================================
//  INIT
// ============================================================
buildThemeList();
initDivider();

const loaded = loadFromBrowser();
if (!loaded) {
addFile(‘index.html’, DEFAULT_HTML);
addFile(‘style.css’, DEFAULT_CSS);
addFile(‘app.js’, DEFAULT_JS);
switchToFile(‘index.html’);
setTimeout(runPreview, 300);
} else {
setTimeout(runPreview, 300);
}

// Auto-save every 30s
setInterval(saveToBrowser, 30000);

notify(‘CodeForge ready! Ctrl+Enter to run ▶’,‘info’);
</script>

</body>
</html>