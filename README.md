# Anarchy Addon (Meteor)

Ton client = **Meteor Client** (base, contient déjà la plupart des hacks de Wurst et LiquidBounce)
\+ cet addon, qui ajoute une catégorie **Anarchy** :

| Module | Origine | Ce qu'il fait |
|---|---|---|
| **elytra-cruise** | nouveau | Vol en élytres pour 2b2fr, en physique vanilla (voir plus bas) |
| **glide** | Wurst | Ralentit tes chutes |
| **dolphin** | Wurst | Remonte tout seul à la surface dans l'eau |
| **eagle** | LiquidBounce | S'accroupit automatiquement au bord des blocs (bridge) |
| **panic** | Wurst | Désactive tous les modules d'un coup |

Déjà dans Meteor (pas besoin de les ajouter) : KillAura, Criticals, Velocity, AutoTotem, CrystalAura, Speed, Flight, NoFall, Scaffold, Step, Spider, Jesus, Blink, Timer, ESP, Xray, Tracers, Fullbright, Freecam, Nuker, AutoTool, AutoEat, ElytraFly, etc.

## Compiler

Il faut **Java 25** (JDK, par ex. Temurin 25) et une connexion internet.

```
cd anarchy-addon
./gradlew build          (Windows : gradlew.bat build)
```

Le fichier se trouve ensuite dans `build/libs/anarchy-addon-0.1.0.jar`.

Le projet vise **Minecraft 26.3** avec la dernière Meteor. Pour une autre version, modifie
`gradle/libs.versions.toml` (`minecraft`, `meteor`, `fabric-loader`) pour qu'ils correspondent
à ta version de Meteor.

## Installer

1. Installe **Fabric Loader** pour ta version de Minecraft.
2. Mets dans `.minecraft/mods/` : le jar de **Meteor Client** (meteorclient.com) + `anarchy-addon-0.1.0.jar`.
3. Lance le jeu, ouvre la ClickGUI de Meteor (touche **Shift droit**) → catégorie **Anarchy**.

## ElytraCruise : comment ça marche

Les anti-cheats de mouvement détectent quand ta vitesse ne correspond pas à la physique du jeu.
ElytraCruise **ne touche jamais à ta vitesse** : il fait seulement ce qu'un joueur pourrait faire
à la main, mais en continu :

- il ajuste ton **pitch** (inclinaison) pour tenir une altitude ;
- il lance des **fusées** quand tu ralentis ou que tu es trop bas ;
- quand le serveur te **rubberband** (te renvoie en arrière), il fait une pause et baisse
  automatiquement sa vitesse max de 10 % (elle remonte doucement ensuite).

Tu gardes le contrôle de la direction avec la souris. L'info à côté du module affiche
ta vitesse (blocs/s) et le nombre de rubberbands (RB).

### Utilisation

1. Équipe des élytres, mets des fusées dans l'inventaire.
2. Active **elytra-cruise**, saute d'un endroit en hauteur : les élytres s'ouvrent seules.
3. Oriente-toi avec la souris. C'est tout.

### Réglages conseillés pour 2b2fr

Commence prudent puis monte petit à petit :

- `max-speed` : **28–32**. Si le compteur RB augmente vite, baisse de 2 en 2.
- `min-speed` : **20–22**.
- `rocket-delay` : **30–40** ticks.
- `rotation-speed` : **3–5** (plus bas = plus humain).
- Nether : `altitude-mode` = Fixed, `fixed-altitude` = **122+** pour voler au-dessus du toit
  (si le serveur l'autorise).

Si ça rubberband toujours : regarde à quelle vitesse ça commence, et règle `max-speed`
juste en dessous. C'est le seul réglage qui compte vraiment contre un anti-cheat de vitesse.
