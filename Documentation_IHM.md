# Documentation des Prototypes d'Interface (IHM)
## Système d'évaluation des enseignants

---

## 📱 Vue d'ensemble des interfaces créées

### Fichiers PlantUML Salt créés

1. **[IHM_UC1_Remplir_Evaluation.puml](IHM_UC1_Remplir_Evaluation.puml)** - 7 écrans
2. **[IHM_UC6_Tableau_Bord.puml](IHM_UC6_Tableau_Bord.puml)** - 8 écrans
3. **[Navigation_Globale.puml](Navigation_Globale.puml)** - Diagramme de navigation complet

**Total : 15 écrans + 1 diagramme de navigation**

---

## 🎨 UC1 : Remplir une évaluation (7 écrans)

### Écran 1 : Liste des évaluations disponibles (Desktop)
**Rôle :** Page d'accueil de l'étudiant  
**Éléments principaux :**
- En-tête avec nom utilisateur et déconnexion
- Menu de navigation (Tableau de bord, Mes évaluations, Historique, Notifications, Aide)
- Tableau des évaluations en attente avec statut (À compléter, Brouillon, Non commencée)
- Boutons d'action (Commencer, Reprendre)
- Indicateur du nombre d'évaluations en attente

**Actions possibles :**
- Commencer une nouvelle évaluation → Écran 2
- Reprendre un brouillon → Écran 2 (pré-rempli)
- Actualiser la liste

---

### Écran 2 : Formulaire d'évaluation (Desktop)
**Rôle :** Interface principale de saisie des évaluations  
**Éléments principaux :**
- Fil d'Ariane avec bouton retour
- Indicateur de progression (barre + pourcentage)
- Temps restant avant expiration
- Formulaire par sections (repliables/dépliables)
- Questions avec différents types de réponses (radio, textarea)
- Indicateurs de questions obligatoires (*)
- Zones de commentaires libres anonymes

**Sections affichées :**
1. Qualité de l'enseignement (6 questions)
2. Matériel pédagogique (4 questions)
3. Évaluation globale (3 questions)

**Actions possibles :**
- Sauvegarder brouillon → Écran 1
- Annuler → Écran 1 (avec confirmation)
- Continuer → Écran 3 ou Écran 7 (si erreurs)

---

### Écran 3 : Confirmation avant soumission
**Rôle :** Récapitulatif et validation finale  
**Éléments principaux :**
- Résumé complet de l'évaluation
- Nombre de questions remplies par section
- Note globale calculée
- Nombre de commentaires ajoutés
- Avertissement sur l'impossibilité de modifier après soumission
- Rappel de l'anonymat garanti
- Checkbox de certification

**Actions possibles :**
- Annuler → Écran 1
- Modifier → Écran 2
- Soumettre l'évaluation → Écran 4 (ou erreur système)

---

### Écran 4 : Confirmation de soumission réussie
**Rôle :** Confirmation et prochaines étapes  
**Éléments principaux :**
- Message de succès (✓ vert)
- Récapitulatif de la soumission (cours, date, référence)
- Mention de l'email de confirmation
- Rappel des évaluations restantes
- Suggestions de prochaines actions

**Actions possibles :**
- Retour à la liste → Écran 1
- Voir l'historique → Historique des évaluations

---

### Écran 5 : Version Mobile - Liste des évaluations
**Rôle :** Interface mobile optimisée  
**Éléments principaux :**
- Header compact avec menu hamburger
- Cartes d'évaluation empilées verticalement
- Informations essentielles (prof, cours, statut, deadline)
- Boutons d'action tactiles
- Navigation bottom bar

**Spécificités mobile :**
- Design vertical scroll
- Boutons plus grands (touch-friendly)
- Informations condensées
- Bottom navigation bar

---

### Écran 6 : Version Mobile - Formulaire d'évaluation
**Rôle :** Formulaire adapté mobile  
**Éléments principaux :**
- Navigation par sections (1 section à la fois)
- Barre de progression
- Questions affichées une par une ou par petits groupes
- Boutons de navigation (Précédent/Suivant)
- Sauvegarde automatique

**Spécificités mobile :**
- Scroll vertical
- Questions condensées
- Options radio adaptées au tactile
- Auto-save fréquent

---

