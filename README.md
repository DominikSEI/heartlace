# YOURBRAND — Wedding Invitation Generator
## Setup & Deploy Guide

---

## 📁 Projektstruktur

```
/
├── netlify.toml          ← Netlify Konfiguration
├── public/
│   ├── index.html        ← Landing Page (Hauptseite)
│   ├── hochzeit-demo.html← Demo-Einladung (eingebettet auf Landing Page)
│   └── css/, js/, images/← Assets (aktuell leer, alles inline)
└── pages/
    ├── generator.html    ← Der KI-Generator für Kunden
    ├── impressum.html    ← Impressum (⚠️ Platzhalter befüllen!)
    └── datenschutz.html  ← Datenschutzerklärung
```

---

## 🚀 Schritt 1: GitHub Repository anlegen

```bash
# Im Projektordner:
git init
git add .
git commit -m "Initial commit — YOURBRAND wedding invitations"

# Dann auf github.com ein neues Repo anlegen und:
git remote add origin https://github.com/DEIN-USERNAME/yourbrand.git
git push -u origin main
```

---

## 🌐 Schritt 2: Netlify verbinden (automatisches Hosting)

1. Gehe zu **netlify.com** → kostenloser Account
2. Klick "Add new site" → "Import from Git"
3. GitHub verbinden → dein Repository auswählen
4. Build settings:
   - **Publish directory:** `public`
   - Build command: leer lassen
5. Klick "Deploy site"

✅ Deine Seite ist live! Netlify gibt dir eine URL wie `https://yourbrand.netlify.app`

**Auto-Deploy:** Jedes Mal wenn du `git push` machst → Netlify deployed automatisch.

---

## 🔑 Schritt 3: Anthropic API Key einrichten

Der Generator braucht einen API Key. Zwei Optionen:

### Option A: Netlify Environment Variables (empfohlen)
```
Netlify Dashboard → Site Settings → Environment Variables
→ Neue Variable: ANTHROPIC_API_KEY = sk-ant-xxxxx
```
Dann im generator.html den Fetch-Request anpassen:
```javascript
// Statt direktem API-Call → eigene Netlify Function bauen
fetch('/.netlify/functions/generate', { ... })
```

### Option B: Temporär direkt im Code (nur zum Testen!)
Im generator.html, im fetch-Call headers ergänzen:
```javascript
headers: {
  'Content-Type': 'application/json',
  'x-api-key': 'sk-ant-DEIN-KEY',  // ← nur zum lokalen Testen!
  'anthropic-version': '2023-06-01'
}
```
⚠️ Niemals einen API Key in öffentlichem Code committen!

---

## 💳 Schritt 4: Stripe für Bezahlung (optional, später)

1. Account auf **stripe.com** anlegen
2. Stripe Checkout Link erstellen (einfachste Option, kein Code nötig)
3. Link im generator.html als "Jetzt kaufen"-Button einbauen

---

## 🏠 Schritt 5: Eigene Domain

1. Domain kaufen z.B. auf **namecheap.com** oder **Hetzner** (~10€/Jahr)
2. In Netlify: Domain Management → Add custom domain
3. DNS bei deinem Registrar auf Netlify zeigen lassen
→ Netlify erklärt das Schritt für Schritt

---

## ⚠️ Impressum befüllen (WICHTIG!)

Vor dem Launch in `pages/impressum.html` und `pages/datenschutz.html`:
- [ ] Deinen vollständigen Namen eintragen
- [ ] Deine Adresse eintragen
- [ ] Deine E-Mail-Adresse eintragen
- [ ] Telefonnummer eintragen
- [ ] Ort des Gewerbeamts eintragen
- [ ] E-Mail in Datenschutz ersetzen

---

## 🎨 Logo erstellen mit Gemini / Midjourney

Kopiere diesen Prompt in **Gemini ImageFX** oder **Midjourney**:

### Prompt (Gemini ImageFX):
```
A minimalist luxury wedding brand logo for a company called "[DEIN NAME]". 
Elegant serif typography, thin golden letterforms on cream/off-white background. 
Small decorative botanical element — a single delicate rose branch or olive sprig — 
integrated into the lettering. Art deco inspired, refined, timeless. 
Horizontal layout. No gradients, flat design. Wedding stationery aesthetic. 
PNG with transparent background.
```

### Prompt (Midjourney):
```
/imagine logo design for luxury wedding invitation brand "[DEIN NAME]", 
minimal elegant serif font, gold color #b8955a on transparent background, 
small botanical flourish, art deco, flat design, vector style --v 6 --ar 3:1 --style raw
```

---

## 🔄 Claude Code — Erweiterungen

Mit Claude Code kannst du folgendes direkt im Terminal bauen:

```bash
# Claude Code starten im Projektordner:
claude

# Dann z.B. sagen:
"Baue eine Netlify Function in /netlify/functions/generate.js 
die den Anthropic API Key sicher aus Environment Variables liest 
und den Generator-Request weiterleitet"

"Füge Stripe Checkout zum Generator hinzu — nach der Vorschau 
soll ein Kaufen-Button erscheinen"

"Erstelle eine Admin-Seite unter /pages/admin.html wo ich 
alle RSVP-Antworten sehen kann"
```

---

## 📦 Lokale Entwicklung

```bash
# Netlify CLI installieren:
npm install -g netlify-cli

# Lokal starten:
netlify dev

# Öffnet http://localhost:8888
```

---

## 💰 Preisempfehlung zum Start

| Paket | Preis | Inhalt |
|-------|-------|--------|
| Essential | 39€ | Einladungsseite, 6 Stile, RSVP, 12 Monate |
| Full Story | 69€ | + Fotos, Quiz-Reveal, Custom Domain |

**Kleinunternehmerregelung:** Bis 22.000€ Jahresumsatz keine MwSt. 
→ Preise sind Bruttopreise, keine MwSt. ausweisen!

---

## 📱 Marketing-Tipps

### Instagram / TikTok Content-Ideen:
1. Screen-Recording: Generator ausfüllen → fertige Seite in 60 Sekunden
2. Vorher/Nachher: WhatsApp-Screenshot-Einladung vs. deine Seite
3. "Rate my wedding invitation" — verschiedene Stile zeigen
4. Behind the scenes: wie KI die Seite generiert

### Keywords für SEO:
- "digitale Hochzeitseinladung"
- "wedding invitation website"
- "online Hochzeitseinladung erstellen"
- "Hochzeitseinladung Link teilen"

---

Viel Erfolg! 🌿
