# 🔵⬜ **01 CLUB** ⬜🔵

## **FORMATION GIT – SÉANCE 2**

### **Revenir en arrière et travailler avec les autres**

> 💙 *Dernière séance : on passe de « je sauvegarde seul » à « je travaille en équipe ».*

---

## 🟦 **PLAN DE LA SÉANCE**

| ⬜ | **Partie** | **Contenu** |
|---|---|---|
| 🔵 | **0** | Rappel de la séance 1 |
| 🔵 | **1** | Revenir en arrière |
| 🔵 | **2** | Les branches |
| 🔵 | **3** | GitHub : `clone`, `push`, `pull` |
| 🔵 | **4** | Les conflits |
| 🔵 | **5** | Exercice final en binôme |
| 🔵 | **6** | Conclusion |

---

# 🔵 **PARTIE 0 – RAPPEL DE LA SÉANCE 1**

## **Ce qu’on sait déjà faire**

### 🔷 **Les 3 zones**

```
Dossier de travail  --git add-->  Staging  --git commit-->  Dépôt local
```

### 🔷 **Les commandes vues**

| ⬜ | **Commande** | **À quoi elle sert** |
|---|---|---|
| 🔵 | `git init` | Démarrer le suivi dans un dossier |
| 🔵 | `git status` | Voir l’état des fichiers |
| 🔵 | `git add fichier` | Préparer pour la sauvegarde |
| 🔵 | `git commit -m "..."` | Enregistrer une version |
| 🔵 | `git log --oneline` | Voir l’historique |
| 🔵 | `git diff` / `git diff --staged` | Voir ce qui a changé |

### 🟦 **Questions pour la salle**

- ❓ Quelle commande fait passer un fichier du dossier de travail au staging ?
- ❓ Pourquoi `git diff` n’affiche-t-il plus rien après `git add` ?
- ❓ Le dépôt distant (GitHub) fait-il partie des 3 zones ?

> 💙 **Réponse à la dernière :** non, c’est un **quatrième endroit**. On le découvre aujourd’hui.

---

# 🔵 **PARTIE 1 – REVENIR EN ARRIÈRE**

## **Annuler une erreur sans panique**

### 🟦 **Exemple : on reprend le devoir**

À la séance 1, on disait : *« le chapitre 1 est mauvais, je reviens à la sauvegarde précédente. »* Voyons comment.

### 🔷 **L’idée clé : une annulation pour chaque zone**

| ⬜ | **Où est l’erreur ?** | **Situation** | **Commande** |
|---|---|---|---|
| 1 | **Dossier de travail** | J’ai modifié un fichier et je veux tout annuler | `git restore fichier` |
| 2 | **Staging** | J’ai fait `git add` par erreur | `git restore --staged fichier` |
| 3 | **Dépôt local** | J’ai déjà fait le commit | `git revert` |

> 💙 **Avant d’annuler : dans quelle zone est mon erreur ?** `git status` te le dit.

---

### 🔷 **Commande 1 : `git restore fichier`**

```
git restore chapitre1.txt
```

- 🔷 **Ce que ça fait :** le fichier revient tel qu’il était à la **dernière sauvegarde**.
- 🟦 **Exemple :** tu as barbouillé ton brouillon, tu reprends la dernière version propre.
- ✅ **Pourquoi :** annuler un essai raté sans rien casser.

⚠️ **Attention : c’est la seule commande dangereuse de cette partie.** Les modifications annulées sont **perdues définitivement**, car Git ne les avait jamais sauvegardées.

❌ **À ne pas faire :** l’utiliser « pour voir ce que ça fait ». Toujours faire `git diff` avant, pour voir ce qu’on va perdre.

---

### 🔷 **Commande 2 : `git restore --staged fichier`**

```
git restore --staged chapitre1.txt
```

- 🔷 **Ce que ça fait :** le fichier sort du staging, mais **tes modifications restent** dans le fichier.
- 🟦 **Exemple :** tu ressors un objet de la valise, mais il reste sur ton bureau, intact.
- ✅ **Pourquoi :** corriger un `git add` fait trop vite (par exemple un `git add .` qui a pris un brouillon).
- ✅ **Sans danger :** aucun travail n’est perdu, on change seulement de zone.

