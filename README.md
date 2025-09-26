<!doctype html>
<html lang="pl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>Piłkarski Feed — Twoje pionowe wideo/tekst</title>
  <meta name="description" content="Pionowy feed o piłce nożnej — publikuj aktualności, zdjęcia, filmy, komentuj, lajkuj i udostępniaj." />
  <style>
    :root{
      --bg:#05060a; --card:#0d1117; --muted:#9aa5b1; --accent:#ffb020; --glass:rgba(255,255,255,0.03);
      --accent-2:#ff7a18; --success:#22c55e;
      color-scheme: dark; font-family: Inter, system-ui, -apple-system, Roboto, "Helvetica Neue", Arial;
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;background:linear-gradient(180deg,#021428,#031025);color:#e6eef6}
    /* App layout */
    .app{height:100vh;display:flex;flex-direction:column}
    header.appbar{height:64px;display:flex;align-items:center;padding:10px 16px;gap:12px;background:linear-gradient(90deg,rgba(255,255,255,0.02),transparent);border-bottom:1px solid rgba(255,255,255,0.03)}
    .brand{display:flex;align-items:center;gap:12px}
    .logo{width:44px;height:44px;border-radius:10px;background:linear-gradient(135deg,var(--accent),var(--accent-2));display:grid;place-items:center;font-weight:700;color:#08101a}
    .title{font-size:16px;font-weight:700}
    .subtitle{font-size:12px;color:var(--muted)}

    /* Main vertical feed area */
    main.feed{flex:1;overflow-y:auto;scroll-snap-type:y mandatory;-webkit-overflow-scrolling:touch}
    .post{min-height:calc(100vh - 64px); /* fill below header */scroll-snap-align:start;display:flex;flex-direction:column;justify-content:flex-end;padding:18px;position:relative}
    .post-inner{background:linear-gradient(180deg, rgba(0,0,0,0.15), rgba(0,0,0,0.35));border-radius:12px;padding:18px;max-width:820px;margin:0 auto;width:100%;box-shadow:0 10px 30px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.02)}

    /* Media area */
    .media{position:absolute;inset:64px 0 0 0;display:grid;place-items:center;overflow:hidden}
    .media img{max-width:100%;max-height:100%;object-fit:cover;width:100%}
    .media iframe, .media video{width:100%;height:100%;border:0}

    /* Overlay content */
    .overlay{position:relative;z-index:3}
    .post-info{display:flex;justify-content:space-between;align-items:flex-start;gap:12px}
    .meta{max-width:70%}
    .meta h3{margin:0 0 6px 0;font-size:18px}
    .meta p{margin:0;color:var(--muted)}

    .actions{display:flex;flex-direction:column;align-items:center;gap:12px}
    .action-btn{background:var(--glass);border-radius:12px;padding:8px;display:flex;flex-direction:column;align-items:center;gap:6px;width:62px}
    .action-btn button{background:none;border:0;color:var(--muted);cursor:pointer;font-size:14px}
    .count{font-weight:700}

    /* Composer floating */
    .composer-btn{position:fixed;right:18px;bottom:20px;background:linear-gradient(90deg,var(--accent),var(--accent-2));padding:12px 14px;border-radius:50px;color:#08101a;font-weight:800;box-shadow:0 8px 30px rgba(0,0,0,0.6);cursor:pointer;border:0}

    /* Modal */
    .modal{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:linear-gradient(rgba(0,0,0,0.6),rgba(0,0,0,0.6));z-index:40;padding:20px}
    .modal.open{display:flex}
    .modal-card{width:100%;max-width:760px;background:linear-gradient(180deg,#071827,#061420);padding:18px;border-radius:12px;border:1px solid rgba(255,255,255,0.03)}
    .field{display:flex;flex-direction:column;margin-bottom:12px}
    label{font-size:13px;color:var(--muted);margin-bottom:6px}
    input[type=text],textarea,select{background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.03);padding:10px;border-radius:8px;color:var(--text)}
    textarea{min-height:110px}
    .row{display:flex;gap:8px}
    .btn{padding:8px 12px;border-radius:8px;border:0;cursor:pointer}
    .btn.primary{background:linear-gradient(90deg,var(--accent),var(--accent-2));color:#08101a;font-weight:800}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.04);color:var(--muted)}

    /* Comments panel */
    .comments{position:fixed;right:18px;top:80px;width:320px;max-height:60vh;background:linear-gradient(180deg,#071827,#061420);border-radius:12px;padding:10px;border:1px solid rgba(255,255,255,0.03);overflow:auto}
    .comments h4{margin:6px 0}
    .comment{padding:8px;border-radius:8px;background:rgba(255,255,255,0.02);margin-bottom:8px}

    /* Controls bar */
    .controls{display:flex;gap:10px;align-items:center;margin-left:auto}
    .search{padding:8px;border-radius:8px;background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.03);color:var(--text)}

    /* small screens adjustments */
    @media(max-width:900px){
      .comments{position:static;width:100%;max-height:200px;margin-top:12px}
      .post-inner{border-radius:0;padding:14px}
      .actions{position:fixed;right:10px;bottom:90px;flex-direction:row;background:transparent}
    }

    /* Empty state */
    .empty{display:grid;place-items:center;height:calc(100vh - 64px);color:var(--muted)}

    /* Utility */
    .muted{color:var(--muted)}
    .chip{display:inline-block;padding:6px 10px;border-radius:999px;background:rgba(255,255,255,0.02);font-size:13px}
  </style>
</head>
<body>
  <div class="app">
    <header class="appbar">
      <div class="brand">
        <div class="logo">⚽</div>
        <div>
          <div class="title">Piłkarski Feed</div>
          <div class="subtitle">Pionowy feed do dzielenia się newsami i wideo</div>
        </div>
      </div>
      <div class="controls">
        <input id="search" class="search" placeholder="Szukaj (drużyna, słowo)..." />
        <button id="importBtn" class="btn ghost">Import</button>
        <button id="exportBtn" class="btn ghost">Eksport</button>
      </div>
    </header>

    <main id="feed" class="feed" tabindex="0">
      <!-- Posty będą tutaj renderowane -->
    </main>

    <!-- CTA: dodaj post -->
    <button id="openComposer" class="composer-btn">+ Dodaj post</button>

    <!-- modal composer -->
    <div id="modal" class="modal" aria-hidden="true">
      <div class="modal-card" role="dialog" aria-modal="true">
        <h3>Nowy post</h3>
        <div class="field">
          <label>Tytuł</label>
          <input id="postTitle" type="text" placeholder="Np. Wielkie zwycięstwo Klubu A" />
        </div>
        <div class="field">
          <label>Treść / opis</label>
          <textarea id="postText" placeholder="Napisz opis, wrażenia, analizę..."></textarea>
        </div>
        <div class="field">
          <label>Typ mediów</label>
          <select id="mediaType">
            <option value="none">Brak (tekst)</option>
            <option value="image">Obrazek (URL)</option>
            <option value="video">YouTube (wklej link)</option>
          </select>
        </div>
        <div class="field" id="mediaField" style="display:none">
          <label>Adres URL</label>
          <input id="mediaURL" type="text" placeholder="https://..." />
        </div>
        <div class="field">
          <label>Tagi (oddziel przecinkami)</label>
          <input id="tags" type="text" placeholder="np. liga,transfery,analiza" />
        </div>
        <div style="display:flex;gap:8px;justify-content:flex-end">
          <button id="closeModal" class="btn ghost">Anuluj</button>
          <button id="savePost" class="btn primary">Opublikuj</button>
        </div>
      </div>
    </div>

    <!-- Comments drawer (dynamic) -->
    <div id="comments" class="comments" style="display:none">
      <h4>Komentarze</h4>
      <div id="commentsList"></div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <input id="commentInput" placeholder="Dodaj komentarz..." style="flex:1;padding:8px;border-radius:8px;background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.03);color:var(--text)" />
        <button id="postComment" class="btn primary">Wyślij</button>
      </div>
    </div>

  </div>

  <template id="postTemplate">
    <article class="post">
      <div class="media"></div>
      <div class="post-inner overlay">
        <div class="post-info">
          <div class="meta">
            <h3 class="title">Tytuł</h3>
            <p class="desc muted">Opis...</p>
            <div style="margin-top:8px"><span class="chip tags muted">#tag</span></div>
            <div class="muted" style="margin-top:8px;font-size:12px">Opublikowano: <span class="time">—</span></div>
          </div>
          <div class="actions">
            <div class="action-btn like">
              <button class="likeBtn">❤</button>
              <div class="count likeCount">0</div>
            </div>
            <div class="action-btn commentToggle">
              <button class="commentBtn">💬</button>
              <div class="count commentCount">0</div>
            </div>
            <div class="action-btn shareBtnWrap">
              <button class="shareBtn">↗</button>
              <div class="muted" style="font-size:11px">Udost.</div>
            </div>
          </div>
        </div>
      </div>
    </article>
  </template>

  <script>
    // Prosty, rozbudowany klient feedu z localStorage
    const STORAGE_KEY = 'pilkarski_feed_v1';
    const feedEl = document.getElementById('feed');
    const modal = document.getElementById('modal');
    const openComposer = document.getElementById('openComposer');
    const closeModal = document.getElementById('closeModal');
    const savePost = document.getElementById('savePost');
    const mediaType = document.getElementById('mediaType');
    const mediaField = document.getElementById('mediaField');
    const mediaURL = document.getElementById('mediaURL');
    const postTitle = document.getElementById('postTitle');
    const postText = document.getElementById('postText');
    const tagsInput = document.getElementById('tags');
    const commentsPanel = document.getElementById('comments');
    const commentsList = document.getElementById('commentsList');
    const commentInput = document.getElementById('commentInput');
    const postComment = document.getElementById('postComment');
    const importBtn = document.getElementById('importBtn');
    const exportBtn = document.getElementById('exportBtn');
    const searchInput = document.getElementById('search');

    let posts = [];
    let currentCommentsFor = null;

    // helpers
    function uid(){return Date.now().toString(36) + Math.random().toString(36).slice(2,8)}
    function now(){return new Date().toISOString()}

    // load/save
    function save(){localStorage.setItem(STORAGE_KEY, JSON.stringify(posts))}
    function load(){const raw=localStorage.getItem(STORAGE_KEY);posts = raw ? JSON.parse(raw) : []}

    // render single post
    function renderPost(post){
      const tpl = document.getElementById('postTemplate');
      const node = tpl.content.firstElementChild.cloneNode(true);
      node.dataset.id = post.id;
      // media
      const mediaWrap = node.querySelector('.media');
      mediaWrap.innerHTML = '';
      if(post.mediaType === 'image' && post.mediaURL){
        const img = document.createElement('img'); img.src = post.mediaURL; img.alt = post.title || '';
        mediaWrap.appendChild(img);
      } else if(post.mediaType === 'video' && post.mediaURL){
        // embed youtube
        const url = post.mediaURL;
        const vid = extractYouTubeID(url);
        if(vid){
          const iframe = document.createElement('iframe');
          iframe.src = `https://www.youtube.com/embed/${vid}?rel=0&modestbranding=1&playsinline=1`;
          iframe.allow = 'accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture';
          mediaWrap.appendChild(iframe);
        } else {
          mediaWrap.textContent = 'Nieprawidłowy link wideo';
        }
      }

      // meta
      node.querySelector('.title').textContent = post.title || 'Bez tytułu';
      node.querySelector('.desc').textContent = post.text || '';
      node.querySelector('.time').textContent = (new Date(post.created)).toLocaleString();
      const tagsWrap = node.querySelector('.tags');
      tagsWrap.innerHTML = '';
      (post.tags||[]).slice(0,4).forEach(t=>{const s=document.createElement('span');s.className='chip';s.textContent='#'+t;tagsWrap.appendChild(s);tagsWrap.appendChild(document.createTextNode(' '))});

      // counts and buttons
      const likeCount = node.querySelector('.likeCount'); likeCount.textContent = post.likes||0;
      const commentCount = node.querySelector('.commentCount'); commentCount.textContent = (post.comments||[]).length;

      // like
      node.querySelector('.likeBtn').addEventListener('click',()=>{
        post.likes = (post.likes||0)+1; likeCount.textContent = post.likes; save();
      });

      // comments
      node.querySelector('.commentToggle').addEventListener('click',()=>{
        openComments(post.id);
      });

      // share
      node.querySelector('.shareBtn').addEventListener('click',async ()=>{
        const link = makeShareLink(post.id);
        try{
          if(navigator.share){
            await navigator.share({title:post.title,text:post.text,url:link});
          } else {
            await navigator.clipboard.writeText(link);
            alert('Link skopiowany do schowka');
          }
        }catch(e){alert('Udostępnianie nie powiodło się')}
      });

      // update comment count when comments change
      return node;
    }

    function renderFeed(filterText=''){
      feedEl.innerHTML = '';
      const list = posts.slice().reverse(); // newest first
      const filtered = list.filter(p=>{
        if(!filterText) return true;
        const t = filterText.toLowerCase();
        return (p.title||'').toLowerCase().includes(t) || (p.text||'').toLowerCase().includes(t) || (p.tags||[]).join(',').toLowerCase().includes(t);
      });
      if(filtered.length===0){
        const empty = document.createElement('div');empty.className='empty';empty.innerHTML='<div><h2>Brak postów</h2><p class="muted">Dodaj pierwszy post klikając przycisk "Dodaj post"</p></div>';
        feedEl.appendChild(empty);return;
      }
      filtered.forEach(p=>{feedEl.appendChild(renderPost(p))});
    }

    // compose
    openComposer.addEventListener('click',()=>{modal.classList.add('open');modal.setAttribute('aria-hidden','false')});
    closeModal.addEventListener('click',()=>{modal.classList.remove('open');modal.setAttribute('aria-hidden','true');clearComposer()});
    mediaType.addEventListener('change',()=>{mediaField.style.display = mediaType.value==='none' ? 'none' : 'block'});

    savePost.addEventListener('click',()=>{
      const title = postTitle.value.trim(); const text = postText.value.trim(); const type = mediaType.value; const url = mediaURL.value.trim();
      const tags = tagsInput.value.split(',').map(s=>s.trim()).filter(Boolean);
      if(!title && !text){alert('Dodaj tytuł lub treść');return}
      if(type!=='none' && !url){alert('Podaj adres URL mediów');return}
      const post = {id:uid(),title,text,mediaType:type,mediaURL:url,tags,created:now(),likes:0,comments:[]};
      posts.push(post); save(); renderFeed(searchInput.value);
      modal.classList.remove('open');modal.setAttribute('aria-hidden','true');clearComposer();
      // scroll to top (show newest)
      setTimeout(()=>{feedEl.scrollTo({top:0,behavior:'smooth'})},200);
    });

    function clearComposer(){postTitle.value='';postText.value='';mediaURL.value='';tagsInput.value='';mediaType.value='none';mediaField.style.display='none'}

    // comments
    function openComments(postId){
      const post = posts.find(p=>p.id===postId); if(!post) return;
      currentCommentsFor = postId; commentsPanel.style.display='block'; commentsList.innerHTML='';
      post.comments = post.comments||[];
      post.comments.forEach(c=>{const el=document.createElement('div');el.className='comment';el.innerHTML=`<strong>${escapeHtml(c.author)}</strong><div class="muted" style="font-size:12px">${new Date(c.created).toLocaleString()}</div><div style="margin-top:6px">${escapeHtml(c.text)}</div>`;commentsList.appendChild(el)});
      document.getElementById('commentInput').focus();
      updateCommentCounts();
    }

    postComment.addEventListener('click',()=>{
      const text = commentInput.value.trim(); if(!text || !currentCommentsFor) return; const post = posts.find(p=>p.id===currentCommentsFor);
      const comment = {id:uid(),author:'Anon',text,created:now()}; post.comments = post.comments||[]; post.comments.push(comment); save(); commentInput.value=''; openComments(currentCommentsFor); renderFeed(searchInput.value);
    });

    function updateCommentCounts(){
      document.querySelectorAll('.post').forEach(node=>{
        const id = node.dataset.id; const p = posts.find(x=>x.id===id); if(!p) return; const cc = (p.comments||[]).length; node.querySelector('.commentCount').textContent = cc;
      })
    }

    // export/import
    exportBtn.addEventListener('click',()=>{
      const blob = new Blob([JSON.stringify(posts,null,2)],{type:'application/json'});
      const url = URL.createObjectURL(blob); const a = document.createElement('a'); a.href=url; a.download='pilkarski_feed_export.json'; a.click(); URL.revokeObjectURL(url);
    });

    importBtn.addEventListener('click',()=>{
      const inp = document.createElement('input'); inp.type='file'; inp.accept='application/json'; inp.onchange = async (e)=>{
        const f = e.target.files[0]; if(!f) return; const text = await f.text(); try{ const data = JSON.parse(text); if(Array.isArray(data)) { posts = data; save(); renderFeed(); alert('Import zakończony'); } else alert('Plik nie ma poprawnej struktury'); }catch(err){alert('Błąd odczytu pliku')}
      }; inp.click();
    });

    // search
    searchInput.addEventListener('input',()=>renderFeed(searchInput.value));

    // share link factory (encode id in URL hash)
    function makeShareLink(postId){ const base = location.origin + location.pathname; return base + '#post=' + encodeURIComponent(postId); }

    // deep link handling
    function checkDeepLink(){ const h = location.hash; if(h && h.startsWith('#post=')){ const id = decodeURIComponent(h.split('=')[1]); // open the post by scrolling to it
      setTimeout(()=>{ const el = document.querySelector(`[data-id="${id}"]`); if(el){ el.scrollIntoView({behavior:'smooth'}); el.style.outline='3px solid rgba(255,187,50,0.4)'; setTimeout(()=>el.style.outline='none',2500); openComments(id); } },400);
    }}

    // utils
    function extractYouTubeID(url){ try{ const u=new URL(url); if(u.hostname.includes('youtube') || u.hostname.includes('youtu.be')){
        if(u.hostname==='youtu.be') return u.pathname.slice(1);
        return u.searchParams.get('v');
      } }catch(e){} return null }
    function escapeHtml(s){ return (s+'').replace(/[&<>"']/g, c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":"&#39;"})[c]) }

    // initial demo posts (only if storage empty)
    function seedIfEmpty(){ if(posts.length>0) return; posts = [
      {id:uid(),title:'Wielkie derby miasta',text:'Klub A pokonał Klub B 3:2 po emocjonującym spotkaniu. Bramki: 12', 55', 87'.','mediaType':'image','mediaURL':'https://images.unsplash.com/photo-1517927033932-9c2f0a8b8a4f?q=80&w=1600&auto=format&fit=crop&ixlib=rb-4.0.3&s=abcd','tags':['derby','liga'],'created:':now(),'created':now(),'likes':12,comments:[{id:uid(),author:'Kibic',text:'Co za mecz!',created:now()}]},
      {id:uid(),title:'Analiza taktyczna 4-3-3',text:'Krótka analiza ustawienia i pressingu — zobaczcie wideo.',mediaType:'video',mediaURL:'https://www.youtube.com/watch?v=dQw4w9WgXcQ',tags:['analiza','taktika'],created:now(),likes:3,comments:[]}
    ]; save(); }

    // initialisation
    load(); seedIfEmpty(); renderFeed(); checkDeepLink();

    // keyboard navigation (arrow keys)
    document.addEventListener('keydown',e=>{
      if(e.key==='ArrowDown' || e.key==='j'){ window.scrollBy({top:window.innerHeight-64,behavior:'smooth'}) }
      if(e.key==='ArrowUp' || e.key==='k'){ window.scrollBy({top:-(window.innerHeight-64),behavior:'smooth'}) }
      if(e.key==='Escape'){ modal.classList.remove('open'); modal.setAttribute('aria-hidden','true') }
    });

    // simple accessibility focus
    feedEl.addEventListener('focus',()=>feedEl.style.outline='none');

    // show current post from hash on load
    window.addEventListener('hashchange',checkDeepLink);

    // make sure comment panel updates comment counts
    window.addEventListener('storage',()=>{ load(); renderFeed(); });

    // touch: swipe hint for mobile — (no external libs)
    let touchStartY=0; feedEl.addEventListener('touchstart',e=>{ touchStartY = e.touches[0].clientY });
    feedEl.addEventListener('touchend',e=>{ const dy = e.changedTouches[0].clientY - touchStartY; if(dy < -60) window.scrollBy({top:window.innerHeight-120,behavior:'smooth'}); if(dy > 60) window.scrollBy({top:-window.innerHeight+120,behavior:'smooth'}); });

    // small helper: when posts update, refresh comments counts
    const obs = new MutationObserver(()=>updateCommentCounts()); obs.observe(feedEl,{childList:true,subtree:true});

    // expose helper for debugging (optional)
    window._PILKA = {posts, save, load, renderFeed};
  </script>
</body>
</html>



