/* ── Reset & Base ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --blue: #185FA5; --blue-light: #E6F1FB; --blue-dark: #0C447C;
  --green: #3B6D11; --green-light: #EAF3DE;
  --amber: #854F0B; --amber-light: #FAEEDA;
  --red: #A32D2D; --red-light: #FCEBEB;
  --gray: #5F5E5A; --gray-light: #F1EFE8; --gray-mid: #B4B2A9;
  --purple: #534AB7; --purple-light: #EEEDFE;
  --teal: #0F6E56; --teal-light: #E1F5EE;
  --text: #2C2C2A; --text-2: #5F5E5A; --text-3: #888780;
  --bg: #ffffff; --bg-2: #F8F7F4; --bg-3: #F1EFE8;
  --border: rgba(44,44,42,0.12); --border-2: rgba(44,44,42,0.22);
  --radius: 8px; --radius-lg: 12px; --radius-xl: 16px;
  --shadow: 0 1px 3px rgba(0,0,0,0.08);
  --font: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, sans-serif;
  --safe-bottom: env(safe-area-inset-bottom, 0px);
}
@media (prefers-color-scheme: dark) {
  :root {
    --blue: #85B7EB; --blue-light: #0C447C; --blue-dark: #B5D4F4;
    --green: #97C459; --green-light: #27500A;
    --amber: #EF9F27; --amber-light: #633806;
    --red: #F09595; --red-light: #791F1F;
    --gray: #B4B2A9; --gray-light: #444441; --gray-mid: #5F5E5A;
    --purple: #AFA9EC; --purple-light: #3C3489;
    --teal: #5DCAA5; --teal-light: #085041;
    --text: #E8E6DF; --text-2: #B4B2A9; --text-3: #888780;
    --bg: #1C1C1A; --bg-2: #242422; --bg-3: #2C2C2A;
    --border: rgba(255,255,255,0.1); --border-2: rgba(255,255,255,0.2);
  }
}
html { font-size: 16px; -webkit-text-size-adjust: 100%; }
body { font-family: var(--font); color: var(--text); background: var(--bg-2); min-height: 100vh; }

/* ── Layout ── */
#app { display: flex; flex-direction: column; min-height: 100vh; }
.topbar {
  background: var(--bg); border-bottom: 0.5px solid var(--border);
  padding: 0 16px; height: 56px; display: flex; align-items: center;
  justify-content: space-between; position: sticky; top: 0; z-index: 100;
}
.topbar-logo { font-size: 17px; font-weight: 600; color: var(--blue); letter-spacing: -0.3px; }
.topbar-actions { display: flex; align-items: center; gap: 8px; }

.sidebar {
  width: 220px; background: var(--bg); border-right: 0.5px solid var(--border);
  padding: 12px 0; position: fixed; top: 56px; left: 0; bottom: 0;
  overflow-y: auto; z-index: 90; transition: transform 0.25s ease;
}
.sidebar.hidden { transform: translateX(-100%); }
.sidebar-section { padding: 4px 12px 4px; }
.sidebar-label { font-size: 11px; font-weight: 500; color: var(--text-3); text-transform: uppercase; letter-spacing: 0.5px; padding: 8px 4px 4px; }
.sidebar-item {
  display: flex; align-items: center; gap: 8px; padding: 8px 10px;
  border-radius: var(--radius); cursor: pointer; font-size: 14px; color: var(--text-2);
  transition: background 0.15s; text-decoration: none;
}
.sidebar-item:hover { background: var(--bg-3); }
.sidebar-item.active { background: var(--blue-light); color: var(--blue); font-weight: 500; }
.sidebar-dot { width: 8px; height: 8px; border-radius: 50%; background: currentColor; opacity: 0.6; flex-shrink: 0; }

.main {
  margin-left: 220px; padding: 20px; flex: 1;
  transition: margin-left 0.25s ease;
}
.main.full { margin-left: 0; }

