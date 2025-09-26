# Pi-karskieInfo
Nowe informacje o piłce nożnej znajdziesz na naszej stronie.
<!doctype html>
<html lang="pl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Piłka Nożna — Strona Informacyjna</title>
  <meta name="description" content="Prosta, czytelna strona o piłce nożnej — wiadomości, drużyny, terminarz i zasady. Gotowa do wysłania znajomemu." />

  <!-- Prosty, czysty styl -->
  <style>
    :root{
      --bg:#0f1724; /* ciemne tło inspirowane technicznymi sklepami */
      --card:#0b1220;
      --accent:#ffb020;
      --muted:#94a3b8;
      --text:#e6eef6;
      --glass: rgba(255,255,255,0.03);
      font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      background:linear-gradient(180deg,var(--bg), #08101a);
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      line-height:1.45;
    }
    .container{max-width:1000px;margin:28px auto;padding:20px;}
    header{
      display:flex;gap:16px;align-items:center;
      margin-bottom:20px;
    }
    .logo{
      width:64px;height:64px;border-radius:12px;
      background:linear-gradient(135deg,var(--accent),#ff7a18);
      display:flex;align-items:center;justify-content:center;
      box-shadow: 0 6px 18px rgba(0,0,0,0.6);
      flex-shrink:0;
    }
    .logo svg{filter:drop-shadow(0 2px 6px rgba(0,0,0,0.5));}
    h1{font-size:20px;margin:0}
    p.lead{color:var(--muted);margin:2px 0 0;font-size:13px}

    nav.top{
      display:flex;gap:10px;margin-top:12px;flex-wrap:wrap;
    }
    nav.top a{
      background:var(--glass);padding:8px 12px;border-radius:10px;color:var(--text);
      text-decoration:none;font-size:13px;border:1px solid rgba(255,255,255,0.03);
    }

    main{display:grid;grid-template-columns:1fr 340px;gap:18px;margin-top:18px;}
    @media (max-width:900px){ main{grid-template-columns:1fr;} .container{padding:14px;} }

    /* karty */
    .card{background:linear-gradient(180deg,var(--card), rgba(255,255,255,0.01)); padding:14px;border-radius:12px;
      box-shadow: 0 6px 16px rgba(2,6,23,0.6); border:1px solid rgba(255,255,255,0.02);}
    .section-title{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}
    .section-title h2{font-size:16px;margin:0}
    .muted{color:var(--muted);font-size:13px}

    /* news list */
    .news-item{padding:10px 0;border-bottom:1px dashed rgba(255,255,255,0.02)}
    .news-item:last-child{border-bottom:0}
    .news-item h3{margin:0;font-size:15px}
    .news-meta{font-size:12px;color:var(--muted);margin-top:6px}

    /* teams */
    .team-list{display:grid;grid-template-columns:1fr 1fr;gap:8px}
    .team{padding:8px;border-radius:8px;background:rgba(255,255,255,0.01);display:flex;align-items:center;gap:10px}
    .crest{width:38px;height:38px;border-radius:8px;background:linear-gradient(135deg,#fff1,#fff2);display:flex;align-items:center;justify-content:center;font-weight:700;color:#0b1220}

    /* fixtures */
    .fixture{display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid rgba(255,255,255,0.02)}
    .fixture:last-child{border-bottom:0}
    .score{font-weight:700}

    footer{margin-top:22px;color:var(--muted);font-size:13px;text-align:center}

    /* print */
    @media print{
      body{background:white;color:black}
      .logo{display:none}
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="logo" aria-hidden="true">
        <!-- prosty piłkarski symbol w SVG -->
        <svg width="36" height="36" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="12" cy="12" r="10" fill="white" />
          <path d="M12 4.5L14.1 8.6L18.5 9.6L15.2 12.5L16 16.9L12 14.6L8 16.9L8.8 12.5L5.5 9.6L9.9 8.6L12 4.5Z" fill="#0b1220" />
        </svg>
      </div>
      <div>
        <h1>Wiadomości i informator: Piłka Nożna</h1>
        <p class="lead">Szybka, czytelna strona z najważniejszymi informacjami o piłce nożnej — gotowa do wysłania znajomemu.</p>
        <nav class="top" aria-label="Nawigacja">
          <a href="#news">Wiadomości</a>
          <a href="#teams">Drużyny</a>
          <a href="#fixtures">Terminarz</a>
          <a href="#rules">Zasady</a>
          <a href="#about">O stronie</a>
        </nav>
      </div>
    </header>

    <main>
      <!-- GŁÓWNA KOLUMNA -->
      <section>
        <article id="news" class="card" aria-labelledby="news-title">
          <div class="section-title">
            <h2 id="news-title">Najnowsze wiadomości</h2>
            <div class="muted">Aktualne (statyczne przykłady)</div>
          </div>

          <div class="news-item">
            <h3>Wielki mecz: Klub A — Klub B 2:1</h3>
            <div class="news-meta">28 wrz 2025 — Bramki: 45' i 78' — Krótki opis wydarzeń, kluczowe momenty i statystyki.</div>
            <p class="muted" style="margin-top:8px">Komentarz: Mecz obfitował w akcje, znakomite interwencje bramkarzy i kontrowersyjne decyzje sędziowskie.</p>
          </div>

          <div class="news-item">
            <h3>Transfer: Zawodnik X przenosi się do Klubu C</h3>
            <div class="news-meta">27 wrz 2025 — Testy medyczne i 4-letni kontrakt.</div>
            <p class="muted" style="margin-top:8px">Komentarz: Transfer oznacza wzmocnienie linii ataku Klubu C.</p>
          </div>

          <div class="news-item">
            <h3>Nowa taktyka trenera Y daje efekty</h3>
            <div class="news-meta">25 wrz 2025 — Analiza taktyczna i przykłady ustawienia 4-2-3-1.</div>
            <p class="muted" style="margin-top:8px">Szybkie podsumowanie: większe naciskanie w środku pola, zmiana pozycji skrzydłowego.</p>
          </div>

        </article>

        <article id="teams" class="card" style="margin-top:16px;">
          <div class="section-title">
            <h2>Drużyny (przykłady)</h2>
            <div class="muted">Kliknij nazwę, by przeczytać opis</div>
          </div>

          <div class="team-list">
            <div class="team">
              <div class="crest">A</div>
              <div>
                <strong>Klub A</strong><div class="muted" style="font-size:12px">Miasto — Stadion A — Trener: Kowalski</div>
              </div>
            </div>

            <div class="team">
              <div class="crest">B</div>
              <div>
                <strong>Klub B</strong><div class="muted" style="font-size:12px">Miasto — Stadion B — Trener: Nowak</div>
              </div>
            </div>

            <div class="team">
              <div class="crest">C</div>
              <div>
                <strong>Klub C</strong><div class="muted" style="font-size:12px">Miasto — Stadion C — Trener: Wiśniewski</div>
              </div>
            </div>

            <div class="team">
              <div class="crest">D</div>
              <div>
                <strong>Klub D</strong><div class="muted" style="font-size:12px">Miasto — Stadion D — Trener: Zieliński</div>
              </div>
            </div>
          </div>
        </article>

        <article id="fixtures" class="card" style="margin-top:16px;">
          <div class="section-title">
            <h2>Najbliższe spotkania</h2>
            <div class="muted">Data i godzina (lokalna)</div>
          </div>

          <div class="fixture">
            <div>
              <div><strong>Klub A</strong> vs <strong>Klub B</strong></div>
              <div class="muted" style="font-size:13px">30 wrz 2025 • 20:45 • Stadion A</div>
            </div>
            <div class="score muted">—</div>
          </div>

          <div class="fixture">
            <div>
              <div><strong>Klub C</strong> vs <strong>Klub D</strong></div>
              <div class="muted" style="font-size:13px">03 paź 2025 • 18:00 • Stadion C</div>
            </div>
            <div class="score muted">—</div>
          </div>

          <p class="muted" style="margin-top:10px">Uwaga: To przykładowy terminarz — możesz edytować daty i godziny w pliku HTML.</p>
        </article>

        <article id="rules" class="card" style="margin-top:16px;">
          <div class="section-title">
            <h2>Podstawowe zasady piłki nożnej</h2>
            <div class="muted">Krótki przewodnik</div>
          </div>

          <ul style="margin:0;padding-left:18px;color:var(--muted)">
            <li>Mecz trwa 90 minut — dwie połowy po 45 minut + doliczony czas.</li>
            <li>11 zawodników w każdej drużynie (w tym bramkarz).</li>
            <li>Rzut karny przy faulu w polu karnym; rzuty wolne — w zależności od przewinienia.</li>
            <li>Spalone: zawodnik w pozycji spalonej może być ukarany, jeśli bierze udział w akcji.</li>
          </ul>
          <p class="muted" style="margin-top:8px">To tylko szybkie przypomnienie — szczegółowe przepisy są opisane w Przepisach Gry FIFA.</p>
        </article>

      </section>

      <!-- PRAWY PANEL -->
      <aside>
        <div class="card" id="about">
          <div class="section-title"><h2>O tej stronie</h2><div class="muted">Wersja offline</div></div>
          <p class="muted">Ta strona to pojedynczy plik HTML. Możesz edytować tekst (wiadomości, terminarz, drużyny) w zwykłym edytorze tekstu. Wszystko działa offline — wystarczy otworzyć plik w przeglądarce.</p>

          <hr style="border:none;border-top:1px solid rgba(255,255,255,0.03);margin:12px 0">

          <div style="display:flex;gap:8px;flex-direction:column">
            <button onclick="window.print()" style="padding:8px;border-radius:8px;border:0;background:linear-gradient(90deg,var(--accent),#ff7a18);color:#08101a;font-weight:700;cursor:pointer">Drukuj / Zapisz jako PDF</button>
            <a href="#" onclick="downloadHTML()" style="text-decoration:none;padding:8px;border-radius:8px;background:rgba(255,255,255,0.02);display:inline-block;color:var(--text);text-align:center">Pobierz plik HTML</a>
          </div>

          <script>
            function downloadHTML(){
              const blob = new Blob([document.documentElement.outerHTML], {type: 'text/html;charset=utf-8'});
              const url = URL.createObjectURL(blob);
              const a = document.createElement('a');
              a.href = url;
              a.download = 'pilka.html';
              a.click();
              URL.revokeObjectURL(url);
            }
          </script>
        </div>

        <div class="card" style="margin-top:16px">
          <div class="section-title"><h2>Przydatne wskazówki</h2><div class="muted">Jak edytować i wysłać</div></div>
          <ol style="color:var(--muted);padding-left:18px">
            <li>Otwórz plik w edytorze (Notepad / TextEdit / VSCode).</li>
            <li>Znajdź sekcję <code>&lt;article id="news"&gt;</code> i edytuj wiadomości.</li>
            <li>Zapisz plik i otwórz w przeglądarce — zmiany od razu widoczne.</li>
            <li>Wyślij plik jako załącznik w e-mailu lub udostępnij link z Google Drive.</li>
          </ol>
        </div>

        <div class="card" style="margin-top:16px">
          <div class="section-title"><h2>Kontakt</h2><div class="muted">Masz pomysł na zmianę?</div></div>
          <p class="muted">Jeśli chcesz, mogę: dodać - aktualne wyniki pobierane z internetu, - podświetlanie najważniejszych wiadomości, - sekcję statystyk (strzelcy, asysty).</p>
        </div>
      </aside>
    </main>

    <footer>
      &copy; <span id="curYear"></span> Strona przykładowa — do użytku osobistego. Plik: pilka.html
    </footer>
  </div>

  <script>
    // ustaw aktualny rok
    document.getElementById('curYear').textContent = new Date().getFullYear();
  </script>
</body>
</html>

