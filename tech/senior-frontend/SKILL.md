---
name: senior-frontend
description: >
  Développeur frontend senior pour HB Digital. Déclenche sur : créer une page,
  développer une landing page, HTML, CSS, JavaScript, React, intégrer un design,
  responsive, mobile-first, performance web, Core Web Vitals, temps de chargement,
  optimiser une page, intégrer un formulaire, JavaScript vanilla, animation CSS,
  Tailwind, composant, UI, interface. Contexte : LPs lead gen, sites WordPress,
  SEYDI Paris (Shopify), kits HTML email, outils d'interface interne.
  Self-healing : produit du code fonctionnel même avec des spécifications
  partielles.
---

# Senior Frontend — HB Digital Performance

## Contexte frontend HB Digital

| Projet | Stack | Contraintes principales |
|---|---|---|
| LPs Lead Gen | HTML statique + CSS + JS | Vitesse critique, zero framework |
| Sites WordPress | PHP + Elementor / Gutenberg | Compatibilité WP, performance |
| SEYDI Paris | Shopify Liquid + JS | Thème Shopify, limitations platform |
| Kits email HTML | HTML tables + CSS inline | Compatibilité Outlook, sans JS |
| Outils internes | React ou HTML/JS vanilla | Fonctionnalité prioritaire |
| Landing pages A/B | HTML statique | Chargement < 2s, mobile first |

---

## ÉTAPE 0 — Self-healing

| Situation | Comportement |
|---|---|
| Stack non précisée | Proposer HTML/CSS/JS vanilla (plus universel) |
| Design non fourni | Créer un design fonctionnel et propre |
| Specs incomplètes | Implémenter le cas standard + noter les variantes |
| Framework non précisé | Demander ou produire sans framework (plus léger) |

---

## ÉTAPE 1 — Standards de développement

### 1.1 Principes de base HB Digital Frontend

```
PERFORMANCE FIRST :
→ LCP (Largest Contentful Paint) < 2.5s
→ FID / INP < 100ms
→ CLS < 0.1
→ Poids total page < 300ko (sans images)

MOBILE FIRST :
→ Breakpoint principal : 375px (iPhone SE)
→ Tablet : 768px
→ Desktop : 1024px+

COMPATIBILITÉ :
→ Chrome, Firefox, Safari, Edge (2 dernières versions)
→ iOS Safari (critique pour lead gen)
→ Android Chrome
```

### 1.2 Structure HTML sémantique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="[Description SEO 150 car]">
  <title>[Titre SEO — 60 car max]</title>
  
  <!-- Preload des ressources critiques -->
  <link rel="preload" href="fonts/mon-font.woff2" as="font" type="font/woff2" crossorigin>
  
  <!-- CSS critique inline pour LCP -->
  <style>
    /* Styles above-the-fold uniquement */
    :root {
      --color-primary: #2563EB;
      --color-secondary: #F59E0B;
      --color-text: #1F2937;
      --color-bg: #FFFFFF;
    }
    /* ... */
  </style>
  
  <!-- CSS principal (defer) -->
  <link rel="stylesheet" href="styles.css" media="print" onload="this.media='all'">
</head>
<body>
  <header role="banner">...</header>
  <main id="main-content">...</main>
  <footer role="contentinfo">...</footer>
  
  <!-- JS en bas de page, defer -->
  <script src="main.js" defer></script>
</body>
</html>
```

---

## ÉTAPE 2 — Templates de composants

### 2.1 Landing page lead gen (structure complète)

```html
<!-- HERO SECTION -->
<section class="hero" aria-label="Accroche principale">
  <div class="container">
    <div class="hero__content">
      <h1 class="hero__title">
        [Bénéfice principal en une ligne]
      </h1>
      <p class="hero__subtitle">
        [Sous-titre bénéfice secondaire]
      </p>
      <a href="#formulaire" class="btn btn--primary">
        [Texte CTA orienté bénéfice]
      </a>
    </div>
    <div class="hero__visual">
      <img src="hero.webp" alt="[Description]" 
           width="600" height="400" loading="eager" fetchpriority="high">
    </div>
  </div>
