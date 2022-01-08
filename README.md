1. Bekannte Optionen sind von Gravaton Server übernommen
# Refer to [Minecraft Fandom](https://minecraft.fandom.com/wiki/Server.properties) for information.
- pvp
- difficulty
- max-players
- allow-flight
- allow-nether
- white-list
- enforce-whitelist=true
- max-world-size=5000

# Optimizing (Hopefull)

> Komplette welt größe ist mit dem [Chunky](https://www.spigotmc.org/resources/chunky.81534/) plugin vor generiert (r = 5000, d = 10000 )
> worldborder set d (10000)
> worldborder center 0 0


2. Dieses Beispiel nutzt [Pufferfish](https://github.com/pufferfish-gg/Pufferfish) !!!

#                                                                           Server.Properties
#### network-compression-threshold von 256 auf 512 
- Belastet mehr die internet verbindung um die CPU zu entlasten.

#### simulation-distance von 10 auf 5
- Begrenzt die Reichweite in der Chunks berechnet werden ohne die sichtweite zu minimieren.

#### view-distance von 10 auf 8
- simulation-distance + view-distance = Sichtweite
- Hier kann man also ins. 13 chunks weit sehen.

#                                                                              paper.yml
#### max-auto-save-chunks-per-tick von 24 auf 10
- Speichert die Chunks nach und nach Lag Spikes zu minimieren.

#### prevent-moving-into-unloaded-chunks von false auf true
- Verhindert, dass spieler in nicht geladene chunks laufen um das laden im Main Thread nicht zu provozieren.

#### despawn-ranges von
```yml
despawn-ranges:
    monster:
        soft: 32
        hard: 128
    creature:
        soft: 32
        hard: 128
    ambient:
        soft: 32
        hard: 128
    axolotls:
        soft: 32
        hard: 128
    underground_water_creature:
        soft: 32
        hard: 128
    water_creature:
        soft: 32
        hard: 128
    water_ambient:
        soft: 32
        hard: 64
    misc:
        soft: 32
        hard: 128
```
auf
```yml
despawn-ranges:
    monster:
        soft: 30
        hard: 88
    creature:
        soft: 30
        hard: 88
    ambient:
        soft: 30
        hard: 88
    axolotls:
        soft: 30
        hard: 88
    underground_water_creature:
        soft: 30
        hard: 88
    water_creature:
        soft: 30
        hard: 88
    water_ambient:
        soft: 30
        hard: 88
    misc:
        soft: 30
        hard: 88
```
- Ermöglicht das Anpassen der entity-Despawn-Bereiche (in Blöcken).
- hard = (simulation-distance * 16) + 8

#### max-entity-collisions von 8 auf 6 
- Es ist erwähnenswert, dass dies die maxEntityCramming Gamerule nutzlos macht, wenn ihr Wert über dem Wert dieser Konfigurationsoption liegt.
- Sie können entscheiden, wie viele Kollisionen eine entity gleichzeitig verarbeiten kann.

#### update-pathfinding-on-block-update von true auf false
- weniger wegberechnung durch mobs, der Path wird nun passiv alle 0,25 sec updated.

#### fix-climbing-bypassing-cramming-rule von false auf true
- Entfernt Mob limit bypass durch kletternde mobs z.b. Spinnen.

#### tick-rates von
```yml
tick-rates:
      sensor:
        villager:
          secondarypoisensor: 40
      behavior:
        villager:
          validatenearbypoi: -1
```
auf
```yml
tick-rates:
    sensor:
        villager:
          secondarypoisensor: 80
          nearestbedsensor: 80
          villagerbabiessensor: 40
          playersensor: 40
          nearestlivingentitysensor: 40
    behavior:
        villager:
          validatenearbypoi: 60
          acquirepoi: 120
```
- Dies entscheidet, wie oft bestimmte Verhaltensweisen und Sensoren in Ticks ausgelöst werden.

#### use-faster-eigencraft-redstone von false auf true
- Bessere Redstone berechnung.

#### mob-spawner-tick-rate von 1 auf 2
- Spawning Mobs a bit slower to gain a bit more CPU power back :hehe:

#### optimize-explosions von false auf true
- Optimizing Explosions.

#### grass-spread-tick-rate von 1 auf 4
- Grass spreading wird ein bisschen langsamer berechnet.

#### non-player-arrow-despawn-rate von -1 auf 20 (1sec)
- Lässt nicht aufsammelbare pfeile (z.b. von Skeleten) schneller despawnen.

#### creative-arrow-despawn-rate von -1 auf 20 (1 sec)
- das selbe wie oben nur ist hier die src. ein creative spieler.

#### remove-corrupt-tile-entities von false auf true
- Removing Error generating entitys, wirkt außerdem einigen cheats entgegen.

#### anti-xray configuriert mit hilfe von: [Anti-Xray Config](https://gist.github.com/stonar96/ba18568bd91e5afd590e8038d14e245e)
- Besser als Plugin based ;)

### Resultat:
![XrayTest](../blob/master/XrayTest.png?raw=true)


#                                                                              Bukkit.yml
#### spawn-limits von
```yml
spawn-limits:
  monsters: 70
  animals: 10
  water-animals: 5
  water-ambient: 20
  water-underground-creature: 5
  ambient: 15
```
auf 
```yml
spawn-limits:
    monsters: 20
    animals: 8
    water-animals: 2
    water-ambient: 2
    water-underground-creature: 3
    ambient: 1
```
- Spawn Limit ist Pro spieler also Spieler * Limit 

#### ticks-per von
```yml
ticks-per:
  animal-spawns: 400
  monster-spawns: 1
  water-spawns: 1
  water-ambient-spawns: 1
  water-underground-creature-spawns: 1
  ambient-spawns: 1
  autosave: 6000
```
auf
```yml
ticks-per:
    monster-spawns: 10
    animal-spawns: 20
    water-spawns: 200
    water-ambient-spawns: 200
    water-underground-creature-spawns: 200
    ambient-spawns: 200
```
- Diese Option legt fest, wie oft (in Ticks) der Server versucht, bestimmte Lebewesen zu spawnen.


#                                                                              spigot.yml
#### mob-spawn-range: von 8 auf 3
- Spawnt Mobs näher am spieler um die Begrenzung nicht auffallen zu lassen :P

####  von
```yml
entity-activition-range:
    animals: 32
    monsters: 32
    raiders: 48
    misc: 16
    water: 16
    villagers: 32
    flying-monsters: 32
```
auf
```yml
entity-activition-range:
    animals: 16
    monsters: 24
    raiders: 48
    misc: 8
    water: 8
    villagers: 16
    flying-monsters: 48
```
- die Range in der Mobs berechnet werden (vom spieler aus gesehen.)

#### entity-tracking-range von
```yml
entity-tracking-range:
    players: 48
    animals: 48
    monsters: 48
    misc: 32
    other: 64
```
auf
```yml
entity-tracking-range:
    players: 48
    animals: 48
    monsters: 48
    misc: 32
    other: 64
```
- Die Entfernung in Blöcken, ab der entities sichtbar sind.

#### merge-radius von
```yml
merge-radius:
    item: 2.5
    exp: 3.0
```
auf 
```yml
merge-radius:
    item: 3.5
    exp: 4.0
```
- Dadurch wird der Abstand zwischen den zu Mergenden Items und EXP bestimmt, wodurch die Menge der Gegenstände verringert wird, die auf dem Boden Ticket werden.

#### ticks-per von
```yml
ticks-per:
    hopper-transfer: 8
    hopper-check: 1
```
auf
```yml
ticks-per:
    hopper-transfer: 8
    hopper-check: 8
```
- hopper-transfer
    - Zeit in Ticks, die Hopper warten, um einen Item zu bewegen.
- hopper-check
    - Zeit in Ticks zwischen Hoppern, die nach einem Gegenstand über ihnen oder im Inventar über ihnen suchen.

> Dies macht "Hopper clocks" und einige Item Sort Systems useless, allerdings sollte kleinere Farmen weiterhin funktionieren.


# Plugins die nicht genutzt werden sollten: 
1. "Item Remover" das sollte in der despawn setting und mit merge radius gemacht werden.
2. "Mob Stacker" durch das stacken werden die die ganze zeit mehr mobs gespawned um die anzahl zu halten, was mehr lagg verursacht.

# Nützliches:
[Lag Spikes Finden](https://spark.lucko.me/docs/guides/Finding-lag-spikes)
[Server.properties Wiki](https://minecraft.fandom.com/wiki/Server.properties)
[Anti-Xray Config](https://gist.github.com/stonar96/ba18568bd91e5afd590e8038d14e245e)