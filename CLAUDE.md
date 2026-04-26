# CLAUDE.md — Portfolio Chayann Lucas

Mémoire persistante du projet. Mis à jour au fil des sessions.

---

## 1. Contexte du projet

Portfolio académique de **Chayann Lucas**, étudiant en **BTS SIO option SISR** au lycée Félix Le Dantec (Lannion), présenté pour l'épreuve **E5/E6**.

- **Cible d'affichage** : écran ordinateur (jury de soutenance). Le responsive mobile n'est pas une priorité — ne pas s'inquiéter si une modification dégrade légèrement l'affichage mobile.
- **Hébergement** : GitHub (push manuel). Aucun pipeline CI/CD, aucun déploiement automatique.
- **Contenu** : pages thématiques (parcours, projets, compétences, stages, certifications, veille, contact, docs) modifiées progressivement au fil des sessions.

---

## 2. Stack technique

| Techno | Détail |
|---|---|
| HTML5 | Toutes les pages, `lang="fr"` |
| Bootstrap CSS | **5.3.0** — CDN jsdelivr |
| Bootstrap JS Bundle | **5.3.0** — CDN jsdelivr — chargé uniquement sur `stages.html`, `Contact.html`, `Doc.html` (manquant ailleurs) |
| CSS custom | `styles.css` — fichier unique à la racine (~460 lignes) |
| JavaScript | Vanilla JS inline dans `<script>` — pas de framework, pas de bibliothèque externe |
| Images / PDFs | Hébergés externement sur `clucasit.wordpress.com` |

Aucun outil de build, aucun `package.json`, aucun préprocesseur CSS.

---

## 3. Structure du projet

```
portfolio/
├── index.html           # Accueil / À propos
├── parcours.html        # Parcours scolaire
├── certification.html   # Certifications
├── competences.html     # Compétences techniques
├── stages.html          # Expériences professionnelles
├── Veille.html          # Veille technologique (+ easter egg)
├── projets.html         # Projets pédagogiques (page principale)
├── Contact.html         # Informations de contact
├── Doc.html             # Documentations techniques (PDF)
└── styles.css           # Feuille de style unique
```

Pas de sous-dossiers. Toutes les images et PDFs sont des liens externes WordPress.

---

## 4. Conventions de code

### Nommage des fichiers
- Majorité en minuscules (`index.html`, `projets.html`, `competences.html`)
- Exceptions avec majuscule initiale : `Veille.html`, `Contact.html`, `Doc.html` (incohérence historique, à corriger un jour)

### Structure des pages
Chaque page partage le même squelette :
1. `<nav>` Bootstrap fixe en haut (copié-collé identique sur toutes les pages)
2. Contenu principal dans `<section class="container ...">` ou `<div class="...page">`
3. `<footer>` identique sur toutes les pages
4. `<script>` inline en fin de body pour l'active nav (+ lightbox sur projets.html)

### Active nav link
Géré par JS vanilla (DOMContentLoaded) : compare `window.location.pathname.split("/").pop()` au `href` de chaque `.nav-link`, puis ajoute la classe `active`.

### Body class
- `class="bg-light"` : pages standard
- `class="index-page"` : uniquement `index.html`

### Composants CSS réutilisables
| Classe | Usage |
|---|---|
| `.competence-card` | Carte contenu textuel (compétences, veille, contact) |
| `.projet-card` | Carte projet pédagogique |
| `.certificate` | Carte certification |
| `.formation` | Bloc parcours / stage (image + texte + date) |
| `.doc-block` | Bloc documentation (image + texte + bouton) |
| `.btn-doc` | Bouton bleu navbar "Docs" |
| `.btn-doc-projet` | Bouton bleu interne projets.html |
| `.section-title` | Titre de section uppercase avec border-bottom |
| `.barre-separation` | Ligne dégradée bleu sous les titres |

### CSS page-spécifique
Certaines pages ont un bloc `<style>` dans leur `<head>` pour les règles locales (ex: `.projets-grid`, `.lightbox` sur `projets.html` ; `.doc-block img` sur `Doc.html`). C'est voulu — ne pas tout déplacer dans `styles.css`.

### Navbar gradient
La navbar a un fond dégradé bleu foncé → bleu cyan (`#0a3664` → `#0d637a`) défini dans `styles.css`, avec texte blanc.

