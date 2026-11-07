# 🔵⬜ **01 CLUB** ⬜🔵

## **FORMATION GIT – SÉANCE 1**

### **Sauvegarder son travail en local**

> 💙 *Aucun prérequis. On apprend pas à pas, avec des exemples simples.*

---

## 🟦 **PLAN DE LA SÉANCE**

| ⬜ | **Partie** | **Contenu** |
|---|---|---|
| 🔵 | **1** | La problématique : pourquoi Git existe |
| 🔵 | **2** | C’est quoi Git ? |
| 🔵 | **3** | La configuration |
| 🔵 | **4** | Les 3 zones de Git |
| 🔵 | **5** | Les premières commandes |
| 🔵 | **6** | Consulter l’historique |
| 🔵 | **7** | Exercice pratique |
| 🔵 | **8** | Conclusion |

---

# 🔵 **PARTIE 1 – LA PROBLÉMATIQUE**

## **Pourquoi Git existe-t-il ?**

### 🔷 **Question pour la salle**

> **« Comment gardez-vous les anciennes versions d’un travail ? »**

### 🟦 **Exemple : le chaos des versions**

- `rapport.docx`
- `rapport_final.docx`
- `rapport_final_vrai.docx`
- `rapport_final_vrai_corrige_V3.docx`

👉 **On ne sait plus quelle version est la bonne, ni ce qui a changé entre deux.**

### 🔷 **Quand on travaille à plusieurs, ça se complique**

| ⬜ | **Problème** | **Conséquence** |
|---|---|---|
| 1 | **Écrasement** | Deux personnes modifient le même fichier, l’une efface le travail de l’autre |
| 2 | **Pas d’historique** | On ne sait pas qui a changé quoi, quand et pourquoi |
| 3 | **Pas de retour en arrière** | Impossible de revenir à la version qui marchait |
| 4 | **Tester est risqué** | On a peur de casser le projet |

### 🟦 **La petite histoire de Git**

En **2005**, **Linus Torvalds**, le créateur de Linux, avait besoin d’un outil pour que **des milliers de développeurs** travaillent ensemble sur le même projet.

L’outil qu’ils utilisaient est devenu indisponible, alors il a créé **Git** en quelques semaines.

Ses objectifs :

- 🔵 **Rapide**
- 🔵 **Fiable**
- 🔵 **Chacun peut travailler en parallèle**

### 💙 **À RETENIR**

> **Le problème : trop de versions, aucun historique, du travail écrasé.**
> **La solution : Git.**

---

# 🔵 **PARTIE 2 – C’EST QUOI GIT ?**

## **Définition simple**

> 💙 **Git est un outil qui enregistre l’historique de ton projet, et qui permet à plusieurs personnes de travailler ensemble sans s’écraser ou Logiciel de gestion de versions qui permet de suivre les modifications d'un projet et de conserver son historique localement.**

### 🟦 **Exemple : écrire un devoir à plusieurs**

| ⬜ | **Étape** | **Ce qui se passe** |
|---|---|---|
| 1 | **Introduction** | Tu l’écris, puis tu sauvegardes : *« Ajout de l’introduction »* (un **commit**) |
| 2 | **Chapitre 1** | Nouvelle sauvegarde : *« Ajout du chapitre 1 »* |
| 3 | **Retour en arrière** | Le chapitre 1 est mauvais : tu reviens à la sauvegarde précédente en un instant |
| 4 | **Branche** | Ton camarade teste une autre conclusion sans toucher à ta version (une **copie parallèle**) |
| 5 | **Fusion** | Sa conclusion est bonne : vous la **fusionnez** avec la version principale |

✅ Un même fichier, tout l’historique, **sans** `_final_vrai_V3`.

> ⬜ *Aujourd’hui : étapes 1 et 2 (sauvegarder). Les étapes 3 à 5 viendront à la séance 2.*

### 🔷 **Git ou GitHub ?**

