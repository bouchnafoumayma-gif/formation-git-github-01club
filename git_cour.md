# Cours Git – Séance 1 : sauvegarder son travail en local

*Formation pour débutants · Séance 1 sur 2*

## Objectifs de la séance

À la fin de cette séance, l’étudiant sait :

- expliquer **pourquoi** Git existe et **ce qu’il fait** ;
- configurer Git (nom et email) ;
- expliquer les **3 zones** de Git ;
- utiliser `git init`, `git status`, `git add` et `git commit` ;
- lire l’historique avec `git log` et voir les changements avec `git diff`.

**Plan indicatif de la séance**

| Partie | Contenu | Durée indicative |
| --- | --- | --- |
| 1 | La problématique | 15 min |
| 2 | C’est quoi Git ? | 15 min |
| 3 | La configuration | 10 min |
| 4 | Les 3 zones de Git | 15 min |
| 5 | Les premières commandes | 30 min |
| 6 | L’historique | 20 min |
| 7 | Exercice final | 15 min |

*Les durées sont des suggestions : adapte-les au rythme du groupe.*

## 1. La problématique : pourquoi Git a-t-il été créé ?

### 1.1 Le chaos des versions (activité d’accroche)

Commence par poser cette question aux étudiants : **« Comment gardez-vous les anciennes versions d’un travail ? »**

Demande-leur de donner leurs propres noms de fichiers « catastrophiques ». Ils connaissent sûrement ça :

- `rapport.docx`
- `rapport_final.docx`
- `rapport_final_vrai.docx`
- `rapport_final_vrai_corrige_V3.docx`

Ça les fait sourire, et ça montre le problème : **on ne sait plus quelle version est la bonne, ni ce qui a changé entre deux versions.**

**Pourquoi commencer ainsi :** les étudiants vivent le problème avant d’entendre la solution. Ils sont actifs, et l’idée reste mieux en mémoire.

### 1.2 Ce qui se complique quand on travaille à plusieurs

1. **Écrasement** : deux personnes modifient le même fichier, et l’une efface le travail de l’autre.
2. **Pas d’historique** : impossible de savoir qui a changé quoi, quand et pourquoi.
3. **Pas de retour en arrière** : si une modification casse tout, on ne peut pas revenir à la version qui marchait.
4. **Tester des idées est risqué** : on a peur de casser le projet.

### 1.3 La petite histoire de Git (à raconter en 1 minute)

En 2005, **Linus Torvalds**, le créateur de Linux, avait besoin d’un outil pour que des milliers de développeurs travaillent ensemble sur le même projet. L’outil qu’ils utilisaient est devenu indisponible, alors il a créé Git en quelques semaines.

Il voulait un outil :

- **rapide** ;
- **fiable** ;
- qui permet à **chacun de travailler en parallèle**.

### 1.4 La transition vers la suite

Pose la question : **« Et si on avait un outil qui garde automatiquement tout l’historique, sans les noms de fichiers à rallonge ? »** C’est exactement ce que fait Git.

## 2. C’est quoi Git ?

### 2.1 Définition simple

> **Git est un outil qui enregistre l’historique de ton projet, comme des points de sauvegarde dans un jeu vidéo, et qui permet à plusieurs personnes de travailler ensemble sans s’écraser.**

### 2.2 Exemple simple : écrire un devoir à plusieurs

1. Tu écris l’introduction, puis tu fais une sauvegarde nommée *« Ajout de l’introduction »* (c’est un **commit**).
2. Tu ajoutes le chapitre 1, nouvelle sauvegarde : *« Ajout du chapitre 1 »*.
3. Tu changes d’avis et le chapitre 1 est mauvais : tu reviens à la sauvegarde précédente en un instant.
4. Ton camarade veut tester une autre idée de conclusion sans toucher à ta version : il crée sa **branche** (une copie parallèle).
5. Quand sa conclusion est bonne, vous la **fusionnez** avec la version principale.

Un même fichier, mais avec tout l’historique, **sans** `_final_vrai_V3`.

*Les points 3 à 5 (retour en arrière, branches, fusion) seront détaillés en séance 2. Aujourd’hui, on apprend à faire les points 1 et 2 : sauvegarder son travail.*

### 2.3 Une phrase à retenir

> **Git remplace les copies de fichiers par un historique propre et organisé.**

### 2.4 Git et GitHub : ne pas confondre

