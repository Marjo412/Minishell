<img width="150" height="150" alt="image" src="https://github.com/user-attachments/assets/e1110d56-4261-49e2-a841-a9927d6d3e0b" />

## 🎮 Description

**Minishell** est un projet qui consiste à recréer un shell UNIX minimaliste, capable d’interpréter
et d’exécuter des commandes comme un vrai terminal.

---

## 🧩 Objectifs du projet

Le but du projet **Minishell** est de comprendre le fonctionnement interne d’un shell UNIX (comme bash)
en le réimplémentant en C. Vous apprendrez à gérer les processus (parent-enfant), les pipes, la redirection
d’entrée/sortie et la gestion des signaux.

Le programme doit reproduire le comportement d’un shell classique, notamment :
  - L’affichage d’un prompt en attente de commande.
  - L’exécution de commandes simples et chaînées (avec `|`, `<`, `>`, `<<`, `>>`).
  - La gestion des variables d’environnement et du code de retour (`$?`).
  - L’implémentation des builtins (`echo`, `cd`, `pwd`, `export`, `unset`, `env`, `exit`).

---

## 🧠 Concepts théoriques abordés

## 1. **Processus & Fork**
Chaque commande externe est exécutée dans un nouveau processus enfant grâce à `fork()` et `execve()`. Le parent
attend sa fin avec `waitpid()`. Cela permet d’exécuter plusieurs commandes en parallèle dans un pipeline.

## 2. **Signaux**
Le shell doit réagir correctement à :
  - `Ctrl+C` → interrompt la ligne en cours (ne quitte pas le shell)
  - `Ctrl+D` → quitte le shell (EOF)
  - `Ctrl+\` → ignoré et ne fait rien

## 3. **Builtins**
Certaines commandes sont exécutées directement dans le processus du shell (sans fork), car elles modifient son
état interne. Exemple : `cd` change le répertoire du shell lui-même.

## 4. **Heredoc**
Un heredoc permet d’écrire plusieurs lignes de texte jusqu’à un délimiteur. Ces lignes sont ensuite utilisées
comme entrée d’une commande. Il faut gérer les signaux pendant la saisie et supprimer le fichier temporaire à la fin.

## 5. **Redirections & Duplication de descripteurs**
Les redirections et pipes utilisent les appels système dup2() et pipe() pour réassigner les flux standard (`stdin`, `stdout`).

## 6. **Variables d’environnement**
Les variables sont stockées dans une structure (souvent `t_env` ou dans `t_data`) et manipulées par les builtins
`export`, `unset`, `env`, et lors des expansions `$VAR`.

---


## ⚙️ Compilation, exécution et nettoyage

### 1. **Compilation**
Le projet se compile en utilisant la commande :

    make

### 2. **Exécution**
Pour lancer le programme, il faut utiliser la ligne de commande :

    ./minishell

Exemple de commandes :

    minishell> echo "Hello world"
    Hello world
    minishell> ls -l | grep .c | wc -l
    minishell> export NAME=42
    minishell> echo $NAME
    42

## 3. **Nettoyage**
Pour supprimer les fichiers objets et l’exécutable:

    make clean     # Supprime uniquement les fichiers objets (.o)
    make fclean    # Supprime les fichiers objets + l’exécutable
    make re        # Reconstruit complètement le projet

---

## ✨ Pour conclure
**Minishell** est un projet exigeant, une véritable immersion dans le fonctionnement des systèmes
UNIX et des shells. Vous y apprendrez à orchestrer des processus, manipuler les descripteurs de fichiers, et
synchroniser plusieurs comportements dans un environnement interactif. 🚀
Ce projet à été réalisé par daniefe2 et mrosset.