---

### 🔷 **Commande 3 : `git revert`**

```
git log --oneline
git revert --no-edit a1b2c3d
```

*(`a1b2c3d` : l’identifiant du commit à annuler, vu avec `git log --oneline`.)*

- 🔷 **Ce que ça fait :** Git crée un **nouveau commit** qui fait l’inverse du commit choisi.
- 🟦 **Exemple :** tu as sauvegardé « Ajout du chapitre 1 », mais il est mauvais. Git ne l’efface pas : il ajoute une sauvegarde *« Revert : Ajout du chapitre 1 »* qui annule son effet.
- ✅ **Pourquoi :** l’historique reste **honnête et complet**. On voit l’erreur **et** sa correction. Indispensable quand plusieurs personnes travaillent ensemble.
- ✅ **Pourquoi `--no-edit` :** sans lui, Git ouvre l’éditeur `vim` qui bloque beaucoup de débutants.

**Pour annuler le dernier commit :**

```
git revert --no-edit HEAD
```

`HEAD` veut simplement dire « le commit le plus récent ».

**Avant / après avec `git log --oneline` :**

```
c3d4e5f Revert "Ajout du chapitre 1"
b2c3d4e Ajout du chapitre 1
a1b2c3d Ajout de l'introduction
```

### ⚠️ **Et `git reset` ?**

Tu en entendras parler : cette commande **efface** des commits de l’historique. Si d’autres les ont déjà récupérés, ça crée de gros problèmes.

> 💙 **Règle simple : pour annuler un commit, on utilise `revert`.**

### 💙 **À RETENIR**

> **Chaque zone a sa commande d’annulation : `restore` (dossier de travail), `restore --staged` (staging), `revert` (commit déjà fait).**

---

# 🔵 **PARTIE 2 – LES BRANCHES**

## **Tester sans risque**

### 🟦 **Exemple : la conclusion du camarade**

Ton camarade veut tester une autre conclusion **sans toucher à ta version**. Il prend **une photocopie** du cahier, essaie ses idées dessus, et si c’est bon, on **recopie** sa conclusion dans le cahier d’origine.

### 🔷 **L’idée clé**

> 💙 **Une branche est une copie parallèle du projet.** Si ça rate, la version principale n’a rien senti.

La branche principale s’appelle **`main`**. En séance 1, on travaillait toujours dessus.

---

### 🔷 **Commande 1 : `git branch`**

```
git branch
```

```
* main
```

- 🔷 **Ce que ça fait :** liste les branches. L’étoile `*` marque celle où tu te trouves.

✅ **Règle de nommage :**

| ✅ **À faire** | ❌ **À éviter** |
|---|---|
| `conclusion-camarade` | `conclusion camarade` *(pas d’espaces)* |
| Un nom clair, avec des tirets | `test`, `truc` |

---

### 🔷 **Commande 2 : `git switch`**

```
git switch -c conclusion-camarade
```

- 🔷 **Ce que ça fait :** crée la branche **et** s’y place (`-c` veut dire « create »).
- 🟦 **Exemple :** tu poses ton cahier d’origine et tu prends la photocopie.
- ✅ **Pourquoi :** créer une branche ne suffit pas, il faut **aller dessus** pour y travailler.

Pour changer de branche ensuite :

```
git switch main
```

### 🔷 **Le moment « waouh »**

1. Sur la branche `conclusion-camarade`, créer `conclusion.txt` et faire un commit.
2. Revenir sur `main` avec `git switch main`.
3. Regarder le dossier : **`conclusion.txt` a disparu !**
4. Revenir sur la branche : il est de retour.

> 💙 **Chaque branche a son propre contenu.**

💙 **Pour savoir où l’on est :** `git status` affiche `On branch ...` en première ligne.

---

### 🔷 **Commande 3 : `git merge`**

```
git switch main
git merge conclusion-camarade
```