- **Git** : l’outil installé sur ton ordinateur, qui garde l’historique.
- **GitHub** : un site web où l’on peut envoyer son projet pour le partager. On le verra en séance 2.

## 3. Configurer Git

**Exemple pour l’introduire :** quand tu rends un devoir, tu écris ton nom dessus. Git fait pareil : chaque sauvegarde (commit) est **signée** avec un nom et un email. La configuration, c’est dire une fois pour toutes quel nom mettre.

*Les commandes se tapent dans le terminal (sous Windows, on peut utiliser « Git Bash »).*

### 3.1 Vérifier que Git est installé

```
git --version
```

**Pourquoi :** avant de configurer quoi que ce soit, on s’assure que l’outil existe. Si ça affiche un numéro de version (par exemple `git version 2.43.0`), c’est bon.

### 3.2 Donner son nom et son email

```
git config --global user.name "Marie Dupont"
git config --global user.email "marie@exemple.com"
```

**Pourquoi le faire :** chaque commit garde en mémoire *qui* a fait la modification. Dans un travail d’équipe, on voit ainsi qui a changé quoi.

**Pourquoi mettre le même email que GitHub :** GitHub relie les commits à ton compte grâce à l’email. Avec un email différent, tes contributions n’apparaissent pas sur ton profil.

**À ne pas faire :**

- Oublier les guillemets quand le nom contient un espace. `git config --global user.name Marie Dupont` ne marche pas bien : Git lit « Marie » comme le nom et « Dupont » comme autre chose.
- Mettre un faux email au hasard : tes commits ne seront reliés à personne.
- Mettre un mot de passe dans la configuration : ce n’est jamais nécessaire ici.

### 3.3 Comprendre `--global`

- **Avec `--global`** : le réglage s’applique à **tous** tes projets sur l’ordinateur. On le fait une seule fois.
- **Sans `--global`** (dans un dossier de projet) : le réglage s’applique à **ce projet seulement**.

**Pourquoi `--global` pour commencer :** on évite de refaire la configuration à chaque nouveau projet. On utilise la version locale seulement si on veut un autre email pour un projet précis (par exemple un projet de travail).

### 3.4 Vérifier que ça a marché

```
git config user.name
git config user.email
```

**Pourquoi :** une faute de frappe est vite arrivée, et on ne la découvre qu’au premier commit si on ne vérifie pas. Pour tout voir d’un coup : `git config --list`.

### 3.5 (Optionnel) Choisir le nom de la branche principale

```
git config --global init.defaultBranch main
```

**Pourquoi :** selon la version de Git, la branche principale s’appelle `master` ou `main`. GitHub utilise `main`, donc on évite une confusion plus tard.

### Mini exercice

1. Taper `git --version`.
2. Configurer son nom et son email.
3. Vérifier avec `git config user.name`.

> **Récap :** configurer Git, c’est signer ton travail une seule fois, pour que chaque sauvegarde porte ton nom.

## 4. Les trois zones de Git

C’est **la** notion à bien expliquer **avant** les commandes. Sans elle, `add` et `commit` paraissent magiques.

### 4.1 Les 3 zones

1. **Le dossier de travail** (working directory) : tes fichiers, tels que tu les modifies.
2. **La zone de préparation** (staging) : ce que tu as choisi de sauvegarder, avec `git add`.
3. **Le dépôt local** (repository) : l’historique des sauvegardes validées sur ton ordinateur, avec `git commit`.

### 4.2 Exemple : envoyer un colis

| Zone | Image du colis |
| --- | --- |
| Dossier de travail | Ton bureau, où tu travailles et où tout traîne |
| Staging | Le carton, où tu mets seulement ce que tu veux envoyer |
| Dépôt local | Le colis fermé et étiqueté, rangé chez toi avec son numéro de suivi |
| Dépôt distant (GitHub) | Le bureau de poste, où tu l’envoies pour que d’autres y accèdent *(séance 2)* |

### 4.3 Le schéma à retenir

```
Dossier de travail  --git add-->  Staging  --git commit-->  Dépôt local
```

### 4.4 Pourquoi la zone de préparation existe

Tu peux avoir modifié 5 fichiers mais n’en sauvegarder que 2, ceux qui vont ensemble. Sans cette zone, tu sauvegarderais tout, même ce qui n’est pas fini.

### 4.5 Attention : le dépôt distant n’est pas une des 3 zones

Le dépôt distant (GitHub) est un **quatrième endroit**, à part. Il se voit en séance 2. Si on le mélange avec les 3 zones, les étudiants confondent `commit` (qui reste sur ton ordinateur) et `push` (qui envoie vers GitHub). C’est l’une des confusions les plus fréquentes.