- 🔵 **Git** : l’outil installé sur **ton ordinateur**, qui garde l’historique.
- ⬜ **GitHub** : Plateforme en ligne qui permet d'héberger des dépôts Git, de partager des projets et de collaborer avec d'autres développeurs. *(séance 2)*.

### 💙 **À RETENIR**

> **Git remplace les copies de fichiers par un historique propre et organisé.**

---

# 🔵 **PARTIE 3 – LA CONFIGURATION**

## **Dire à Git qui tu es**

### 🟦 **Exemple**

Quand tu rends un devoir, tu écris **ton nom** dessus. Git fait pareil : chaque sauvegarde est **signée** avec un nom et un email. On le règle **une seule fois**.

### 🔷 **Étape 1 : vérifier que Git est installé**

```
git --version
```

✅ **Pourquoi :** on s’assure que l’outil existe. Un numéro de version s’affiche : c’est bon.

### 🔷 **Étape 2 : donner son nom et son email**

```
git config --global user.name "Marie Dupont"
git config --global user.email "marie@exemple.com"
```

✅ **Pourquoi :** chaque commit garde en mémoire **qui** a fait la modification.

✅ **Pourquoi le même email que GitHub :** GitHub relie les commits à ton compte grâce à l’email.

❌ **À ne pas faire :**

- Oublier les **guillemets** quand le nom contient un espace
- Mettre un **faux email** : tes commits ne seront reliés à personne
- Mettre un **mot de passe** : ce n’est jamais nécessaire ici

### 🔷 **Étape 3 : comprendre `--global`**

| ⬜ | **Option** | **Effet** |
|---|---|---|
| 🔵 | **Avec `--global`** | Le réglage s’applique à **tous** tes projets (une seule fois) |
| 🔵 | **Sans `--global`** | Le réglage s’applique à **ce projet seulement** |

✅ **Pourquoi `--global` pour commencer :** on ne refait pas la configuration à chaque projet.

### 🔷 **Étape 4 : vérifier**

```
git config user.name
git config user.email
```

✅ **Pourquoi :** une faute de frappe est vite arrivée. Mieux vaut le voir **maintenant** qu’au premier commit.

### 🔷 **Étape 5 (optionnelle) : la branche principale**

```
git config --global init.defaultBranch main
```

✅ **Pourquoi :** GitHub utilise `main`. On évite une confusion plus tard.

### 💙 **À RETENIR**

> **Configurer Git, c’est signer son travail une seule fois.**

---

# 🔵 **PARTIE 4 – LES 3 ZONES DE GIT**

## **La notion la plus importante**

### 🔷 **Les 3 zones**

| ⬜ | **Zone** | **C’est quoi ?** | **Commande** |
|---|---|---|---|
| 1 | **Dossier de travail(Working Directory)** |  Les fichiers de ton projet que tu consultes et modifies. | |
| 2 | **Staging** (préparation) | Ce que tu as choisi de sauvegarder.Une zone gérée par Git stockée dans .git/index | `git add` |
| 3 | **Dépôt local** | L’historique des sauvegardes sur ton ordinateur dans .git/objects | `git commit` |



<h2 style="color:#2563EB; border-bottom:2px solid #2563EB; padding-bottom:8px;">
   Le schéma à mémoriser
</h2>

<div align="center">

<div style="background:#EFF6FF; border:2px solid #3B82F6; border-radius:12px; padding:16px; margin:10px 0; max-width:500px;">
  <h3 style="color:#1D4ED8; margin:0;">01 · WORKING DIRECTORY</h3>
  <p style="color:#1E3A8A; margin:8px 0 0;">Tu modifies tes fichiers</p>
</div>

<div style="color:#2563EB; font-size:14px; font-weight:bold;">↓ git add</div>

<div style="background:#FFFFFF; border:2px solid #60A5FA; border-radius:12px; padding:16px; margin:10px 0; max-width:500px;">
  <h3 style="color:#2563EB; margin:0;">02 · STAGING AREA</h3>
  <p style="color:#334155; margin:8px 0 0;">Tu sélectionnes les modifications à enregistrer</p>