- 🔷 **Ce que ça fait :** ramène dans `main` le travail fait sur `conclusion-camarade`.
- 🟦 **Exemple :** on recopie la bonne conclusion de la photocopie dans le cahier d’origine.

⚠️ **Le point qui trompe les débutants :** **on se place d’abord sur la branche qui reçoit.**

> 💙 **`git merge X` veut dire : « ramène X ici, là où je suis ».**

💡 Si Git ouvre `vim` pendant la fusion : `git merge --no-edit conclusion-camarade`.

---

### 🔷 **Commande 4 : `git branch -d`**

```
git branch -d conclusion-camarade
```

- 🔷 **Ce que ça fait :** supprime la branche **une fois fusionnée**.
- ✅ **Pourquoi :** garder un projet propre.
- ✅ **Sans danger :** `-d` (petit d) **refuse** de supprimer une branche non fusionnée.

❌ **À ne pas faire :** utiliser `-D` (grand D) : il **force** la suppression, même sans fusion, et on peut perdre du travail.

### 🔷 **Pourquoi des branches ?**

| ❌ **Sans branche** | ✅ **Avec branche** |
|---|---|
| On teste directement sur la version principale | On teste sur une copie, la version principale reste intacte |
| Si ça rate, il faut annuler | Si ça rate, on supprime la branche |
| À plusieurs, on se gêne | Chacun travaille sur sa branche |

### 🔷 **Le cycle complet**

```
git switch -c conclusion-camarade   → je crée la branche et j'y vais
(créer conclusion.txt)
git add conclusion.txt
git commit -m "Ajout de la conclusion"
git switch main                     → je reviens sur la version principale
git merge conclusion-camarade       → je ramène la conclusion dans main
git branch -d conclusion-camarade   → je range
```

> 💙 **Bonne habitude : faire un commit avant de changer de branche.**

### 💙 **À RETENIR**

> **Une branche est une copie parallèle : on la crée avec `switch -c`, on se place sur `main`, puis on fusionne avec `merge`.**

---

# 🔵 **PARTIE 3 – GITHUB**

## **Partager son travail**

### 🟦 **Exemple : le bureau de poste**

Ton colis (tes commits) est rangé chez toi. Pour que ton camarade le récupère, tu l’**envoies** au bureau de poste, et lui va le **chercher**.

### 🔷 **L’idée clé**

> 💙 **GitHub est un site web qui garde une copie de ton projet en ligne, pour le partager et le sauvegarder.**

| ⬜ | **Commande** | **Direction** | **Image du colis** |
|---|---|---|---|
| 🔵 | `git commit` | dossier → **dépôt local** | Fermer le colis, chez toi |
| 🔵 | `git push` | **dépôt local → GitHub** | Déposer le colis au bureau de poste |
| 🔵 | `git pull` | **GitHub → dépôt local** | Aller chercher les colis des autres |
| 🔵 | `git clone` | **GitHub → nouveau dossier** | Récupérer le colis complet la première fois |

> ⚠️ **`commit` reste chez toi. Rien n’est partagé tant que tu n’as pas fait `push`.**

### 🔷 **Avant de commencer**

1. 🔵 Avoir un **compte GitHub**.
2. 🔵 Créer un **dépôt vide** sur GitHub (bouton **New repository**), **sans** cocher « Add a README ».
3. 🔵 Avoir un moyen de se connecter : GitHub n’accepte plus le mot de passe habituel pour envoyer du code. Il demande un **jeton d’accès** ou un outil de connexion intégré.

### 🔷 **Un réglage à faire une seule fois**

```
git config --global pull.rebase false
```

✅ **Pourquoi :** quand ton historique et celui de GitHub ont chacun avancé de leur côté, ce réglage dit à Git de **les fusionner** au moment du `pull`. Sans lui, les versions récentes de Git peuvent s’arrêter en demandant comment faire.

---

### 🔷 **Commande 1 : `git remote add`**

```
git remote add origin https://github.com/marie/mon-devoir.git
git remote -v
```