## 5. Les premières commandes

**Exemple fil rouge pour toute cette partie :** tu écris un devoir dans un dossier `mon-devoir`. On y met un fichier `intro.txt` et on apprend à le sauvegarder avec Git.

**Le cycle à retenir :** modifier → préparer → sauvegarder.

### 5.1 `git init` : démarrer le suivi

```
cd mon-devoir
git init
```

**Ce que ça fait :** Git crée un dossier caché `.git` qui contiendra tout l’historique.

**Exemple :** c’est comme acheter un classeur vide pour ton projet. Tant que tu n’as pas le classeur, rien n’est rangé.

**Pourquoi le faire :** sans `git init`, Git ne surveille rien dans ce dossier.

**À ne pas faire :**

- Le faire plusieurs fois : une seule fois par projet suffit.
- Le faire dans un dossier trop large (Bureau, Documents, dossier personnel) : Git essaierait de suivre des centaines de fichiers sans rapport. Toujours dans le dossier **du projet**.
- Le faire dans un dossier qui est déjà un dépôt Git (on ne met pas un classeur dans un classeur).

### 5.2 `git status` : regarder où on en est

```
git status
```

**Ce que ça fait :** Git explique quels fichiers sont nouveaux, modifiés, ou prêts à être sauvegardés.

**Exemple :** c’est regarder ton bureau avant de ranger : « qu’est-ce qui traîne, qu’est-ce qui est déjà rangé ? »

**Pourquoi le faire :** c’est la commande de sécurité. Les débutants se perdent presque toujours parce qu’ils ne savent pas ce que Git est en train de voir.

**Conseil :** taper `git status` **avant et après chaque autre commande**. Ça ne modifie rien, donc zéro risque.

### 5.3 `git add` : préparer ce qu’on veut sauvegarder

```
git add intro.txt
```

**Ce que ça fait :** Git met `intro.txt` dans la **zone de préparation**.

**Exemple :** tu prépares ta valise. Tu choisis ce que tu mets dedans, mais tu n’as pas encore fermé la valise ni quitté la maison.

**Pourquoi cette étape existe :** elle permet de **choisir** quelles modifications vont ensemble. Si tu as modifié 5 fichiers mais que seuls 2 forment une même idée, tu ajoutes ces 2 et tu fais un commit propre.

**Deux façons de l’utiliser :**

- `git add intro.txt` : un fichier précis. **Recommandé au début**, parce qu’on contrôle tout.
- `git add .` : tout ce qui a changé dans le dossier. Pratique, mais à utiliser avec attention : on peut ajouter par erreur un brouillon, un mot de passe ou un fichier lourd.

**À ne pas faire :**

- Croire que `git add` sauvegarde : **rien n’est encore enregistré dans l’historique**. C’est l’erreur n°1 des débutants.
- Faire `git add .` sans avoir regardé `git status` avant.

### 5.4 `git commit` : enregistrer la version

```
git commit -m "Ajout de l'introduction"
```

**Ce que ça fait :** Git enregistre une version avec ton message. C’est ton **point de sauvegarde**.

**Exemple :** tu fermes la valise et tu mets une étiquette dessus : « valise vacances été ». Plus tard, tu retrouves facilement ce qu’elle contient.

**Pourquoi le message est important :** dans 3 mois, personne (y compris toi) ne se souviendra de ce que tu as fait. Le message est ton explication.

| ❌ À éviter | ✅ À faire |
| --- | --- |
| `"truc"` | `"Ajout de l'introduction"` |
| `"modif"` | `"Correction des fautes dans le chapitre 1"` |
| `"final"` | `"Ajout de la conclusion"` |

**Règle simple :** le message doit répondre à la question *« qu’est-ce que j’ai fait dans cette sauvegarde ? »*.

**À ne pas faire :**

- Faire un énorme commit avec 3 jours de travail. Plusieurs petits commits valent mieux qu’un gros : on retrouve et on annule plus facilement.
- Oublier `-m "..."`. Sans lui, Git ouvre un éditeur de texte (souvent `vim`) qui bloque beaucoup de débutants (voir la partie 9).

### 5.5 Le cycle complet à montrer en démonstration

```
git init
git status
git add intro.txt
git status
git commit -m "Ajout de l'introduction"
git status
git log
```