### Écran 7 : Erreur de validation (questions manquantes)
**Rôle :** Gestion des erreurs de saisie  
**Éléments principaux :**
- Message d'erreur clair en rouge
- Liste détaillée des champs manquants (section, question)
- Bouton pour naviguer directement à la première erreur
- Questions manquantes surlignées en rouge
- Indicateurs visuels (⚠️)

**Actions possibles :**
- Aller à la première question manquante (scroll auto)
- Compléter les champs
- Sauvegarder brouillon
- Réessayer la soumission → Écran 3 (si OK)

---

## 📊 UC6 : Visualiser le tableau de bord (8 écrans)

### Écran 1 : Tableau de bord principal - Enseignant (Desktop)
**Rôle :** Vue d'ensemble des performances  
**Éléments principaux :**
- **4 KPI principaux** (cartes avec icônes)
  - Note globale (4.2/5.0) avec évolution
  - Taux de participation (87%) avec tendance
  - Nombre d'évaluations (142)
  - Taux de satisfaction (85%) avec évolution
- **Graphique d'évolution temporelle** (ligne)
  - Affichage de septembre à février
  - Tendance visible
- **Répartition par catégorie** (barres horizontales)
  - 6 catégories avec notes sur 5
- **Commentaires récents** (tableau)
  - 5 derniers commentaires avec sentiment
- **Filtres et exports**
  - Sélecteur de période
  - Boutons actualiser et exporter PDF

**Actions possibles :**
- Appliquer des filtres → Écran 2
- Voir tous les commentaires → Écran 3
- Accéder aux statistiques détaillées → Écran 4
- Exporter en PDF

---

### Écran 2 : Tableau de bord avec filtres actifs
**Rôle :** Vue filtrée et personnalisée  
**Éléments principaux :**
- Zone de filtres avec dropdowns
  - Période (année, semestre, mois)
  - Cours spécifique
  - Note minimale
- Tags de filtres actifs (supprimables)
- KPI recalculés selon filtres
- Distribution des notes (graphique en barres)
- Résultats filtrés mis en évidence

**Actions possibles :**
- Appliquer/modifier filtres
- Réinitialiser tous les filtres → Écran 1
- Supprimer un filtre individuel

---

### Écran 3 : Page des commentaires détaillés
**Rôle :** Consultation exhaustive des commentaires anonymes  
**Éléments principaux :**
- Barre de recherche textuelle
- Filtres par sentiment (positif/neutre/négatif)
- Tri (plus récent, plus utile)
- Liste de commentaires avec :
  - Sentiment visuel (😊 😐 😢)
  - Date et cours
  - Contenu du commentaire
  - Boutons d'action (utile, marquer, signaler)
- Pagination (page X/Y)

**Actions possibles :**
- Rechercher dans les commentaires
- Filtrer par sentiment
- Trier les commentaires
- Marquer un commentaire
- Signaler un commentaire inapproprié
- Naviguer entre les pages

---

### Écran 4 : Statistiques détaillées par cours
**Rôle :** Analyse approfondie d'un cours spécifique  
**Éléments principaux :**
- Sélecteur de cours (dropdown)
- **Vue d'ensemble du cours**
  - Période, nombre d'étudiants, taux de participation, note moyenne
- **Tableau d'analyse par question**
  - Chaque question avec sa moyenne
  - Évolution par rapport à la période précédente (▲▼─)
  - Bouton "Voir détails" par question
- **Points forts et axes d'amélioration**
  - Deux colonnes comparatives
  - Identification automatique

**Actions possibles :**
- Changer de cours
- Voir détails d'une question spécifique
- Exporter le rapport du cours

---

### Écran 5 : Comparaison avec moyennes (Administrateur)
**Rôle :** Positionnement par rapport aux pairs  
**Éléments principaux :**
- **KPI comparatifs**
  - Note de l'enseignant
  - Moyenne du département
  - Classement et quartile
- **Graphique de comparaison**
  - Barres comparatives par catégorie
  - Enseignant vs Moyenne département
- **Analyse comparative textuelle**
  - Points supérieurs à la moyenne
  - Tendances observées
  - Positionnement (top 20%, etc.)

**Spécificité :** Accessible uniquement aux administrateurs (et enseignants si configuré)

---