</section>

<!-- BÉNÉFICES -->
<section class="benefits" aria-label="Avantages">
  <div class="container">
    <ul class="benefits__list" role="list">
      <li class="benefits__item">
        <span class="benefits__icon" aria-hidden="true">✓</span>
        <p>[Bénéfice 1]</p>
      </li>
      <!-- répéter × 3 -->
    </ul>
  </div>
</section>

<!-- FORMULAIRE -->
<section class="form-section" id="formulaire" aria-label="Formulaire de contact">
  <div class="container">
    <h2>[Titre formulaire]</h2>
    <form class="lead-form" novalidate>
      <div class="form-group">
        <label for="prenom">Prénom *</label>
        <input type="text" id="prenom" name="prenom" 
               required autocomplete="given-name"
               placeholder="Votre prénom">
      </div>
      <div class="form-group">
        <label for="telephone">Téléphone *</label>
        <input type="tel" id="telephone" name="telephone" 
               required autocomplete="tel"
               placeholder="06 XX XX XX XX"
               pattern="[0-9]{10}">
      </div>
      <div class="form-group">
        <label for="email">Email *</label>
        <input type="email" id="email" name="email" 
               required autocomplete="email"
               placeholder="votre@email.fr">
      </div>
      
      <!-- RGPD obligatoire -->
      <div class="form-group form-group--checkbox">
        <input type="checkbox" id="rgpd" name="rgpd" required>
        <label for="rgpd">
          J'accepte d'être contacté(e) et la 
          <a href="/politique-confidentialite">politique de confidentialité</a> *
        </label>
      </div>
      
      <button type="submit" class="btn btn--primary btn--full">
        [Texte CTA]
      </button>
    </form>
  </div>
</section>
```

### 2.2 CSS — Système de design minimal

```css
/* Variables CSS */
:root {
  --color-primary: #2563EB;
  --color-primary-dark: #1D4ED8;
  --color-secondary: #F59E0B;
  --color-success: #10B981;
  --color-text: #1F2937;
  --color-text-light: #6B7280;
  --color-bg: #FFFFFF;
  --color-bg-alt: #F3F4F6;
  --color-border: #E5E7EB;
  
  --font-family: system-ui, -apple-system, 'Segoe UI', sans-serif;
  --font-size-base: 16px;
  
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 2rem;
  --spacing-2xl: 3rem;
  
  --radius: 0.375rem;
  --shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
}

/* Reset minimal */
*, *::before, *::after { box-sizing: border-box; }
body { margin: 0; font-family: var(--font-family); color: var(--color-text); }
img { max-width: 100%; height: auto; }

/* Container */
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

/* Boutons */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.875rem 1.75rem;
  border: none;
  border-radius: var(--radius);
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.2s ease;
  min-height: 48px; /* Accessibilité tactile */
}

.btn--primary {
  background: var(--color-primary);
  color: white;
}

.btn--primary:hover {
  background: var(--color-primary-dark);
  transform: translateY(-1px);
}

.btn--full { width: 100%; }

/* Formulaire */
.form-group {
  margin-bottom: var(--spacing-md);
}

label {
  display: block;
  margin-bottom: var(--spacing-xs);
  font-weight: 500;
}

input[type="text"],
input[type="email"],
input[type="tel"] {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  font-size: 1rem;
  transition: border-color 0.2s;
}

input:focus {
  outline: 2px solid var(--color-primary);
  outline-offset: 1px;
  border-color: var(--color-primary);
}

/* Responsive */
@media (max-width: 768px) {
  h1 { font-size: 1.75rem; }
  .hero { padding: 2rem 0; }
}
```

### 2.3 JavaScript — Validation formulaire

```javascript
// Validation formulaire lead
const form = document.querySelector('.lead-form');

