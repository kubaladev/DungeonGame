# Dungeon Crawler VS tutorial od [Hemisfera](https://www.hemisfera.sk). <img align="right" alt="hemisfera.sk" width="128px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/logo.png?raw=true" />
  
Tento návod ti pomôže vytvoriť vlastnú 2D hru žánru [Dungeon Crawler](https://www.youtube.com/watch?v=FQed13kgHSE). Hráč ovláda hrdinu, ktorý sa ocitol v mysterióznej jaskyni plnej nástrah a nepriatelov. Naprogramuj ho tak, aby sa mu podarilo z jaskyne dostať a zároveň, aby to pre teba ako hráča bola výzva.
  
Ak sa zasekneš alebo si nebudeš v niektorej časti istý, tak neváhaj spýtať sa lektora alebo jedného z tvojích spolužiakov. **Držíme ti palce!**
## Inštalácia
Aby si mohol začať programovat, tak potrebuješ mať stiahnuté unity, **verziu 2021** alebo novšiu. Ak ešte nemáš tak urob tak na [tomto linku](https://unity.com/download). Ak máš s inštaláciou problémy, tak skús si pozrieť [toto video](https://www.youtube.com/watch?v=9IKSJdNqzWg).
  
Ďalším krokom je stiahnuť si projekt z tejto github stránky. Takto nebudeš musiet nahadzovať grafiku, objekty do hernej scény a môžeš sa sústrediť na programovanie. V prípade, že máš grafiku vlastnú, tak **odporúčam ti aj tak si spraviť najprv všetko s touto grafikou** a potom na záver ju **vymeniť za vlasnú**.
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/0.gif?raw=true" alt="Error" width="75%"/>
  
Keď máš projekt stiahnutí otvor si ho pomocou Unity Hubu. Ak máš nainštalovaných viacero verzii daj pozor aby si ju otvoril v tej 2021. 
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/01.gif?raw=true" alt="Error" width="75%"/>
  
Posledný krok je otvoriť si scénu **Level1**.
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/02.gif?raw=true" alt="Error" width="75%"/>

## Pohyb hráča <img align="right" alt="hemisfera.sk" width="32px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/player.png?raw=true" />
Poďme si rozpohybovať hráča. Nájdime si, kde v projekte máme objekt hráča uložený. Mal by sa nachádzať v **priečinku prefabs**. Následne si ho rozklikneme možnosťou **open prefab**. Tento krok je dôležitý, **nepreskakuj ho!** Keďže ide o hru s pohľadom zhora, tak hráč by sa mal vedieť hýbať do všetkých smerov.  

Pridajme hráčovi nový komponent typu Script machine, nazvime ho Player a uložme si tento graf do súboru.
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/1.gif?raw=true" alt="Error" width="75%"/>
  
**Otvorme si graf** vo Visual Scripting editore a hurá! Môžeme sa pustiť do kódenia.
 >**_Tip 1: Zoom:_** Pomocou dvojkliku vo visual editor zóne si vieš zväčšiť alebo zmenšiť okno v ktoróm sa tvorí vizuálny skript. Pomôže ti to ak budeš tvoriť rozsiahlé skripty.

<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/2.gif?raw=true" alt="Error" width="75%"/>

Ako prvé musíme detekovať, kedy hráč stlačil klávesy na pohyb postavy. Najlepši spôsob je použiť príkaz **Get Axis Raw**. V ňom upresníme, či sa chceme snímať **horizontálny**(vľavo-vpravo) alebo **vertikálny**(hore-dole) pohyb. V našom prípade chceme oba typy sledovať, pretože hráč sa vie pohybovať do všetkých smerov.

>**_Príkaz: GetAxisRaw("Horizontal)_** funguje tak, že ak je stlačená šípka vpravo, tak príkaz da výslednu hodnotu 1. Naopak ak je stlačená šípka  vľavo, tak príkaz da výslednu hodnotu -1. To je pre nás užitočné lebo hodnotu použijeme na posun po X osy. Rovnako to platí pre vertikálny smer.

Výsledok príkazov si uložíme do nového **Vectoru3**(alebo Vectoru2, aj ten by fungoval správne, keďže robíme 2D hru).

>**_Príkaz: Vector3 Create_** nám vytvorí Vektor, ktorí hovorí o smere a veľkosti posunu pre ľubovolný herný objekt. Používať ho budeme vždy keď budeme chcieť hýbať objektami. 

<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/p1.gif?raw=true" alt="Error" width="75%"/>