- 🔷 **Ce que ça fait :** tu donnes à Git l’**adresse** du bureau de poste.
- 🟦 **Exemple :** enregistrer un contact dans ton téléphone. `origin` est simplement le **nom** du contact.
- ✅ **Pourquoi `git remote -v` :** pour vérifier l’adresse avant l’envoi.

❌ **À ne pas faire :** recopier l’adresse de mémoire. Toujours la **copier-coller** depuis le bouton vert **Code** de GitHub.

---

### 🔷 **Commande 2 : `git push`**

```
git push -u origin main
```

- 🔷 **Ce que ça fait :** tes commits partent de ton ordinateur vers GitHub.
- 🟦 **Exemple :** tu déposes ton colis au bureau de poste.
- ✅ **Pourquoi `-u` :** il dit à Git *« retiens que `main` va avec `origin` »*. On ne le met **qu’une fois** : ensuite, `git push` suffit.

💡 **Si Git dit que `main` n’existe pas :** la branche s’appelle peut-être `master`. On la renomme avec `git branch -M main`.

❌ **À ne pas faire :**

- Envoyer des **mots de passe, clés ou fichiers personnels** : une fois sur GitHub, c’est visible (surtout si le dépôt est public), et même supprimé plus tard, ça reste dans l’historique.
- Faire `push` **sans avoir fait `commit`** : il n’y a rien de nouveau à envoyer.

---

### 🔷 **Commande 3 : `git clone`**

```
git clone https://github.com/marie/mon-devoir.git
```

- 🔷 **Ce que ça fait :** crée un **nouveau dossier** avec tout le projet **et son historique**, déjà relié à GitHub.
- 🟦 **Exemple :** ton camarade récupère le colis complet pour la première fois.
- ✅ **Pourquoi pas `git init` :** avec `clone`, tout est déjà en place, y compris `origin`.

❌ **À ne pas faire :** cloner **à l’intérieur** d’un dossier qui est déjà un dépôt Git.

---

### 🔷 **Commande 4 : `git pull`**

```
git pull
```

- 🔷 **Ce que ça fait :** Git va chercher les nouveautés sur GitHub et les **ajoute** à ton projet.
- 🟦 **Exemple :** tu passes au bureau de poste récupérer les colis arrivés pour toi.
- ✅ **Pourquoi :** pour **être à jour** avant de travailler.

### 🔷 **Les 2 bonnes habitudes**

1. 🔵 **`git pull` avant de commencer à travailler**
2. 🔵 **`git pull` avant chaque `git push`**

### ⚠️ **Le message d’erreur classique**

```
! [rejected]  main -> main (fetch first)
```

- **Ce que ça veut dire :** quelqu’un a envoyé du travail que tu n’as pas encore.
- **Solution :** `git pull`, puis `git push` à nouveau.

> 💙 **Ce n’est pas une panne : c’est Git qui te protège.**

### 🔷 **Le cycle complet**

**Côté Marie :**

```
git remote add origin https://github.com/marie/mon-devoir.git
git push -u origin main
```

**Côté son camarade :**

```
git clone https://github.com/marie/mon-devoir.git
(modifier conclusion.txt)
git add conclusion.txt
git commit -m "Ajout de la conclusion"
git push
```

**De retour chez Marie :**

```
git pull
git log --oneline
```

### 💙 **À RETENIR**

> **`commit` sauvegarde chez toi, `push` envoie sur GitHub, `pull` récupère le travail des autres, `clone` copie un projet entier la première fois.**

---

# 🔵 **PARTIE 4 – LES CONFLITS**

## **Quand deux personnes modifient la même ligne**

### 🟦 **Exemple : la même phrase de la conclusion**

Ton camarade et toi écrivez **la même phrase** de la conclusion, chacun à votre façon. Git ne peut pas deviner laquelle garder : c’est un **conflit**.

### 🔷 **L’idée clé**

> 💙 **Un conflit n’est pas une panne. C’est Git qui dit : « Ces deux personnes ont modifié la même ligne, décidez vous-mêmes laquelle garder. »**

**Rien n’est perdu** : Git protège le travail de chacun.

### 🔷 **Quand arrive-t-il ?**

