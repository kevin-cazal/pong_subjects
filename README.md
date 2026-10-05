# Pong

Crée ton jeu Pong avec TIC-80, en Python ou en Lua : à toi de choisir.

Deux sujets, le même jeu, un langage chacun. Ce dépôt les compose et porte la page d'accueil, et c'est lui qu'une instance CTFd de la plateforme [CTFd_coding_platform](https://github.com/kevin-cazal/CTFd_coding_platform) importe.

| Ordre | Sujet | Ce qu'on y fait |
|---|---|---|
| démarrage | [Accueil](accueil/) | lire quelques lignes : deux sujets, la même console, le même jeu |
| au choix | [PyPong](https://github.com/kevin-cazal/pypong_subject) | un Pong à un joueur en Python : le pad, la balle, les rebonds, le score, les vies |
| au choix | [LuaPong](https://github.com/kevin-cazal/luapong_subject) | le même jeu, étape par étape, en Lua |

Une fois l'accueil lu, les deux sujets s'ouvrent en même temps. Le participant fait l'un, l'autre, ou les deux, dans l'ordre qu'il veut. Les deux sujets ont les mêmes étapes et les mêmes quiz, seul le langage change.

## L'accueil, un sujet à part

`accueil/` est le starter de l'atelier, et il vit dans ce dépôt. Il tient en une étape : un texte court et un bouton « J'ai lu ».

C'est une exception voulue : il n'a aucun exercice, donc ni étape de clôture, ni avis à donner, ni « Pour aller plus loin ». Dans `workshop.yaml`, il est désigné par un simple `path:`, sans `repo:`.

Cette forme demande une plateforme qui inclut [la PR « one-step starter »](https://github.com/Manta-Epitech-Academy/ctfd-workshop-platform/pull/41) : sans elle, les deux sujets s'importent sans attendre l'accueil, et l'accueil n'apparaît sur aucune page.

## Mettre cet atelier en ligne

```sh
git clone --recursive https://github.com/kevin-cazal/pong_subjects
git clone https://github.com/kevin-cazal/CTFd_coding_platform
cd CTFd_coding_platform
python3 tools/sync_workshop.py ../pong_subjects \
    --url http://localhost:8080 --admin-user admin --admin-pass ...
```

Les réponses des quiz sont chiffrées dans chaque sujet : lancer `GPG_PASSPHRASE=... ./decrypt.sh` dans `pypong_subject` et dans `luapong_subject` avant l'import.

Depuis une instance déjà déployée, la page `/admin/workshop/sync` fait la même chose en allant chercher ce dépôt puis chacun de ses sujets sur GitHub.

## Mettre à jour un sujet

Depuis la page `/admin/workshop/sync`, chaque import prend la tête de la branche indiquée par `ref:` dans `workshop.yaml` (`content/lint-fixes` pour PyPong, `main` pour LuaPong) : pousser sur un sujet puis cliquer sur Sync suffit. Pour figer un sujet avant une session, remettre `ref: submodule`, un tag ou un commit.

En ligne de commande, c'est le sous-module qui est lu : pousser sur un sujet ne change rien tant que le pointeur n'est pas avancé ici.

```sh
git -C luapong_subject pull
git add luapong_subject && git commit -m "bump luapong" && git push
```