if (form) {
  form.addEventListener('submit', async (e) => {
    e.preventDefault();
    
    // Validation
    const errors = validateForm(form);
    if (errors.length > 0) {
      showErrors(errors);
      return;
    }
    
    // Tracking
    if (typeof gtag !== 'undefined') {
      gtag('event', 'generate_lead', { event_category: 'form' });
    }
    if (typeof fbq !== 'undefined') {
      fbq('track', 'Lead');
    }
    
    // Soumission
    const submitBtn = form.querySelector('[type="submit"]');
    submitBtn.disabled = true;
    submitBtn.textContent = 'Envoi en cours...';
    
    try {
      const formData = new FormData(form);
      const response = await fetch('/api/lead', {
        method: 'POST',
        body: formData
      });
      
      if (response.ok) {
        window.location.href = '/merci';
      } else {
        throw new Error('Erreur serveur');
      }
    } catch (error) {
      submitBtn.disabled = false;
      submitBtn.textContent = 'Réessayer';
      showError(form, 'Une erreur est survenue. Veuillez réessayer.');
    }
  });
}

function validateForm(form) {
  const errors = [];
  const email = form.querySelector('#email').value;
  const tel = form.querySelector('#telephone').value;
  const rgpd = form.querySelector('#rgpd').checked;
  
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
    errors.push({ field: 'email', message: 'Email invalide' });
  }
  
  if (!/^[0-9]{10}$/.test(tel.replace(/\s/g, ''))) {
    errors.push({ field: 'telephone', message: 'Numéro invalide (10 chiffres)' });
  }
  
  if (!rgpd) {
    errors.push({ field: 'rgpd', message: 'Consentement requis' });
  }
  
  return errors;
}
```

---

## ÉTAPE 3 — Performance et optimisation

### 3.1 Checklist Core Web Vitals

**LCP (< 2.5s) :**
- [ ] Image hero en WebP + attribut `fetchpriority="high"`
- [ ] CSS critique inline dans le `<head>`
- [ ] Police système ou `font-display: swap`
- [ ] Hébergement performant (CDN ou VPS rapide)

**CLS (< 0.1) :**
- [ ] Dimensions `width` et `height` sur toutes les images
- [ ] Espaces réservés pour les éléments qui chargent dynamiquement
- [ ] Pas d'injection de contenu au-dessus du fold

**FID/INP (< 100ms) :**
- [ ] JS chargé en `defer` ou `async`
- [ ] Pas de JavaScript bloquant dans le `<head>`
- [ ] Interactions gérées efficacement (pas de calculs lourds au clic)

### 3.2 Optimisation images

```html
<!-- Format WebP avec fallback -->
<picture>
  <source srcset="hero.webp" type="image/webp">
  <img src="hero.jpg" alt="[Description]" width="800" height="500" loading="lazy">
</picture>

<!-- Images above-the-fold : loading="eager" fetchpriority="high" -->
<!-- Images below-the-fold : loading="lazy" -->
```

---

## FORMAT DE SORTIE

```
## Développement Frontend — [Composant/Page]

**Stack :** [HTML/CSS/JS / React / Shopify / WordPress]
**Objectif :** [conversion / affichage / interface]

**Code livré :**
[HTML]
[CSS]
[JavaScript]

**Instructions de déploiement :**
[étapes concrètes]

**Tests recommandés :**
- [ ] Chrome DevTools Lighthouse
- [ ] Test mobile (iOS Safari, Android Chrome)
- [ ] Validation HTML : validator.w3.org
- [ ] Core Web Vitals : pagespeed.web.dev

**Prochaine étape :** [intégrer / tester / déployer / A/B tester]
```

---

## RÈGLES ABSOLUES

1. Mobile first — tester sur 375px avant le desktop
2. Performance first — chaque page doit scorer > 90 sur Lighthouse mobile
3. Accessibilité minimum — labels sur les inputs, alt sur les images, contraste suffisant
4. Pas de framework si une page HTML suffit — vitesse avant tout
5. Finir par les tests à effectuer avant mise en production