| ⬜ | **Situation** | **Résultat** |
|---|---|---|
| 🔵 | Deux fichiers **différents** modifiés | ✅ Aucun problème |
| 🔵 | Deux endroits **différents** d’un même fichier | ✅ Git fusionne tout seul |
| 🔵 | **La même ligne** | ⚠️ **Conflit** |

Il apparaît pendant un **`git merge`** ou un **`git pull`**.

### 🔷 **Étape 1 : repérer le conflit**

```
CONFLICT (content): Merge conflict in conclusion.txt
Automatic merge failed; fix conflicts and then commit the result.
```

```
git status
```

```
Unmerged paths:
        both modified:   conclusion.txt
```

- ✅ **`both modified`** : les deux côtés ont modifié ce fichier. `git status` te dit **quels fichiers** sont en conflit.

### 🔷 **Étape 2 : lire les marqueurs**

Git écrit **les deux versions** dans le fichier :

```
<<<<<<< HEAD
Conclusion : Git rend le travail plus simple.
=======
Conclusion : le travail en équipe est plus fort.
>>>>>>> conclusion-camarade
```

| ⬜ | **Partie** | **Signification** |
|---|---|---|
| 🔵 | `<<<<<<< HEAD` | **Début** du conflit |
| 🔵 | Au-dessus de `=======` | **Ta version** (la branche où tu es) |
| 🔵 | `=======` | **Séparation** |
| 🔵 | En dessous de `=======` | **L’autre version** |
| 🔵 | `>>>>>>> nom` | **Fin** du conflit |

### 🔷 **Étape 3 : décider et nettoyer**

Trois choix :

1. 🔵 **Garder ta version**
2. 🔵 **Garder l’autre version**
3. 🔵 **Combiner les deux**

```
Conclusion : Git rend le travail plus simple, et le travail en équipe est plus fort.
```

❌ **À ne pas faire :**

- **Laisser les marqueurs** (`<<<<<<<`, `=======`, `>>>>>>>`) dans le fichier : c’est l’erreur n°1. Il faut **les supprimer**.
- Choisir sa version **sans réfléchir** : parle à ton camarade, il a peut-être raison.

### 🔷 **Étape 4 : dire à Git que c’est réglé**

```
git add conclusion.txt
git commit --no-edit
```

- ✅ **Pourquoi `git add` :** ici, il veut dire *« j’ai résolu ce fichier »*.
- ✅ **Pourquoi `--no-edit` :** Git a déjà préparé un message de fusion, et `vim` ne s’ouvre pas.

### 🔷 **Le bouton de secours**

```
git merge --abort
```

> 💙 **Annule la fusion et te ramène exactement à l’état d’avant.** On peut toujours repartir de zéro.

### 🔷 **Le cas fréquent : conflit avec GitHub**

1. 🔵 Marie et son camarade modifient **la même ligne**.
2. 🔵 Marie fait `git push` : ça passe.
3. 🔵 Son camarade fait `git push` : **refusé** (`rejected`).
4. 🔵 Il fait `git pull` : **`CONFLICT`**.
5. 🔵 Il résout le conflit (étapes 1 à 4).
6. 🔵 Il fait `git push` : cette fois, ça passe.

### 🔷 **Comment réduire les conflits**

| ⬜ | **Bonne habitude** | **Pourquoi** |
|---|---|---|
| 🔵 | `git pull` avant de travailler | On part de la dernière version |
| 🔵 | Petits commits, souvent | Les conflits restent petits |
| 🔵 | Se répartir les fichiers | Chacun son fichier |
| 🔵 | Garder les branches courtes | Les versions divergent moins |
| 🔵 | Communiquer | *« Je prends la conclusion, toi l’intro »* |

### 💙 **À RETENIR**

> **Un conflit arrive quand deux personnes modifient la même ligne : on ouvre le fichier, on choisit, on supprime les marqueurs, puis `add` et `commit`. Et `git merge --abort` permet toujours de repartir à zéro.**

---

# 🔵 **PARTIE 5 – EXERCICE FINAL EN BINÔME**