Les étudiants voient `git status` changer à chaque étape : **fichier non suivi → prêt à sauvegarder → tout propre**. C’est le moment où l’idée des 3 zones devient claire.

### Mini exercice

1. Créer un dossier `mon-devoir` et faire `git init`.
2. Créer un fichier `intro.txt` avec une phrase.
3. Faire `git status`, puis `git add intro.txt`, puis `git status` encore.
4. Faire un `git commit` avec un bon message.
5. Modifier le fichier, puis refaire un 2e commit.
6. Taper `git log` et lire l’historique.

> **Récap :** on modifie, on prépare avec `add`, on sauvegarde avec `commit`, et on vérifie avec `status` à chaque étape.

## 6. Consulter l’historique : `git log` et `git diff`

**Exemple fil rouge :** on reprend le dossier `mon-devoir` avec `intro.txt`. Tu as déjà fait 2 commits. Tu veux répondre à deux questions :

- *« Qu’est-ce que j’ai sauvegardé jusqu’ici ? »* → `git log`
- *« Qu’est-ce que j’ai changé depuis la dernière sauvegarde ? »* → `git diff`

### 6.1 `git log` : lire l’historique

```
git log
```

**Ce que ça fait :** Git affiche la liste de tes commits, du plus récent au plus ancien, avec pour chacun l’auteur, la date et le message.

**Exemple :** c’est le journal de bord de ton projet. On y lit : *« lundi, Marie a ajouté l’introduction ; mardi, Marie a ajouté le chapitre 1 »*.

**Pourquoi le faire :** pour retrouver ce qui a été fait, par qui, et quand. C’est là que les bons messages de commit servent enfin.

**La version courte, plus pratique :**

```
git log --oneline
```

Une ligne par commit, plus facile à lire quand l’historique grandit. C’est celle que je conseille aux débutants.

**Détail qui bloque beaucoup d’étudiants :** quand l’historique est long, Git ouvre un affichage où l’on ne peut plus rien taper. **Pour en sortir, appuyer sur `q`.** Préviens tes étudiants pour éviter les « mon terminal est bloqué ! ».

**Ce que tu verras dans chaque commit :** une suite de lettres et de chiffres (par exemple `a1b2c3d`). C’est **l’identifiant du commit**, comme un numéro de suivi de colis. On s’en servira en séance 2 pour revenir en arrière.

### 6.2 `git diff` : voir ce qui a changé

```
git diff
```

**Ce que ça fait :** Git compare ton fichier actuel à la dernière version sauvegardée et montre les différences.

**Comment lire le résultat :**

- une ligne qui commence par **`+`** (en vert) : ligne **ajoutée** ;
- une ligne qui commence par **`-`** (en rouge) : ligne **supprimée**.

**Exemple :** tu ajoutes une phrase à `intro.txt`. `git diff` te montre :

```
+ Cette phrase est nouvelle.
```

Tu vois exactement ce qui a bougé, sans rouvrir tout le fichier.

**Pourquoi le faire avant un `git add` :** c’est ta relecture. Tu vérifies que tu sauvegardes bien ce que tu voulais, et pas un test oublié ou une faute de frappe.

### 6.3 Le piège classique : `git diff` ne montre rien après un `git add`

Après `git add intro.txt`, si tu fais `git diff`, **rien ne s’affiche**. C’est normal, et c’est le moment idéal pour reparler des 3 zones :

- `git diff` compare le **dossier de travail** au **staging** ;
- une fois le fichier ajouté, il est dans le staging : il n’y a plus de différence à montrer.

Pour voir ce qui est **prêt à être sauvegardé**, on utilise :

```
git diff --staged
```

| Je veux voir… | Commande |
| --- | --- |
| Ce que j’ai modifié mais **pas encore ajouté** | `git diff` |
| Ce que j’ai ajouté et qui sera dans **le prochain commit** | `git diff --staged` |
| Les commits **déjà faits** | `git log --oneline` |

### 6.4 Ce qu’il ne faut pas faire

- **Avoir peur de ces commandes.** `git log` et `git diff` ne modifient **rien** : elles servent juste à regarder.
- **Faire un commit « à l’aveugle ».** Prends l’habitude : `git status`, puis `git diff`, puis `git add`, puis `git commit`.
- **Paniquer devant l’affichage qui reste ouvert** : c’est `q` pour quitter.

### 6.5 Le cycle complet à montrer

