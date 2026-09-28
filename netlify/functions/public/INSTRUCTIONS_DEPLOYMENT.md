# Instructions de Déploiement - CERES Scolarité

Tous les fichiers ont été créés et commités localement. Voici les étapes pour finaliser le déploiement:

## ✅ Ce qui a été fait

1. ✓ Créé la fonction backend `netlify/functions/demander-etablissement.js`
2. ✓ Créé la configuration Netlify (`netlify.toml`)
3. ✓ Créé le formulaire HTML (`public/demander-etablissement.html`)
4. ✓ Créé `package.json` avec les dépendances
5. ✓ Créé `.gitignore` pour exclure les fichiers inutiles
6. ✓ Mis à jour le `README.md` avec les instructions complètes
7. ✓ Commité tous les changements sur la branche `main`

## 🔄 Étapes suivantes

### Étape 1: Ajouter les variables d'environnement dans Netlify

1. Allez sur https://app.netlify.com
2. Sélectionnez votre projet `ceres-scolarite`
3. Allez à **Site settings** → **Build & deploy** → **Environment**
4. Ajoutez les variables:

   | Variable | Valeur |
   |----------|--------|
   | `RESEND_API_KEY` | Votre clé API Resend (déjà configurée ✓) |
   | `SUPABASE_URL` | `https://[votre-projet].supabase.co` |
   | `SUPABASE_ANON_KEY` | Votre clé Supabase publique |

**Pour obtenir vos clés Supabase:**
1. Allez sur https://supabase.com
2. Connectez-vous à votre projet
3. Allez à **Settings** → **API**
4. Copiez `Project URL` et `anon public key`

### Étape 2: Créer la table dans Supabase

1. Allez sur https://supabase.com et ouvrez votre projet
2. Allez à **SQL Editor**
3. Créez une nouvelle requête
4. Copiez et exécutez ce code:

```sql
CREATE TABLE demandes_etablissements (
  id SERIAL PRIMARY KEY,
  nom_etablissement VARCHAR(255) NOT NULL,
  ville VARCHAR(255) NOT NULL,
  province VARCHAR(255) NOT NULL,
  nom_directeur VARCHAR(255) NOT NULL,
  telephone VARCHAR(20) NOT NULL,
  email VARCHAR(255) NOT NULL,
  formule_souhaitee VARCHAR(255) NOT NULL,
  message TEXT,
  date_soumission TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  email_envoye BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Étape 3: Connecter GitHub à Netlify (Déploiement Automatique)

1. Dans Netlify, allez à **Site settings** → **Build & deploy**
2. Cliquez sur **Connect repository** (sous "Continuous Deployment")
3. Sélectionnez GitHub et choisissez `ahmatbongo/ceres-scolarite`
4. Configurez:
   - **Branch to deploy**: `main`
   - **Build command**: `npm install` (les dépendances)
   - **Publish directory**: `public`
5. Cliquez sur **Deploy site**

À partir de là, chaque push sur GitHub déclenchera automatiquement un déploiement!

### Étape 4: Tester le formulaire

1. Une fois déployé, allez sur: `https://ceres-scolarite.netlify.app/demander-etablissement.html`
2. Remplissez le formulaire avec des données de test
3. Vérifiez que:
   - ✓ Vous recevez un email à `ceres151266@gmail.com`
   - ✓ Les données apparaissent dans la table Supabase
   - ✓ Un message de confirmation s'affiche

## 🆘 Dépannage

**Erreur: "Module not found: 'resend'"**
- Netlify n'a pas installé les dépendances
- Solution: Assurez-vous que `package.json` est dans la racine du projet ✓

**Erreur: "SUPABASE_URL undefined"**
- La variable d'environnement n'est pas configurée
- Vérifiez dans Netlify → **Environment variables**

**Le formulaire soumet mais aucun email reçu**
1. Vérifiez la console du navigateur (F12)
2. Regardez les "Function logs" dans Netlify
3. Confirmez que RESEND_API_KEY est correct

## 📋 Checklist de Déploiement

- [ ] Variables d'environnement ajoutées dans Netlify
- [ ] Table Supabase créée
- [ ] GitHub connecté à Netlify pour le déploiement automatique
- [ ] Le formulaire est accessible et fonctionne
- [ ] Les emails sont reçus à ceres151266@gmail.com
- [ ] Les données sont stockées dans Supabase

## 💡 Prochaines Étapes

Une fois que tout fonctionne:
1. Intégrer le formulaire dans le menu principal du site
2. Ajouter une page de succès personnalisée
3. Configurer un domaine personnalisé (si souhaité)
4. Ajouter plus de formulaires ou fonctionnalités

## 📞 Besoin d'aide?

- Documentation Netlify: https://docs.netlify.com
- Documentation Resend: https://resend.com/docs
- Documentation Supabase: https://supabase.com/docs
- Contact: ceres151266@gmail.com