</div>

<div style="color:#2563EB; font-size:14px; font-weight:bold;">↓ git commit</div>

<div style="background:#EFF6FF; border:2px solid #3B82F6; border-radius:12px; padding:16px; margin:10px 0; max-width:500px;">
  <h3 style="color:#1D4ED8; margin:0;">03 · LOCAL REPOSITORY</h3>
  <p style="color:#1E3A8A; margin:8px 0 0;">📁 .git</p>
  <p style="color:#1E3A8A; margin:4px 0 0;">Git conserve les commits localement</p>
</div>

<div style="color:#2563EB; font-size:14px; font-weight:bold;">↓ git push</div>

<div style="background:#FFFFFF; border:2px solid #60A5FA; border-radius:12px; padding:16px; margin:10px 0; max-width:500px;">
  <h3 style="color:#2563EB; margin:0;">04 · REMOTE REPOSITORY</h3>
  <p style="color:#334155; margin:8px 0 0;">☁️ GitHub</p>
  <p style="color:#334155; margin:4px 0 0;">Le projet est partagé en ligne</p>
</div>

</div>



### ✅ **Pourquoi le staging existe**

Tu peux avoir modifié **5 fichiers** et n’en sauvegarder que **2**, ceux qui vont ensemble. Sans le staging, tu sauvegarderais tout, même ce qui n’est pas fini.

### ⚠️ **Attention**

> Le **dépôt distant (GitHub)** n’est **pas** une des 3 zones : c’est un **quatrième endroit**.
> **`commit`** reste sur ton ordinateur. **`push`** (séance 2) envoie vers GitHub.

### 💙 **À RETENIR**

> **Modifier → préparer (`add`) → sauvegarder (`commit`).**

---

# 🔵 **PARTIE 5 – LES PREMIÈRES COMMANDES**

## **Fil rouge : un devoir dans un dossier `mon-devoir`**

### 🔷 **Commande 1 : `git init`**

```
cd mon-devoir
git init
```

- 🔷 **Ce que ça fait :** Git crée un dossier caché `.git` qui contiendra tout l’historique.
- 🟦 **Exemple :** acheter un **classeur vide** pour son projet.
- ✅ **Pourquoi :** sans `git init`, Git ne surveille rien.

❌ **À ne pas faire :**

- Le faire **plusieurs fois** : une seule fois par projet
- Le faire dans un dossier **trop large** (Bureau, Documents) : Git suivrait des centaines de fichiers sans rapport
- Le faire dans un dossier qui est **déjà** un dépôt Git

---

### 🔷 **Commande 2 : `git status`**

```
git status
```

- 🔷 **Ce que ça fait :** Git explique quels fichiers sont nouveaux, modifiés ou prêts à être sauvegardés.
- 🟦 **Exemple :** regarder son **bureau avant de ranger**.
- ✅ **Pourquoi :** c’est la commande de **sécurité**. Elle ne modifie rien, donc **zéro risque**.

💙 **Conseil :** taper `git status` **avant et après** chaque autre commande.

---

### 🔷 **Commande 3 : `git add`**

```
git add intro.txt
```

- 🔷 **Ce que ça fait :** Git met `intro.txt` dans la **zone de préparation**.
- 🟦 **Exemple :** préparer sa **valise** : on choisit ce qu’on met dedans, mais on ne l’a pas encore fermée.
- ✅ **Pourquoi :** on **choisit** quelles modifications vont ensemble pour faire un commit propre.

| ⬜ | **Commande** | **Effet** | **Conseil** |
|---|---|---|---|
| 🔵 | `git add intro.txt` | Un fichier précis | ✅ **Recommandé au début** |
| 🔵 | `git add .` | Tout ce qui a changé | ⚠️ À utiliser avec attention |

❌ **À ne pas faire :**

- Croire que `git add` **sauvegarde** : **rien n’est encore dans l’historique**
- Faire `git add .` sans avoir regardé `git status`

---