@media (max-width: 768px) {
  .sidebar { transform: translateX(-100%); }
  .sidebar.open { transform: translateX(0); box-shadow: 4px 0 16px rgba(0,0,0,0.15); }
  .main { margin-left: 0; padding: 12px; }
  .overlay { display: block; }
}
.overlay {
  display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.4);
  z-index: 80; opacity: 0; transition: opacity 0.25s;
}
.overlay.show { opacity: 1; }

/* ── Cards & Panels ── */
.card {
  background: var(--bg); border: 0.5px solid var(--border);
  border-radius: var(--radius-lg); padding: 16px 20px; margin-bottom: 14px;
}
.card-title {
  font-size: 13px; font-weight: 500; color: var(--text-2);
  padding-bottom: 10px; margin-bottom: 14px;
  border-bottom: 0.5px solid var(--border);
}
.stat-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(120px, 1fr)); gap: 10px; margin-bottom: 16px; }
.stat-card { background: var(--bg-2); border-radius: var(--radius); padding: 12px 14px; }
.stat-label { font-size: 12px; color: var(--text-3); margin-bottom: 4px; }
.stat-value { font-size: 22px; font-weight: 600; color: var(--text); }

/* ── Buttons ── */
.btn {
  display: inline-flex; align-items: center; gap: 6px;
  padding: 7px 14px; border-radius: var(--radius); font-size: 13px; font-weight: 500;
  border: 0.5px solid var(--border-2); background: var(--bg); color: var(--text);
  cursor: pointer; transition: background 0.15s, transform 0.1s; white-space: nowrap;
  font-family: var(--font);
}
.btn:hover { background: var(--bg-3); }
.btn:active { transform: scale(0.98); }
.btn-primary { background: var(--blue); color: #fff; border-color: var(--blue); }
.btn-primary:hover { background: var(--blue-dark); }
.btn-danger { background: var(--red-light); color: var(--red); border-color: var(--red-light); }
.btn-sm { padding: 4px 10px; font-size: 12px; }
.btn-icon { padding: 7px; }

/* ── Forms & Inputs ── */
.form-grid { display: grid; grid-template-columns: 130px 1fr; gap: 10px 14px; align-items: start; }
@media (max-width: 480px) { .form-grid { grid-template-columns: 1fr; } .form-grid .flabel { margin-bottom: -6px; } }
.flabel { font-size: 13px; color: var(--text-2); padding-top: 8px; }
.flabel.required::after { content: ' *'; color: var(--red); }
input[type=text], input[type=email], input[type=number], input[type=date],
input[type=tel], select, textarea {
  width: 100%; padding: 8px 10px; font-size: 14px; font-family: var(--font);
  border: 0.5px solid var(--border-2); border-radius: var(--radius);
  background: var(--bg); color: var(--text);
  transition: border-color 0.15s, box-shadow 0.15s;
}
input:focus, select:focus, textarea:focus {
  outline: none; border-color: var(--blue); box-shadow: 0 0 0 3px rgba(24,95,165,0.12);
}
textarea { resize: vertical; min-height: 72px; line-height: 1.5; }
.input-hint { font-size: 12px; color: var(--text-3); margin-top: 4px; }

/* ── Table ── */
.table-wrap { overflow-x: auto; border-radius: var(--radius-lg); border: 0.5px solid var(--border); }
table { width: 100%; border-collapse: collapse; background: var(--bg); }
th {
  text-align: left; padding: 9px 12px; font-size: 12px; font-weight: 500;
  color: var(--text-3); background: var(--bg-2); border-bottom: 0.5px solid var(--border);
  white-space: nowrap;
}
td { padding: 10px 12px; border-bottom: 0.5px solid var(--border); font-size: 13px; color: var(--text); }
tr:last-child td { border-bottom: none; }
tr:hover td { background: var(--bg-2); cursor: pointer; }
.td-mono { font-family: monospace; font-size: 12px; color: var(--blue); font-weight: 500; }

/* ── Badges ── */
.badge {
  display: inline-block; padding: 2px 9px; border-radius: 99px;
  font-size: 11px; font-weight: 500; white-space: nowrap;
}
.badge-draft    { background: var(--gray-light);   color: var(--gray); }
.badge-pending  { background: var(--amber-light);  color: var(--amber); }
.badge-approved { background: var(--green-light);  color: var(--green); }
.badge-rejected { background: var(--red-light);    color: var(--red); }
.badge-blue     { background: var(--blue-light);   color: var(--blue-dark); }
.badge-purple   { background: var(--purple-light); color: var(--purple); }

/* ── Toolbar ── */
.toolbar {
  display: flex; align-items: center; gap: 8px; flex-wrap: wrap;
  padding: 10px 0; margin-bottom: 12px;
}
.toolbar-spacer { flex: 1; }
.search-box { position: relative; }
.search-box input { padding-left: 30px; width: 200px; }
.search-icon { position: absolute; left: 8px; top: 50%; transform: translateY(-50%); color: var(--text-3); font-size: 14px; }

/* ── Sequence Badge ── */
.seq-badge {
  display: inline-block; padding: 4px 12px; background: var(--blue-light);
  color: var(--blue); border-radius: var(--radius); font-weight: 600;
  font-size: 14px; font-family: monospace; letter-spacing: 0.5px;
}

/* ── Subtable ── */
.subtable { width: 100%; border-collapse: collapse; font-size: 13px; margin-top: 8px; }
.subtable th { padding: 7px 8px; font-size: 12px; background: var(--bg-2); }
.subtable td { padding: 6px 8px; border-bottom: 0.5px solid var(--border); }
.subtable td input, .subtable td select { padding: 5px 7px; font-size: 12px; width: 100%; }
.subtable tfoot td { background: var(--bg-2); font-weight: 600; padding: 8px; }
.subtable .del-btn { width: 28px; padding: 4px; text-align: center; }

/* ── Revision History ── */
.rev-item { padding: 12px 0; border-bottom: 0.5px solid var(--border); }
.rev-item:last-child { border-bottom: none; }
.rev-meta { display: flex; align-items: center; gap: 8px; margin-bottom: 6px; flex-wrap: wrap; }
.rev-ver { font-size: 12px; font-weight: 500; padding: 2px 8px; background: var(--blue-light); color: var(--blue); border-radius: 99px; }
.rev-who { font-size: 12px; color: var(--text-3); }
.rev-changes { background: var(--bg-2); border-radius: var(--radius); padding: 8px 12px; }
.rev-change { font-size: 12px; margin-bottom: 4px; }
.rev-field { font-weight: 500; }
.rev-old { color: var(--red); text-decoration: line-through; }
.rev-new { color: var(--green); }
.rev-reason { font-size: 12px; color: var(--text-3); margin-top: 6px; font-style: italic; }

/* ── Approval Steps ── */
.approval-steps { display: flex; flex-direction: column; gap: 0; }
.approval-step { display: flex; align-items: flex-start; gap: 12px; padding: 12px 0; position: relative; }
.approval-step:not(:last-child)::before {
  content: ''; position: absolute; left: 15px; top: 40px; bottom: -12px;
  width: 1px; background: var(--border-2);
}
.step-circle {
  width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center;
  justify-content: center; font-size: 13px; font-weight: 600; flex-shrink: 0;
  border: 1.5px solid var(--border-2); background: var(--bg-2); color: var(--text-3);
}
.step-circle.done { background: var(--green-light); color: var(--green); border-color: var(--green); }
.step-circle.active { background: var(--amber-light); color: var(--amber); border-color: var(--amber); }
.step-circle.rejected { background: var(--red-light); color: var(--red); border-color: var(--red); }
.step-info { flex: 1; padding-top: 4px; }
.step-name { font-size: 14px; font-weight: 500; }
.step-meta { font-size: 12px; color: var(--text-3); margin-top: 2px; }
.step-comment { font-size: 12px; color: var(--text-2); background: var(--bg-2); border-radius: var(--radius); padding: 6px 10px; margin-top: 6px; }

/* ── Field Builder ── */
.field-list { display: flex; flex-direction: column; gap: 8px; }
.field-item {
  display: grid; grid-template-columns: 1fr 1fr auto auto;
  gap: 8px; align-items: center;
  background: var(--bg-2); border-radius: var(--radius); padding: 10px 12px;
  border: 0.5px solid var(--border);
}
@media (max-width: 480px) { .field-item { grid-template-columns: 1fr 1fr auto; } }
.field-item input, .field-item select { margin: 0; font-size: 13px; }

/* ── Modal ── */
.modal-overlay {
  position: fixed; inset: 0; background: rgba(0,0,0,0.4);
  z-index: 200; display: flex; align-items: center; justify-content: center;
  padding: 16px;
}
.modal {
  background: var(--bg); border-radius: var(--radius-xl);
  border: 0.5px solid var(--border); padding: 20px;
  width: 100%; max-width: 480px; max-height: 90vh; overflow-y: auto;
}
.modal h3 { font-size: 16px; font-weight: 600; margin-bottom: 16px; }
.modal-footer { display: flex; justify-content: flex-end; gap: 8px; margin-top: 16px; padding-top: 12px; border-top: 0.5px solid var(--border); }

/* ── Page Header ── */
.page-header { display: flex; align-items: center; gap: 12px; margin-bottom: 20px; }
.page-title { font-size: 20px; font-weight: 600; }
.page-back { color: var(--text-3); cursor: pointer; font-size: 14px; display: flex; align-items: center; gap: 4px; }
.page-back:hover { color: var(--blue); }

/* ── Mobile Nav Bottom ── */
.mobile-nav {
  display: none; position: fixed; bottom: 0; left: 0; right: 0;
  background: var(--bg); border-top: 0.5px solid var(--border);
  padding: 8px 0 calc(8px + var(--safe-bottom)); z-index: 100;
  flex-direction: row;
}
.mobile-nav-item {
  flex: 1; display: flex; flex-direction: column; align-items: center; gap: 3px;
  font-size: 10px; color: var(--text-3); cursor: pointer; padding: 4px 0;
}
.mobile-nav-item.active { color: var(--blue); }
.mobile-nav-icon { font-size: 20px; line-height: 1; }
@media (max-width: 768px) {
  .mobile-nav { display: flex; }
  .main { padding-bottom: calc(80px + var(--safe-bottom)); }
}

/* ── PWA install banner ── */
.pwa-banner {
  background: var(--blue-light); border: 0.5px solid var(--blue);
  border-radius: var(--radius-lg); padding: 12px 16px; margin-bottom: 16px;
  display: flex; align-items: center; gap: 12px; font-size: 13px; color: var(--blue-dark);
}
.pwa-banner-close { margin-left: auto; cursor: pointer; opacity: 0.6; }

/* ── Toast ── */
.toast {
  position: fixed; bottom: calc(80px + var(--safe-bottom) + 8px); left: 50%;
  transform: translateX(-50%) translateY(20px);
  background: var(--text); color: var(--bg); padding: 10px 18px;
  border-radius: 99px; font-size: 13px; z-index: 500; opacity: 0;
  transition: opacity 0.2s, transform 0.2s; white-space: nowrap;
  pointer-events: none;
}
.toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }
@media (min-width: 769px) { .toast { bottom: 24px; } }

/* ── Misc ── */
.empty-state { text-align: center; padding: 48px 16px; color: var(--text-3); font-size: 14px; }
.empty-icon { font-size: 40px; margin-bottom: 12px; opacity: 0.4; }
.divider { border: none; border-top: 0.5px solid var(--border); margin: 14px 0; }
.text-sm { font-size: 13px; }
.text-xs { font-size: 12px; }
.text-muted { color: var(--text-3); }
.mt-1 { margin-top: 8px; } .mt-2 { margin-top: 14px; } .mt-3 { margin-top: 20px; }
.mb-1 { margin-bottom: 8px; } .mb-2 { margin-bottom: 14px; }
.flex { display: flex; } .items-center { align-items: center; } .gap-2 { gap: 8px; }
.w-full { width: 100%; }
