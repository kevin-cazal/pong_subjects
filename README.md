# Pong

Crée ton jeu Pong avec TIC-80, en Python ou en Lua : à toi de choisir.

Deux sujets, le même jeu, un langage chacun. Ce dépôt ne contient pas de contenu : il compose les deux, et c'est lui qu'une instance CTFd de la plateforme [CTFd_coding_platform](https://github.com/kevin-cazal/CTFd_coding_platform) importe.

| Sujet | Langage | Ce qu'on y fait |
|---|---|---|
| [PyPong](https://github.com/kevin-cazal/pypong_subject) | Python | un Pong à un joueur : le pad, la balle, les rebonds, le score, les vies |
| [LuaPong](https://github.com/kevin-cazal/luapong_subject) | Lua | le même jeu, étape par étape, en Lua |

Aucun ordre imposé : le participant fait l'un, l'autre, ou les deux, dans l'ordre qu'il veut. Les deux sujets ont les mêmes étapes et les mêmes quiz, seul le langage change.

## À savoir avant d'importer

`workshop.yaml` ne déclare aucun `role: starter` : les deux sujets sont au libre choix. La plateforme exige aujourd'hui exactement un starter, et `tools/sync_workshop.py` refuse donc ce fichier (`expected exactly one subject with role: starter, found 0`).

En attendant que la plateforme accepte un atelier sans starter, passer PyPong en `role: starter` rend l'import possible, mais impose alors de finir PyPong avant LuaPong.

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

Les sujets sont des sous-modules : pousser sur l'un d'eux ne change rien tant que le pointeur n'est pas avancé ici.

```sh
git -C luapong_subject pull
git add luapong_subject && git commit -m "bump luapong" && git push
```