### 🔷 **Commande 4 : `git commit`**

```
git commit -m "Ajout de l'introduction"
```

- 🔷 **Ce que ça fait :** Git enregistre une version avec ton message. C’est ton **point de sauvegarde**.
- 🟦 **Exemple :** fermer la valise et mettre une **étiquette** : « valise vacances été ».
- ✅ **Pourquoi le message compte :** dans 3 mois, personne ne se souviendra de ce que tu as fait.

| ❌ **À éviter** | ✅ **À faire** |
|---|---|
| `"truc"` | `"Ajout de l'introduction"` |
| `"modif"` | `"Correction des fautes dans le chapitre 1"` |
| `"final"` | `"Ajout de la conclusion"` |

💙 **Règle simple :** le message répond à *« qu’est-ce que j’ai fait dans cette sauvegarde ? »*

❌ **À ne pas faire :**

- Un **énorme commit** avec 3 jours de travail : plusieurs petits commits valent mieux
- **Oublier `-m "..."`** : Git ouvre un éditeur (`vim`) qui bloque beaucoup de débutants

---

### 🔷 **Le cycle complet**

```
git init
git status
git add intro.txt
git status
git commit -m "Ajout de l'introduction"
git status
git log
```

> `git status` change à chaque étape : **fichier non suivi → prêt à sauvegarder → tout propre**.

### 💙 **À RETENIR**

> **On modifie, on prépare avec `add`, on sauvegarde avec `commit`, on vérifie avec `status`.**

---

# 🔵 **PARTIE 6 – CONSULTER L’HISTORIQUE**

## **Fil rouge : `mon-devoir` avec 2 commits déjà faits**

- ❓ *« Qu’est-ce que j’ai sauvegardé ? »* → **`git log`**
- ❓ *« Qu’est-ce que j’ai changé depuis ? »* → **`git diff`**

### 🔷 **`git log` : lire l’historique**

```
git log --oneline
```

- 🔷 **Ce que ça fait :** liste les commits, du plus récent au plus ancien (auteur, date, message).
- 🟦 **Exemple :** le **journal de bord** du projet : *« lundi, Marie a ajouté l’introduction ; mardi, Marie a ajouté le chapitre 1 »*.
- ✅ **Pourquoi :** retrouver ce qui a été fait, par qui, et quand.
- 🔷 **Identifiant du commit :** une suite de lettres et chiffres (ex. `a1b2c3d`), comme un **numéro de suivi de colis**.

⚠️ **Astuce :** si l’affichage reste ouvert, appuyer sur **`q`** pour quitter.

### 🔷 **`git diff` : voir ce qui a changé**

```
git diff
```

- 🔷 **Ce que ça fait :** compare ton fichier actuel à la dernière sauvegarde.
- 🟦 **Exemple :** tu ajoutes une phrase à `intro.txt`, et Git montre :

```
+ Cette phrase est nouvelle.
```

| ⬜ | **Symbole** | **Signification** |
|---|---|---|
| 🔵 | **`+`** (vert) | Ligne **ajoutée** |
| 🔵 | **`-`** (rouge) | Ligne **supprimée** |

✅ **Pourquoi avant `git add` :** c’est ta **relecture**. Tu vérifies ce que tu vas sauvegarder.

### ⚠️ **Le piège classique**

Après `git add`, `git diff` **n’affiche plus rien** : le fichier est déjà dans le staging. Pour voir ce qui est prêt à partir :

```
git diff --staged
```

| ⬜ | **Je veux voir…** | **Commande** |
|---|---|---|
| 🔵 | Ce que j’ai modifié, **pas encore ajouté** | `git diff` |
| 🔵 | Ce qui sera dans **le prochain commit** | `git diff --staged` |
| 🔵 | Les commits **déjà faits** | `git log --oneline` |

### 🔷 **Le cycle complet**

```
(modifier intro.txt)
git status          → je vois que le fichier a changé
git diff            → je vois exactement ce qui a changé
git add intro.txt   → je prépare
git diff --staged   → je vérifie ce qui va partir
git commit -m "Ajout d'une phrase dans l'introduction"
git log --oneline   → je vois ma nouvelle sauvegarde
```