```
(modifier intro.txt)
git status          → je vois que le fichier a changé
git diff            → je vois exactement ce qui a changé
git add intro.txt   → je prépare
git diff --staged   → je vérifie ce qui va partir
git commit -m "Ajout d'une phrase dans l'introduction"
git log --oneline   → je vois ma nouvelle sauvegarde
```

### Mini exercice

1. Modifier `intro.txt` en ajoutant une phrase.
2. Taper `git diff` et repérer la ligne avec `+`.
3. Faire `git add`, puis `git diff` : constater que rien ne s’affiche.
4. Taper `git diff --staged` : la modification réapparaît.
5. Faire le commit, puis `git log --oneline`.

> **Récap :** `git log` montre ce qui a été sauvegardé, `git diff` montre ce qui a changé depuis, et aucune des deux ne modifie quoi que ce soit.

## 7. Exercice final de la séance 1

**Scénario :** tu écris un devoir à plusieurs étapes et tu le sauvegardes avec Git.

1. Créer un dossier `mon-devoir`, entrer dedans, puis faire `git init`.
2. Vérifier la configuration avec `git config user.name` et `git config user.email`.
3. Créer `intro.txt` avec une phrase. Faire `git status`, `git add intro.txt`, puis `git commit -m "Ajout de l'introduction"`.
4. Créer `chapitre1.txt`. Faire `git add chapitre1.txt`, puis `git commit -m "Ajout du chapitre 1"`.
5. Modifier `intro.txt`. Faire `git diff` et repérer le `+`.
6. Faire `git add intro.txt`, `git diff --staged`, puis le commit avec un message clair.
7. Terminer avec `git log --oneline` : on doit voir **3 commits**.

**Auto-évaluation : l’étudiant doit savoir répondre à ces questions :**

- Pourquoi utilise-t-on Git plutôt que `rapport_final_vrai_V3.docx` ?
- Quelles sont les 3 zones, et quelle commande fait passer d’une zone à l’autre ?
- Pourquoi `git add` ne sauvegarde-t-il pas encore ?
- Quelle différence entre `git diff` et `git log` ?

## 8. Récapitulatif des commandes

| Commande | À quoi elle sert |
| --- | --- |
| `git --version` | Vérifier que Git est installé |
| `git config --global user.name "..."` | Donner son nom (une seule fois) |
| `git config --global user.email "..."` | Donner son email (une seule fois) |
| `git init` | Démarrer le suivi dans un dossier de projet |
| `git status` | Voir l’état des fichiers (à taper tout le temps) |
| `git add fichier` | Préparer un fichier pour la sauvegarde |
| `git commit -m "message"` | Enregistrer une version avec un message |
| `git log --oneline` | Voir l’historique, une ligne par commit |
| `git diff` | Voir les modifications pas encore ajoutées |
| `git diff --staged` | Voir ce qui sera dans le prochain commit |

## 9. Les erreurs fréquentes des étudiants (aide pour l’enseignante)

| Ce que l’étudiant voit | Cause probable | Solution |
| --- | --- | --- |
| `fatal: not a git repository` | Il a oublié `git init` ou il est dans le mauvais dossier | Vérifier le dossier, puis faire `git init` si besoin |
| `Author identity unknown` | La configuration du nom et de l’email n’a pas été faite | Refaire la partie 3 |
| `nothing to commit` | Il n’a rien modifié, ou il a oublié `git add` | Faire `git status` pour voir où il en est |
| Le terminal « bloqué » après `git log` | L’affichage long est resté ouvert | Appuyer sur `q` |
| Une fenêtre étrange s’ouvre au commit | Il a oublié `-m "..."` et Git a ouvert l’éditeur `vim` | Appuyer sur `Échap`, taper `:q!` puis `Entrée`, et refaire le commit avec `-m` |
| `git diff` n’affiche rien | Le fichier est déjà dans le staging, ou rien n’a changé | Essayer `git diff --staged` |

## 10. Aperçu de la séance 2

La séance 1 se suffit à elle-même : à la fin, les étudiants savent **sauvegarder et consulter l’historique**. La séance 2 porte sur **revenir en arrière et travailler avec les autres** :

1. Un court rappel de la séance 1.
2. Revenir en arrière (annuler une erreur).
3. Les branches et la fusion.
4. GitHub : `clone`, `push`, `pull`.
5. Les conflits.
6. Un exercice final en binôme.

*Cette partie sera rédigée en détail dans la suite du cours, avec les mêmes exemples (le devoir à plusieurs, la conclusion de ton camarade, le colis et le bureau de poste).*