## **Écrire un devoir à deux**

> 💙 **Vous êtes deux : l’étudiant A et l’étudiant B. Vous écrivez le devoir ensemble, comme dans l’exemple du cours.**

### 🔷 **Avant de commencer**

- 🔵 Chacun a un **compte GitHub**.
- 🔵 **A** crée un **dépôt vide** nommé `devoir-01club` (sans README).
- 🔵 **A** invite **B** comme collaborateur : dans le dépôt, **Settings → Collaborators → Add people**. **B** accepte l’invitation.
- 🔵 Chacun a fait `git config --global pull.rebase false`.

> ⚠️ **Sans cette invitation, B ne pourra pas envoyer son travail (`push`).**

---

### 🟦 **NIVEAU 1 – Mettre en place et travailler chacun sa branche**

**Étape 1 – A prépare le projet**

```
git init devoir-01club
cd devoir-01club
(créer intro.txt avec une phrase)
git add intro.txt
git commit -m "Ajout de l'introduction"
git branch -M main
git remote add origin <adresse du dépôt>
git push -u origin main
```

**Étape 2 – B récupère le projet**

```
git clone <adresse du dépôt>
cd devoir-01club
git log --oneline
```

**Étape 3 – Chacun sa branche** *(en même temps)*

| ⬜ | **A** | **B** |
|---|---|---|
| 🔵 | `git switch -c intro-a` | `git switch -c conclusion-b` |
| 🔵 | Ajouter une phrase dans `intro.txt` | Créer `conclusion.txt` avec une phrase |
| 🔵 | `git add intro.txt` | `git add conclusion.txt` |
| 🔵 | `git commit -m "Complément de l'introduction"` | `git commit -m "Ajout de la conclusion"` |

**Étape 4 – A fusionne et envoie**

```
git switch main
git merge --no-edit intro-a
git push
```

**Étape 5 – B se met à jour, fusionne et envoie**

```
git switch main
git pull
git merge --no-edit conclusion-b
git push
```

**Étape 6 – A récupère le travail de B**

```
git pull
git log --oneline
```

> ✅ **Réussi si :** les deux voient `intro.txt` **et** `conclusion.txt`, avec les commits des deux.

---

### 🟦 **NIVEAU 2 – Provoquer et résoudre un conflit**

**Étape 7 – Les deux modifient la même ligne** *(en même temps)*

- 🔵 **A** et **B** modifient la **première ligne** de `intro.txt`, **chacun à sa façon**.
- 🔵 Chacun fait `git add intro.txt` puis `git commit -m "Modification de l'introduction"`.

**Étape 8 – A envoie en premier**

```
git push
```

**Étape 9 – B essaie d’envoyer**

```
git push
```

> ⚠️ **Refusé (`rejected`).** C’est normal.

**Étape 10 – B résout le conflit**

```
git pull
git status
```

1. 🔵 Ouvrir `intro.txt`
2. 🔵 Choisir ou combiner les deux versions
3. 🔵 **Supprimer** les 3 lignes de marqueurs
4. 🔵 Terminer :

```
git add intro.txt
git commit --no-edit
git push
```

**Étape 11 – A récupère**

```
git pull
git log --oneline
```

> ✅ **Réussi si :** le fichier ne contient plus aucun `<<<<<<<` et le même texte apparaît chez les deux.

---

### 🟦 **BONUS – Annuler une erreur**

- 🔵 **A** fait volontairement un commit « raté » (par exemple une phrase absurde dans `conclusion.txt`).
- 🔵 **A** l’annule avec `git revert --no-edit HEAD`, puis fait `git push`.
- 🔵 **B** fait `git pull` et lit `git log --oneline` : il voit le commit **et** son annulation.

---

### 🔷 **Vérifier que j’ai compris**

- ❓ Pourquoi mon `push` a-t-il été **refusé** à l’étape 9 ?
- ❓ Que signifient les lignes entre `<<<<<<<` et `=======` ?
- ❓ Pourquoi `revert` plutôt que `reset` ?
- ❓ Que fait `git pull` que `git push` ne fait pas ?

---