---

## 5. Pages existantes

| Fichier | Titre affiché | Description |
|---|---|---|
| `index.html` | À propos | Portrait, présentation personnelle, lien CV (PDF) |
| `parcours.html` | Parcours scolaire | Timeline : Collège → Bac Pro SN → BTS SIO SISR |
| `certification.html` | Certifications | PIX ×2, CNIL RGPD M1-M4, ANSSI SecNum |
| `competences.html` | Compétences | 9 cartes : Cybersécurité, Réseaux, Systèmes, Virtualisation, Infra/Parc, Gestion de projet, Dev/Web, Savoir-faire, Outils |
| `stages.html` | Expériences pro | 8 stages de 2021 à 2026 (SBSI, ELTEC, QI Info ×2, MBJ, Hutchinson ×3) |
| `Veille.html` | Veille technologique | Méthode, sources YouTube/blogs, outils, objectifs |
| `projets.html` | Projets pédagogiques | 7 projets avec lightbox (voir ci-dessous) |
| `Contact.html` | Contact | Email, téléphone, LinkedIn, GitHub |
| `Doc.html` | Documentations | 4 blocs PDF (Ferme RDS, Geltram, Veeam, Hardened Repo) |

### Projets pédagogiques (projets.html — 7 projets)
1. AP Semestre 1 – Egnaro (architecture réseau sécurisée)
2. AP Semestre 2 – Geltram (infra AD, PfSense, GLPI, FOG, WSUS)
3. Projet Ferme RDS (Session Hosts, Connection Broker, UPD)
4. Projet Infrastructure de Sauvegarde (Veeam, SureBackup, Virtual Lab)
5. AP Semestre 3A – GSB Projet A (DMZ, haute dispo, OPNsense)
6. AP Semestre 3B – GSB Projet B (double pare-feu, SIEM Graylog+Wazuh, Zabbix)
7. AP Semestre 4 – GSB Projet C (VPN IPSec/OpenVPN, VoIP, RADIUS, Bastion)

---

## 6. Règles à respecter

### Ne pas toucher
- **Easter eggs** : lien ✨ (toutatice) sur `index.html` et `.hacker-mode` sur `Veille.html` — volontaires, à conserver.

### Modifications directes (sans demander)
- Retouches texte, ajout/modification d'un projet ou d'une certification
- Ajustements CSS (couleurs, espacements, typographie)
- Animations CSS légères et discrètes, transitions (rester sobre et professionnel)
- Corrections de bugs mineurs

### Demander confirmation avant
- Toute refonte structurelle : navbar, footer, organisation globale des pages
- Changement du système de composants (renommer/fusionner des classes majeures)
- Ajout d'une nouvelle page

### Structure de projets.html — immuable
Chaque `.projet-card` doit conserver l'ordre : **Contexte → Points clés → Schéma → Lightbox fullscreen → (optionnel) bouton PDF**. Ne pas réorganiser cette structure.

### Style général
- Sobre et professionnel (portfolio académique, pas un site vitrine créatif)
- Cohérence visuelle entre les pages (même navbar, même footer, mêmes couleurs)
- Palette principale : bleu `#2563eb` / `#1881e9`, fond `#f8f9fa`, cartes blanches avec `box-shadow` léger

---

## 7. TODO

> À traiter quand le temps le permet.

- [ ] **Casse incohérente des noms de fichiers** : `Veille.html`, `Contact.html`, `Doc.html` devraient être en minuscules comme les autres — risque 404 sur serveur Linux (case-sensitive). Renommer + mettre à jour tous les liens internes.
- [ ] **Bootstrap JS manquant** sur la plupart des pages : `stages.html`, `Contact.html`, `Doc.html` ont le bundle JS, mais `index.html`, `parcours.html`, `certification.html`, `competences.html`, `Veille.html`, `projets.html` ne l'ont pas — le hamburger mobile peut ne pas fonctionner.
- [ ] **Lien actif cassé dans Contact.html** : le JS de nav compare au nom de fichier `contact.html` (minuscule) alors que le fichier s'appelle `Contact.html` — l'item Contact ne s'active jamais.
- [ ] **Balise `</div>` orpheline dans parcours.html** : une balise fermante en excès en fin de fichier (ligne ~119).
