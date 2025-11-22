# Apply Filters to SQL Queries  
Projet issu du Google Cybersecurity Professional Certificate

## Objectif du projet
Ce projet a été réalisé dans le cadre du **Google Cybersecurity Professional Certificate**.  
Il consistait à utiliser des requêtes SQL filtrées pour enquêter sur plusieurs événements de sécurité :  
- tentatives de connexion potentiellement malveillantes  
- activité anormale après les heures de bureau  
- accès depuis des pays inattendus  
- identification des employés nécessitant une mise à jour de sécurité  

L’objectif principal était d’utiliser SQL pour extraire rapidement des informations pertinentes d’un système d’authentification lors d’une investigation.

---

## Résumé exécutif
À l’aide de filtres SQL (`WHERE`, `AND`, `OR`, `NOT`, `LIKE`), plusieurs scénarios ont été analysés, notamment :
- des tentatives de connexion échouées après 18h00  
- une activité suspecte sur des dates spécifiques  
- des connexions depuis l’extérieur du pays attendu  
- l’identification de groupes d’employés ciblés pour des mises à jour de sécurité  

Ces requêtes permettent à un analyste SOC de trier efficacement des logs d’authentification pour repérer des comportements anormaux ou orienter une réponse à incident.

---

## Compétences développées
- Analyse d’événements de sécurité via SQL  
- Filtrage logique avec `AND`, `OR`, `NOT`  
- Détection d’activités suspectes basées sur dates, heures, résultats et emplacements  
- Utilisation de `LIKE` pour rechercher des modèles spécifiques  
- Interprétation de logs d’authentification dans un contexte d’enquête  
- Production de requêtes réutilisables pour une investigation SOC

---

## Outils et technologies
- **SQL** (requêtes de filtrage avancé)  
- Base de données d’authentification (tables `log_in_attempts` et `employees`)  
- Analyse de logs dans un contexte de sécurité  

---

## Méthodologie utilisée

### 1. Tentatives de connexion échouées après 18h  
Objectif : identifier un incident après les heures de bureau.  
Techniques utilisées :
```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;
```
Cette requête filtre toutes les authentifications ratées après 18h00, révélant de possibles tentatives malveillantes.

---

### 2. Connexions sur deux dates précises  
Scénario : un incident suspect détecté le 2022-05-09.  
SQL utilisé :
```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```
Cela permet d’étendre l’enquête à la veille de l’incident pour observer un éventuel pattern.

---

### 3. Connexions depuis un pays inattendu  
Objectif : détecter des accès hors du périmètre géographique autorisé.  
```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```
Cette requête retourne tous les accès provenant de l’extérieur du Mexique (MEX ou MEXICO).

---

### 4. Identification des employés ciblés pour une mise à jour de sécurité  
#### Marketing – Bâtiment Est
```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

#### Finance ou Ventes
```sql
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';
```

#### Tous les employés non-IT
```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

Ces filtrages permettent de préparer des mises à jour logicielles segmentées, essentielles en cybersécurité.

---

## Analyse & Apports SOC
Ce projet montre comment SQL peut devenir un outil essentiel pour :
- isoler rapidement des **indicateurs d’activité anormale**  
- obtenir des réponses immédiates lors d’une **analyse d’incident**  
- supporter une démarche structurée de threat hunting  
- corréler des données d’authentification pour identifier des tendances  

Toutes ces compétences s’alignent directement sur les responsabilités réelles d’un **SOC Analyst niveau 1**.

---

## Résultats
- Identification des tentatives de connexion suspectes  
- Détection des accès hors périmètre géographique  
- Filtrage rapide des incidents selon date et succès/échec  
- Identification des groupes d’employés nécessitant action ou investigation  
- Amélioration de la visibilité sur les logs d’authentification

---


## Conclusion
Ce projet démontre une approche analytique rigoureuse, centrée sur l’utilisation de SQL pour conduire des investigations basées sur les logs.  
Il illustre parfaitement la capacité à extraire les informations pertinentes lors d’un potentiel incident de sécurité — une compétence clé dans les métiers de la cybersécurité.