### 💙 **À RETENIR**

> **`git log` montre ce qui a été sauvegardé. `git diff` montre ce qui a changé depuis. Aucune des deux ne modifie quoi que ce soit.**

---

# 🔵 **PARTIE 7 – EXERCICE PRATIQUE**

## **À vous de jouer**

1. 🔵 Créer un dossier `mon-devoir`, entrer dedans, faire `git init`
2. 🔵 Vérifier avec `git config user.name` et `git config user.email`
3. 🔵 Créer `intro.txt`, puis `git status`, `git add intro.txt`, `git commit -m "Ajout de l'introduction"`
4. 🔵 Créer `chapitre1.txt`, puis `git add chapitre1.txt` et `git commit -m "Ajout du chapitre 1"`
5. 🔵 Modifier `intro.txt`, faire `git diff` et repérer le `+`
6. 🔵 Faire `git add intro.txt`, `git diff --staged`, puis le commit
7. 🔵 Terminer par `git log --oneline` : on doit voir **3 commits**

### 🟦 **Je vérifie que j’ai compris**

- ❓ Pourquoi Git plutôt que `rapport_final_vrai_V3.docx` ?
- ❓ Quelles sont les **3 zones** ? Quelle commande passe de l’une à l’autre ?
- ❓ Pourquoi `git add` ne sauvegarde-t-il pas encore ?
- ❓ Quelle différence entre `git diff` et `git log` ?

---

# 🔵 **RÉCAPITULATIF DES COMMANDES**

| ⬜ | **Commande** | **À quoi elle sert** |
|---|---|---|
| 🔵 | `git --version` | Vérifier que Git est installé |
| 🔵 | `git config --global user.name "..."` | Donner son nom (une fois) |
| 🔵 | `git config --global user.email "..."` | Donner son email (une fois) |
| 🔵 | `git init` | Démarrer le suivi dans un dossier de projet |
| 🔵 | `git status` | Voir l’état des fichiers |
| 🔵 | `git add fichier` | Préparer un fichier pour la sauvegarde |
| 🔵 | `git commit -m "message"` | Enregistrer une version |
| 🔵 | `git log --oneline` | Voir l’historique |
| 🔵 | `git diff` | Voir les modifications pas encore ajoutées |
| 🔵 | `git diff --staged` | Voir ce qui sera dans le prochain commit |

---

# 🔵 **PARTIE 8 – CONCLUSION**

## **Ce qu’on a appris aujourd’hui**

| ⬜ | **Question** | **Réponse** |
|---|---|---|
| 🔵 | **Pourquoi Git ?** | Fini les versions en désordre et le travail écrasé |
| 🔵 | **C’est quoi ?** | Un historique de sauvegardes, comme dans un jeu vidéo |
| 🔵 | **Comment commencer ?** | Configurer son nom et son email, une seule fois |
| 🔵 | **Comment ça marche ?** | 3 zones : dossier de travail → staging → dépôt local |
| 🔵 | **Comment sauvegarder ?** | `git add` puis `git commit` |
| 🔵 | **Comment relire ?** | `git log` et `git diff` |

### 💙 **LA PHRASE À RETENIR**

> **Git remplace les copies de fichiers par un historique propre et organisé.**

### 🔷 **À la séance 2**

- 🔵 **Revenir en arrière** (annuler une erreur)
- 🔵 **Les branches** et la fusion
- 🔵 **GitHub** : `clone`, `push`, `pull`
- 🔵 **Les conflits**
- 🔵 **Exercice final en binôme**

---

## 🔵⬜ **MERCI !** ⬜🔵


### **01 CLUB** · *Formation Git – Séance 1*
💙**Cours réalisé et présenté par:** 💙
## 🔵⬜ **Oumayma Bouchnaf** ⬜🔵
> 💙 **Des questions ? C’est le moment !**