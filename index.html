<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Simple To‑Do List</title>
  <style>
    :root{
      --bg:#0f1724; --card:#0b1220; --muted:#94a3b8; --accent:#60a5fa; --success:#34d399; --danger:#fb7185;
    }
    *{box-sizing:border-box}
    body{font-family:Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial; margin:0; min-height:100vh; display:flex; align-items:center; justify-content:center; background:linear-gradient(180deg,#081124 0%, #071426 100%); color:#e6eef8}
    .app{width:min(720px,94vw); padding:28px; background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius:14px; box-shadow:0 8px 30px rgba(2,6,23,0.6)}
    h1{margin:0 0 14px; font-size:20px; letter-spacing:0.3px}

    .top{display:flex; gap:12px; align-items:center}
    .input-wrap{flex:1; display:flex; gap:8px}
    input[type=text]{flex:1; padding:10px 12px; border-radius:10px; border:1px solid rgba(255,255,255,0.06); background:transparent; color:inherit; font-size:15px}
    button.btn{padding:10px 12px; border-radius:10px; border:none; background:var(--accent); color:#052038; font-weight:600; cursor:pointer}
    button.ghost{background:transparent; border:1px solid rgba(255,255,255,0.04); color:var(--muted)}

    .controls{display:flex; gap:8px; margin-top:14px; align-items:center; justify-content:space-between}
    .filters{display:flex; gap:8px}
    .filters button{padding:6px 10px; border-radius:8px; border:none; cursor:pointer; background:transparent; color:var(--muted)}
    .filters button.active{background:rgba(96,165,250,0.12); color:var(--accent)}

    ul.todos{list-style:none; margin:18px 0 8px; padding:0; display:flex; flex-direction:column; gap:8px}
    li.todo{display:flex; gap:12px; align-items:center; padding:10px; border-radius:10px; background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.005)); border:1px solid rgba(255,255,255,0.02)}
    .todo .label{flex:1; display:flex; gap:12px; align-items:center}
    .todo input[type=checkbox]{width:18px; height:18px; accent-color:var(--success)}
    .todo .text{font-size:15px}
    .todo.completed .text{opacity:0.6; text-decoration:line-through}
    .actions{display:flex; gap:6px}
    .small{padding:6px 8px; border-radius:8px; border:none; background:transparent; color:var(--muted); cursor:pointer}

    .meta{display:flex; gap:12px; align-items:center; color:var(--muted); font-size:13px}
    .empty{padding:18px; text-align:center; color:var(--muted); border-radius:10px; border:1px dashed rgba(255,255,255,0.03)}

    @media (max-width:420px){ .top{flex-direction:column; align-items:stretch} .controls{flex-direction:column; align-items:stretch} .filters{justify-content:center} }
  </style>
</head>
<body>
  <main class="app" id="app">
    <h1>To‑Do List</h1>

    <section class="top">
      <div class="input-wrap">
        <label for="new-task" class="sr-only">New task</label>
        <input id="new-task" type="text" placeholder="Add a task and press Enter" aria-label="New task" />
        <button id="addBtn" class="btn" aria-label="Add task">Add</button>
      </div>
      <button id="clearCompleted" class="ghost" title="Clear completed">Clear completed</button>
    </section>

    <section class="controls">
      <div class="filters" role="tablist" aria-label="Filter tasks">
        <button data-filter="all" class="active" role="tab">All</button>
        <button data-filter="active" role="tab">Active</button>
        <button data-filter="completed" role="tab">Completed</button>
      </div>
      <div class="meta"><span id="count">0</span> items</div>
    </section>

    <ul class="todos" id="todoList" aria-live="polite"></ul>

    <div id="empty" class="empty" hidden>You're all caught up — add a new task!</div>
  </main>

  <script>
    // Simple ToDo app with localStorage persistence
    const key = 'todo-list-v1';
    const el = {
      input: document.getElementById('new-task'),
      addBtn: document.getElementById('addBtn'),
      list: document.getElementById('todoList'),
      filters: document.querySelectorAll('.filters button'),
      count: document.getElementById('count'),
      clearCompleted: document.getElementById('clearCompleted'),
      empty: document.getElementById('empty')
    };

    let todos = load();
    let filter = 'all';

    function save(){ localStorage.setItem(key, JSON.stringify(todos)); }
    function load(){ try{ return JSON.parse(localStorage.getItem(key)) || []; }catch(e){return []} }

    function uid(){ return Date.now().toString(36) + Math.random().toString(36).slice(2,7); }

    function render(){
      el.list.innerHTML = '';
      const visible = todos.filter(t => (filter==='all') || (filter==='active' && !t.done) || (filter==='completed' && t.done));

      if(visible.length === 0){ el.empty.hidden = todos.length > 0; } else { el.empty.hidden = true; }

      visible.forEach(task => {
        const li = document.createElement('li');
        li.className = 'todo' + (task.done ? ' completed' : '');
        li.setAttribute('data-id', task.id);

        const label = document.createElement('div'); label.className = 'label';

        const cb = document.createElement('input'); cb.type = 'checkbox'; cb.checked = task.done; cb.setAttribute('aria-label', 'Mark task complete');
        cb.addEventListener('change', ()=>{ toggleDone(task.id); });

        const span = document.createElement('div'); span.className = 'text'; span.tabIndex = 0; span.textContent = task.text;
        span.addEventListener('dblclick', ()=>{ startEdit(span, task.id); });
        // allow Enter to start edit when focused
        span.addEventListener('keydown', (e)=>{ if(e.key === 'Enter'){ startEdit(span, task.id); } });

        label.appendChild(cb); label.appendChild(span);

        const actions = document.createElement('div'); actions.className='actions';
        const editBtn = document.createElement('button'); editBtn.className='small'; editBtn.innerText='Edit'; editBtn.addEventListener('click', ()=> startEdit(span, task.id));
        const delBtn = document.createElement('button'); delBtn.className='small'; delBtn.innerText='Delete'; delBtn.addEventListener('click', ()=> removeTask(task.id));

        actions.appendChild(editBtn); actions.appendChild(delBtn);

        li.appendChild(label); li.appendChild(actions);
        el.list.appendChild(li);
      });

      el.count.textContent = todos.filter(t => !t.done).length;
    }

    function addTask(text){
      const trimmed = text.trim();
      if(!trimmed) return;
      todos.unshift({ id: uid(), text: trimmed, done: false });
      save(); render();
    }

    function removeTask(id){ todos = todos.filter(t=>t.id !== id); save(); render(); }
    function toggleDone(id){ todos = todos.map(t => t.id===id ? {...t, done: !t.done} : t); save(); render(); }

    function startEdit(spanEl, id){
      const old = spanEl.textContent;
      const input = document.createElement('input'); input.type='text'; input.value = old; input.style.width='100%'; input.setAttribute('aria-label','Edit task');
      spanEl.replaceWith(input); input.focus();
      // commit
      function commit(){
        const v = input.value.trim();
        if(v){ todos = todos.map(t => t.id===id ? {...t, text: v} : t); }
        save(); render();
      }
      function cancel(){ render(); }

      input.addEventListener('keydown', (e)=>{ if(e.key==='Enter'){ commit(); } else if(e.key==='Escape'){ cancel(); } });
      input.addEventListener('blur', ()=>{ commit(); });
    }

    // filter handling
    el.filters.forEach(btn => btn.addEventListener('click', ()=>{
      el.filters.forEach(b=>b.classList.remove('active'));
      btn.classList.add('active'); filter = btn.dataset.filter; render();
    }));

    // add handlers
    el.addBtn.addEventListener('click', ()=>{ addTask(el.input.value); el.input.value=''; el.input.focus(); });
    el.input.addEventListener('keydown', (e)=>{ if(e.key === 'Enter'){ addTask(el.input.value); el.input.value=''; } });

    el.clearCompleted.addEventListener('click', ()=>{
      todos = todos.filter(t => !t.done); save(); render();
    });

    // initial render
    render();

    // expose for debug (optional)
    window._todos = todos;
  </script>
</body>
</html>
