<!doctype html>
<html lang="de">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Startup Landingpage</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#7c3aed;--muted:#9ca3af;--glass:rgba(255,255,255,0.03)}
    *{box-sizing:border-box;font-family:Inter,system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial}
    body{margin:0;background:linear-gradient(180deg,#071026 0%, #071226 100%);color:#e6eef8;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:36px}
    .container{max-width:1100px;width:100%;display:grid;grid-template-columns:1fr 420px;gap:32px;align-items:center}
    .hero{padding:48px;background:linear-gradient(180deg, rgba(255,255,255,0.02), transparent);border-radius:16px;box-shadow:0 10px 30px rgba(2,6,23,0.6)}
    h1{font-size:36px;margin:0 0 12px 0;line-height:1.03}
    p.lead{color:var(--muted);margin:0 0 20px 0}
    .cta-row{display:flex;gap:12px;align-items:center}
    .btn{appearance:none;border:0;padding:12px 18px;border-radius:12px;font-weight:600;cursor:pointer}
    .btn-primary{background:linear-gradient(90deg,var(--accent),#5b21b6);color:white;box-shadow:0 8px 24px rgba(124,58,237,0.18)}
    .btn-ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--muted)}
    .card{background:var(--card);padding:20px;border-radius:14px;box-shadow:0 6px 16px rgba(2,6,23,0.5)}

    /* modal */
    .modal-backdrop{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:linear-gradient(180deg,rgba(2,6,23,0.6),rgba(2,6,23,0.85));z-index:60}
    .modal{width:92%;max-width:520px;background:linear-gradient(180deg,#061026,#08142a);border-radius:12px;padding:22px;border:1px solid rgba(255,255,255,0.03);box-shadow:0 20px 60px rgba(2,6,23,0.7)}
    .modal h3{margin:0 0 6px 0}
    .modal p{color:var(--muted);margin:0 0 10px 0}
    .form-row{display:flex;flex-direction:column;gap:8px;margin-top:8px}
    label{font-size:13px;color:var(--muted)}
    input[type="text"],input[type="email"]{padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:var(--glass);color:inherit}
    .modal-footer{display:flex;gap:8px;justify-content:flex-end;margin-top:12px}

    footer.small{color:var(--muted);font-size:13px;margin-top:14px}

    @media (max-width:920px){.container{grid-template-columns:1fr;}
      .hero{order:2}
    }
  </style>
</head>
<body>
  <main class="container">
    <section class="hero card">
      <p style="color:var(--muted);font-size:13px;margin:0 0 10px 0">Beta • Startup</p>
      <h1>Einfach. Schnell. Deine Lösung für [Produktname]</h1>
      <p class="lead">Kurzbeschreibung deines Produkts — was es tut und für wen es gedacht ist. Schlagkräftig, knapp und auf Deutsch.</p>
      <div class="cta-row">
        <button id="orderBtn" class="btn btn-primary">Order now</button>
        <a class="btn btn-ghost" href="#" onclick="document.getElementById('newsletterEmail').focus();return false;">Newsletter abonnieren</a>
      </div>
      <p class="small" style="margin-top:14px;color:var(--muted)">Kostenlos testen — keine Kreditkarte erforderlich. Datenschutz: wir geben deine E-Mail nicht weiter.</p>
    </section>

    <aside class="card">
      <h2 style="margin:0 0 8px 0">Warum unser Produkt?</h2>
      <ul style="margin:0 0 12px 18px;color:var(--muted)">
        <li>Schnell einzurichten</li>
        <li>Skaliert mit deinem Bedarf</li>
        <li>Datenschutz &amp; Sicherheit</li>
      </ul>
      <div style="margin-top:8px">
        <strong>Newsletter</strong>
        <p style="margin:6px 0 10px 0;color:var(--muted)">Trage deine E-Mail ein und erhalte Updates, sobald das Produkt verfügbar ist.</p>
        <form id="newsletterFormInline" class="form-row" onsubmit="return submitInlineNewsletter(event)">
          <input id="newsletterNameInline" type="text" placeholder="Vorname (optional)" />
          <input id="newsletterEmail" type="email" placeholder="deine@email.de" required />
          <div style="display:flex;gap:8px">
            <button type="submit" class="btn btn-primary">Anmelden</button>
            <button type="button" class="btn" onclick="document.getElementById('newsletterEmail').value='';document.getElementById('newsletterNameInline').value='';">Zurücksetzen</button>
          </div>
        </form>
        <p class="small">Hinweis: Die Anmeldung öffnet dein E-Mail-Programm (mailto) und füllt Empfänger + Text. Ersetze die Empfängeradresse im Code mit deiner gewünschten Empfangsadresse.</p>
      </div>
    </aside>
  </main>

  <!-- Modal markup -->
  <div id="modalBackdrop" class="modal-backdrop" role="dialog" aria-modal="true" aria-hidden="true">
    <div class="modal" role="document" aria-labelledby="modalTitle">
      <h3 id="modalTitle">Bestellung</h3>
      <p>Das Produkt ist noch nicht verfügbar, melde dich für den Newsletter an um auf dem laufenden zu bleiben.</p>

      <form id="modalForm" class="form-row" onsubmit="return submitModalNewsletter(event)">
        <label for="name">Vorname (optional)</label>
        <input id="name" name="name" type="text" placeholder="Vorname" />

        <label for="email">E-Mail</label>
        <input id="email" name="email" type="email" placeholder="du@email.de" required />

        <div class="modal-footer">
          <button type="button" class="btn" onclick="closeModal()">Abbrechen</button>
          <button type="submit" class="btn btn-primary">Für Newsletter anmelden</button>
        </div>
      </form>
    </div>
  </div>

  <script>
    // === Konfiguration ===
    // Ersetze diese Adresse mit der E-Mail, an die die Anmeldungen gesendet werden sollen.
    const RECEIVER_EMAIL = 'you@yourdomain.de';

    const orderBtn = document.getElementById('orderBtn');
    const modalBackdrop = document.getElementById('modalBackdrop');

    orderBtn.addEventListener('click', openModal);
    modalBackdrop.addEventListener('click', (e) => { if (e.target === modalBackdrop) closeModal(); });

    function openModal(){
      modalBackdrop.style.display = 'flex';
      modalBackdrop.setAttribute('aria-hidden','false');
      document.getElementById('email').focus();
    }
    function closeModal(){
      modalBackdrop.style.display = 'none';
      modalBackdrop.setAttribute('aria-hidden','true');
    }

    // Construct a mailto link and open the user's email client with prefilled subject/body
    function sendMail(to, subject, body){
      const mailto = `mailto:${encodeURIComponent(to)}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
      window.location.href = mailto;
    }

    function submitModalNewsletter(e){
      e.preventDefault();
      const name = document.getElementById('name').value.trim();
      const email = document.getElementById('email').value.trim();
      if(!email) return alert('Bitte gib eine gültige E-Mail-Adresse ein.');

      const subject = 'Newsletter-Anmeldung: Produkt wartet';
      const body = `Newsletter-Anmeldung%0A%0AVorname: ${name}%0AEmail: ${email}%0A%0AQuelle: Landingpage`;

      // open mail client
      sendMail(RECEIVER_EMAIL, subject, `Vorname: ${name}%0AEmail: ${email}%0A%0AQuelle: Landingpage`);
      closeModal();
    }

    // Inline form in the aside (same behavior)
    function submitInlineNewsletter(e){
      e.preventDefault();
      const name = document.getElementById('newsletterNameInline').value.trim();
      const email = document.getElementById('newsletterEmail').value.trim();
      if(!email) return alert('Bitte gib eine gültige E-Mail-Adresse ein.');
      const subject = 'Newsletter-Anmeldung (Inline)';
      const body = `Vorname: ${name}%0AEmail: ${email}%0A%0AQuelle: Landingpage`;
      sendMail(RECEIVER_EMAIL, subject, body);
      // optional: clear fields
      document.getElementById('newsletterNameInline').value = '';
      document.getElementById('newsletterEmail').value = '';
      alert('Dein E-Mail-Programm sollte sich nun öffnen.');
      return false;
    }
  </script>
</body>
</html>
# locotails.github.io
