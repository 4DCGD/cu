# 🏥 CuraFinder - Plateforme de Tourisme Médical

CuraFinder est une plateforme web moderne qui aide les patients à trouver des cliniques adaptées à leurs besoins médicaux en Turquie. La plateforme permet de rechercher, comparer et prendre rendez-vous facilement avec les meilleures cliniques.

![CuraFinder Platform](https://img.shields.io/badge/React-18.2.0-blue?style=for-the-badge&logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-4.9.5-blue?style=for-the-badge&logo=typescript)
![Material-UI](https://img.shields.io/badge/Material--UI-5.15.10-blue?style=for-the-badge&logo=mui)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## ✨ Fonctionnalités Principales

### 🔍 **Recherche Avancée**
- Recherche de cliniques par spécialité médicale
- Filtrage par localisation, prix, et disponibilité
- Système de notation et d'avis vérifiés
- Comparaison de cliniques côte à côte

### 👤 **Espace Patient**
- Profil utilisateur personnalisé
- Historique des consultations
- Messagerie avec les cliniques
- Système de favoris et de notes

### 🏥 **Espace Clinique**
- Dashboard pour les professionnels de santé
- Gestion des rendez-vous
- Communication avec les patients
- Statistiques et analyses

### 🌐 **Support Multilingue**
- Interface en français et anglais
- Support pour d'autres langues (en développement)
- Contenu localisé selon la région

### 📱 **Design Responsive**
- Interface optimisée pour mobile et desktop
- PWA (Progressive Web App) ready
- Performance optimisée avec lazy loading

## 🚀 Améliorations Récentes

### **Performance & Optimisation**
- ✅ **Lazy Loading** - Chargement différé des pages pour améliorer les performances
- ✅ **Code Splitting** - Division automatique du bundle pour réduire la taille initiale
- ✅ **Suspense** - Gestion élégante des états de chargement
- ✅ **Error Boundaries** - Gestion robuste des erreurs React

### **Sécurité & Authentification**
- ✅ **Authentification Renforcée** - Système de tokens avec refresh automatique
- ✅ **Protection contre les attaques** - Limitation des tentatives de connexion
- ✅ **Validation des données** - Vérification stricte des entrées utilisateur
- ✅ **Gestion des sessions** - Expiration automatique des tokens

### **SEO & Accessibilité**
- ✅ **Meta Tags Optimisés** - Balises Open Graph et Twitter Cards
- ✅ **Structured Data** - Données structurées pour les moteurs de recherche
- ✅ **Performance Core Web Vitals** - Optimisation des métriques de performance
- ✅ **Accessibilité** - Support des lecteurs d'écran et navigation clavier

### **Expérience Utilisateur**
- ✅ **Loading States** - États de chargement élégants avec skeletons
- ✅ **Error Handling** - Gestion d'erreurs conviviale
- ✅ **Responsive Design** - Interface adaptée à tous les écrans
- ✅ **Dark Mode** - Thème sombre/clair avec persistance

## 🛠 Technologies Utilisées

### **Frontend**
- **React 18** - Bibliothèque UI avec hooks et Suspense
- **TypeScript** - Typage statique pour la robustesse du code
- **Material-UI (MUI)** - Composants UI modernes et accessibles
- **React Router** - Navigation côté client
- **i18next** - Internationalisation

### **Outils de Développement**
- **ESLint** - Linting du code avec règles TypeScript
- **Prettier** - Formatage automatique du code
- **Web Vitals** - Monitoring des performances
- **Jest & Testing Library** - Tests unitaires et d'intégration

### **Architecture**
- **Context API** - Gestion d'état globale
- **Custom Hooks** - Logique réutilisable
- **Service Layer** - Séparation des préoccupations
- **Error Boundaries** - Gestion d'erreurs React

## 📦 Installation

### **Prérequis**
- Node.js (version 16 ou supérieure)
- npm ou yarn
- Git

### **Installation Rapide**

```bash
# Cloner le repository
git clone https://github.com/dief36/Curafinder.git
cd Curafinder

# Installer les dépendances
npm install

# Lancer en mode développement
npm start
```

L'application sera accessible à l'adresse [http://localhost:3000](http://localhost:3000).

### **Scripts Disponibles**

```bash
# Développement
npm start              # Lance le serveur de développement
npm run lint           # Vérifie le code avec ESLint
npm run lint:fix       # Corrige automatiquement les erreurs ESLint
npm run format         # Formate le code avec Prettier
npm run type-check     # Vérifie les types TypeScript

# Production
npm run build          # Crée un build optimisé
npm run build:analyze  # Analyse la taille du bundle
npm run serve          # Lance un serveur local pour tester le build

# Tests
npm test               # Lance les tests en mode watch
npm run test:coverage  # Lance les tests avec couverture
npm run test:ci        # Lance les tests en mode CI
```

## 🏗 Structure du Projet

```
src/
├── components/          # Composants réutilisables
│   ├── Navbar.tsx      # Navigation principale
│   ├── Footer.tsx      # Pied de page
│   ├── LoadingSpinner.tsx # Composant de chargement
│   └── ErrorBoundary.tsx  # Gestionnaire d'erreurs
├── pages/              # Pages de l'application
│   ├── HomePage.tsx    # Page d'accueil
│   ├── SearchPage.tsx  # Page de recherche
│   ├── LoginPage.tsx   # Page de connexion
│   ├── RegisterPage.tsx # Page d'inscription
│   ├── UserDashboard.tsx # Dashboard utilisateur
│   ├── AdminDashboard.tsx # Dashboard administrateur
│   └── ...             # Autres pages
├── contexts/           # Contextes React
│   ├── AuthContext.tsx # Gestion de l'authentification
│   └── ThemeContext.tsx # Gestion du thème
├── services/           # Services API
│   ├── authService.ts  # Service d'authentification
│   └── adminService.ts # Service administrateur
├── hooks/              # Custom hooks
│   └── useApi.ts       # Hook pour les appels API
├── utils/              # Utilitaires
│   └── placeholderImages.ts # Images de placeholder
├── locales/            # Fichiers de traduction
│   ├── fr/             # Français
│   └── en/             # Anglais
├── layouts/            # Layouts de pages
└── assets/             # Ressources statiques
```

## 🔧 Configuration

### **Variables d'Environnement**

Créez un fichier `.env` à la racine du projet :

```env
REACT_APP_API_URL=https://api.curafinder.com
REACT_APP_ENVIRONMENT=development
REACT_APP_GOOGLE_ANALYTICS_ID=GA_MEASUREMENT_ID
```

### **Configuration TypeScript**

Le projet utilise TypeScript avec une configuration stricte pour garantir la qualité du code.

### **Configuration ESLint**

ESLint est configuré avec des règles TypeScript et React pour maintenir la qualité du code.

## 🧪 Tests

```bash
# Lancer tous les tests
npm test

# Lancer les tests avec couverture
npm run test:coverage

# Lancer les tests en mode CI
npm run test:ci
```

## 📊 Performance

### **Core Web Vitals**
- **LCP (Largest Contentful Paint)** : < 2.5s
- **FID (First Input Delay)** : < 100ms
- **CLS (Cumulative Layout Shift)** : < 0.1

### **Optimisations**
- Lazy loading des routes
- Code splitting automatique
- Images optimisées
- Cache des requêtes API
- Compression des assets

## 🔒 Sécurité

### **Authentification**
- Tokens JWT avec expiration
- Refresh tokens automatiques
- Protection contre les attaques par force brute
- Validation stricte des entrées

### **Données**
- Chiffrement des mots de passe
- Validation côté client et serveur
- Protection CSRF
- Headers de sécurité

## 🌍 Déploiement

### **Netlify**
```bash
npm run build
# Déployer le dossier 'build'
```

### **Vercel**
```bash
npm run build
# Déployer avec Vercel CLI
```

### **Docker**
```dockerfile
FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

## 🤝 Contribution

Les contributions sont les bienvenues ! Voici comment contribuer :

1. **Fork** le projet
2. **Créez** une branche pour votre fonctionnalité (`git checkout -b feature/AmazingFeature`)
3. **Commitez** vos changements (`git commit -m 'Add some AmazingFeature'`)
4. **Poussez** vers la branche (`git push origin feature/AmazingFeature`)
5. **Ouvrez** une Pull Request

### **Guidelines de Contribution**
- Respectez les conventions de code
- Ajoutez des tests pour les nouvelles fonctionnalités
- Mettez à jour la documentation si nécessaire
- Vérifiez que tous les tests passent

## 📝 Changelog

### **v0.1.0** (2024-01-15)
- ✅ Lazy loading des routes
- ✅ Error boundaries
- ✅ Authentification renforcée
- ✅ SEO optimisé
- ✅ Performance améliorée
- ✅ Design responsive
- ✅ Support multilingue

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

## 📞 Support

- **Email** : support@curafinder.com
- **Documentation** : [docs.curafinder.com](https://docs.curafinder.com)
- **Issues** : [GitHub Issues](https://github.com/dief36/Curafinder/issues)

## 🙏 Remerciements

- [Material-UI](https://mui.com/) pour les composants UI
- [React](https://reactjs.org/) pour le framework
- [TypeScript](https://www.typescriptlang.org/) pour le typage
- [i18next](https://www.i18next.com/) pour l'internationalisation

---

**CuraFinder** - Votre partenaire de confiance pour les soins médicaux en Turquie 🇹🇷