### Écran 6 : Version Mobile - Tableau de bord
**Rôle :** Dashboard optimisé mobile  
**Éléments principaux :**
- Header compact
- KPI empilés verticalement (cartes)
- Graphique d'évolution simplifié
- 2 derniers commentaires avec bouton "Voir plus"
- Bottom navigation bar

**Spécificités mobile :**
- Chargement progressif (données légères d'abord)
- Graphiques adaptés (touch, zoom)
- Scroll vertical
- Navigation tactile

---

### Écran 7 : Aucune donnée disponible (Nouvel enseignant)
**Rôle :** État vide avec guidance  
**Éléments principaux :**
- Message de bienvenue
- Explication claire (aucune évaluation reçue)
- **Prochaines étapes**
  - Informations sur le processus
  - Quand les données apparaîtront
  - Comment ça fonctionne
- Boutons d'aide
  - Consulter le guide
  - Contacter le support

**Objectif :** Rassurer et informer les nouveaux enseignants

---

### Écran 8 : Erreur de chargement
**Rôle :** Gestion des erreurs techniques  
**Éléments principaux :**
- Message d'erreur clair (❌ rouge)
- **Raisons possibles**
  - Problème de connexion
  - Maintenance en cours
  - Timeout
- **Solutions proposées**
  - Vérifier la connexion
  - Réessayer
  - Contacter le support
- Boutons d'action
  - Réessayer (avec spinner)
  - Contacter le support

---

## 🗺️ Diagramme de navigation globale

### Fichier : [Navigation_Globale.puml](Navigation_Globale.puml)

Ce diagramme d'états-transitions représente :

1. **Authentification et routage par rôle**
   - Connexion → Vérification du rôle
   - Redirection vers l'espace approprié (Étudiant/Enseignant/Admin)

2. **Espace Étudiant (UC1)**
   - Liste des évaluations ↔ Formulaire ↔ Confirmation ↔ Succès
   - Gestion des brouillons
   - Historique des évaluations

3. **Espace Enseignant (UC6)**
   - Dashboard principal ↔ Vues filtrées
   - Dashboard ↔ Commentaires détaillés
   - Dashboard ↔ Statistiques par cours
   - Cas particuliers (aucune donnée)

4. **Espace Administrateur**
   - Vue d'ensemble ↔ Comparaisons
   - Vue d'ensemble ↔ Rapports
   - Vue d'ensemble ↔ Gestion système

5. **Version Mobile**
   - Navigation adaptée pour UC1 et UC6
   - États spécifiques mobile

6. **Gestion des erreurs**
   - Erreurs de validation
   - Erreurs de chargement
   - Erreurs de soumission

---

## 🎯 Principes de conception appliqués

### 1. Cohérence visuelle
- En-têtes uniformes sur toutes les pages
- Navigation cohérente (menu top + fil d'Ariane)
- Codes couleurs standardisés :
  - ✅ Vert : Succès, positif
  - ⚠️ Orange : Attention, neutre
  - ❌ Rouge : Erreur, négatif
  - 🔵 Bleu : Information

### 2. Feedback utilisateur
- Messages de confirmation clairs
- Indicateurs de progression visibles
- États de chargement
- Messages d'erreur explicites avec solutions

### 3. Accessibilité
- Hiérarchie d'information claire
- Contrastes suffisants
- Textes alternatifs (icônes + texte)
- Navigation au clavier possible

### 4. Responsive Design
- Versions desktop et mobile distinctes
- Adaptation tactile (boutons plus grands)
- Navigation simplifiée sur mobile
- Chargement progressif sur mobile

### 5. Performance
- Chargement progressif des données
- Sauvegarde automatique (brouillons)
- Mise en cache des données fréquentes
- Feedback immédiat sur les actions

---

## 🔄 Flux de navigation principaux

### Flux 1 : Étudiant remplit une évaluation (Scénario idéal)
```
[Écran 1] Liste évaluations
    ↓ Clic "Commencer"
[Écran 2] Formulaire d'évaluation
    ↓ Remplit + Clic "Continuer"
[Écran 3] Confirmation
    ↓ Clic "Soumettre"
[Écran 4] Succès
    ↓ Clic "Retour liste"
[Écran 1] Liste évaluations (mise à jour)
```

### Flux 2 : Étudiant avec erreur de validation
```
[Écran 1] Liste évaluations
    ↓ Clic "Commencer"
[Écran 2] Formulaire (remplissage partiel)
    ↓ Clic "Continuer"
[Écran 7] Erreur de validation
    ↓ Clic "Aller à la première erreur"
[Écran 2] Formulaire (scroll auto + correction)
    ↓ Complète + Clic "Continuer"
[Écran 3] Confirmation
    ↓ Clic "Soumettre"
[Écran 4] Succès
```

### Flux 3 : Étudiant sauvegarde un brouillon (Mobile)
```
[Écran 5] Liste mobile
    ↓ Clic "Commencer"
[Écran 6] Formulaire mobile
    ↓ Remplit partiellement
    ↓ Clic "Sauvegarder brouillon"
[Écran 5] Liste mobile (avec statut "Brouillon 45%")

... Plus tard ...

[Écran 5] Liste mobile
    ↓ Clic "Reprendre"
[Écran 6] Formulaire mobile (pré-rempli)
    ↓ Continue et soumet
```

### Flux 4 : Enseignant consulte son tableau de bord
```
[Écran 1] Dashboard principal
    ↓ Applique filtres
[Écran 2] Dashboard filtré
    ↓ Clic "Voir tous les commentaires"
[Écran 3] Page commentaires
    ↓ Recherche/Filtre
    ↓ Retour
[Écran 1] Dashboard principal
    ↓ Clic "Statistiques détaillées"
[Écran 4] Stats par cours
```

### Flux 5 : Enseignant mobile
```
[Écran 6] Dashboard mobile (vue simplifiée)
    ↓ Clic "Voir détails"
[Chargement progressif]
[Écran 6] Dashboard mobile (vue complète)
```

---

## ✅ Couverture fonctionnelle

### UC1 : Remplir une évaluation
- ✅ Scénario idéal complet (7 étapes)
- ✅ Alternative 1 : Validation incomplète (Écran 7)
- ✅ Alternative 2 : Sauvegarde brouillon (Écrans 5-6 mobile)
- ✅ Alternative 3 : Erreur système (mentionnée, pas d'écran dédié)
- ✅ Versions desktop et mobile

### UC6 : Visualiser le tableau de bord
- ✅ Scénario idéal (Écran 1)
- ✅ Alternative 1 : Aucune donnée (Écran 7)
- ✅ Alternative 2 : Version mobile (Écran 6)
- ✅ Alternative 3 : Comparaisons (Écran 5)
- ✅ Alternative 4 : Erreur chargement (Écran 8)
- ✅ Filtrage interactif (Écran 2)
- ✅ Commentaires détaillés (Écran 3)
- ✅ Statistiques approfondies (Écran 4)

---

## 📋 Prochaines étapes recommandées

### 1. Diagramme d'états-transitions de navigation
✅ **Déjà créé** : [Navigation_Globale.puml](Navigation_Globale.puml)

Ce diagramme peut servir de base pour votre diagramme d'états-transitions demandé.

### 2. BPMN (Business Process Model and Notation)
À créer avec 2 pools :
- **Pool 1 : Étudiants** (processus d'évaluation)
- **Pool 2 : Université** (gestion et analyse)

PlantUML supporte nativement BPMN ! Je peux créer ce diagramme si vous le souhaitez.

### 3. Tests utilisateurs
- Tester les prototypes avec de vrais utilisateurs
- Valider les flux de navigation
- Ajuster selon les retours

### 4. Spécifications techniques
- Documenter les composants réutilisables
- Définir les APIs nécessaires
- Planifier l'implémentation

---

## 🛠️ Outils et technologies

### PlantUML Salt
- Langage : PlantUML avec syntaxe Salt (wireframes)
- Avantages :
  - Cohérent avec le reste du projet
  - Versionnable (texte)
  - Rapide à modifier
  - Gratuit et open-source

### Visualisation
- Extension VS Code : PlantUML
- En ligne : plantuml.com
- Export : PNG, SVG, PDF

---

**Auteur :** Prototypes IHM - Projet SI  
**Date :** 11 janvier 2026  
**Version :** 1.0  
**Total d'écrans :** 15 écrans + 1 diagramme de navigation