# 🔵 **PARTIE 6 – CONCLUSION**

## **Ce qu’on a appris en 2 séances**

### 🔷 **Le chemin parcouru**

| ⬜ | **Question** | **Réponse** |
|---|---|---|
| 🔵 | **Pourquoi Git ?** | Fini `rapport_final_vrai_V3.docx`, le travail écrasé et l’absence d’historique |
| 🔵 | **Comment sauvegarder ?** | 3 zones : dossier de travail → staging → dépôt local (`add`, `commit`) |
| 🔵 | **Comment relire ?** | `git log --oneline`, `git diff` |
| 🔵 | **Comment annuler ?** | `restore`, `restore --staged`, `revert` |
| 🔵 | **Comment tester sans risque ?** | Une **branche** : `switch -c`, puis `merge` |
| 🔵 | **Comment partager ?** | GitHub : `push`, `pull`, `clone` |
| 🔵 | **Que faire en cas de conflit ?** | Lire les marqueurs, choisir, nettoyer, `add`, `commit` |

### 🔷 **Le rythme de travail à retenir**

```
git pull                      → je pars de la dernière version
(modifier mes fichiers)
git status                    → je regarde où j'en suis
git diff                      → je relis mes changements
git add fichier               → je prépare
git commit -m "message clair" → je sauvegarde
git pull                      → je récupère le travail des autres
git push                      → j'envoie le mien
```

### 🔷 **Les bonnes habitudes**

- 🔵 **`git status` tout le temps** : il ne coûte rien et évite de se perdre
- 🔵 **Des messages de commit clairs** : *« Ajout de l’introduction »*, pas *« truc »*
- 🔵 **Des petits commits, souvent**
- 🔵 **`git pull` avant de travailler** et avant chaque `push`
- 🔵 **Une branche par idée** à tester
- 🔵 **Jamais de mot de passe ni de fichier personnel** dans un projet
- 🔵 **Ne pas paniquer** devant un message d’erreur : on le lit, on tape `git status`

### 🔷 **Aide-mémoire des commandes**

| ⬜ | **Commande** | **À quoi elle sert** |
|---|---|---|
| 🔵 | `git init` | Démarrer le suivi |
| 🔵 | `git status` | Voir l’état |
| 🔵 | `git add fichier` | Préparer |
| 🔵 | `git commit -m "..."` | Sauvegarder |
| 🔵 | `git log --oneline` | Voir l’historique |
| 🔵 | `git diff` / `git diff --staged` | Voir les changements |
| 🔵 | `git restore fichier` | Annuler une modification non ajoutée |
| 🔵 | `git restore --staged fichier` | Retirer du staging |
| 🔵 | `git revert --no-edit <id>` | Annuler un commit |
| 🔵 | `git switch -c nom` | Créer une branche et y aller |
| 🔵 | `git switch nom` | Changer de branche |
| 🔵 | `git merge nom` | Fusionner une branche dans celle où l’on est |
| 🔵 | `git branch -d nom` | Supprimer une branche fusionnée |
| 🔵 | `git clone adresse` | Copier un projet depuis GitHub |
| 🔵 | `git push` | Envoyer ses commits |
| 🔵 | `git pull` | Récupérer ceux des autres |
| 🔵 | `git merge --abort` | Annuler une fusion en conflit |

### 💙 **LA PHRASE À RETENIR**

> **Git remplace les copies de fichiers par un historique propre et organisé, et GitHub permet de le partager sans s’écraser.**

### 🔷 **Pour continuer à progresser**

- 🔵 **Pratiquer** sur de vrais projets, même petits : le plus efficace
- 🔵 **Utiliser Git dans les projets du club**
- 🔵 **Ne pas hésiter à demander de l’aide** : tout le monde bloque sur Git au début

---

## 🔵⬜ **MERCI !** ⬜🔵

### **01 CLUB** · *Formation Git – Séance 2*

💙**Cours réalisé et présenté par:** 💙
## 🔵⬜ **Oumayma Bouchnaf** ⬜🔵

> 💙 **Des questions ? C’est le moment !**
