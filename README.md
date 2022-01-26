# Dungeon Crawler VS tutorial od [Hemisfera](https://www.hemisfera.sk). [<img align="right" alt="hemisfera.sk" width="128px" src="Images/logo.png?raw=true" />](https://www.hemisfera.sk)
  
Vitaj herný tvorca, vítam ťa vo svete Unity. Tento návod ti pomôže vytvoriť vlastnú 2D hru žánru [Dungeon Crawler](https://www.youtube.com/watch?v=FQed13kgHSE). Hráč ovláda hrdinu, ktorý sa ocitol v mysterióznej jaskyni plnej nástrah a nepriatelov. Naprogramuj ho tak, aby sa mu podarilo z jaskyne dostať a zároveň, aby to pre teba ako hráča bola výzva.
  
Ak sa zasekneš alebo si nebudeš v niektorej časti istý, tak neváhaj spýtať sa lektora alebo jedného z tvojích spolužiakov. **Držíme ti palce!**

# Obsah
1. [**Inštalácia** :electric_plug:](#install)
2. [**Pohyb hráča** <img alt="hemisfera.sk" width="16px" src="Images/player.png?raw=true" />](#movement)
3. [**Klúč** <img alt="hemisfera.sk" width="16px" src="Images/key.png?raw=true" />](#key)
4. [**Coin** <img alt="hemisfera.sk" width="16px" src="Images/coin.png?raw=true" />](#coin)
5. [**Pasca** <img alt="hemisfera.sk" width="16px" src="Images/trap.png?raw=true" />](#trap)
6. [**Nepriateľ** <img alt="hemisfera.sk" width="16px" src="Images/enemy.png?raw=true" />](#enemy)

## :electric_plug: Inštalácia <a name="install"></a>
Aby si mohol začať programovat, tak potrebuješ mať stiahnuté unity, **verziu 2021** alebo novšiu. Ak ešte Unity nemáš tak urob tak na [tomto linku](https://unity.com/download). Keby máš s inštaláciou problémy, tak skús si pozrieť [toto video](https://www.youtube.com/watch?v=9IKSJdNqzWg).
  
Ďalším krokom je stiahnuť si projekt z github stránky. Takto nebudeš musiet nahadzovať grafiku, objekty do hernej scény a môžeš sa sústrediť na programovanie. V prípade, že máš grafiku vlastnú, tak **odporúčam ti aj tak si spraviť najprv všetko s touto grafikou** a potom na záver ju **vymeniť za vlasnú**.
  
<img src="Images/0.gif?raw=true" alt="Error" width="80%"/>
  
Keď máš projekt stiahnutí, [odzipuj](https://www.youtube.com/watch?v=XAFwU2BQwHE) si ho na miesto kde ho chceš mať uložený a otvor si ho pomocou Unity Hubu. Ak máš nainštalovaných viacero verzii daj pozor aby si ju otvoril v tej 2021. 
  
<img src="Images/01.gif?raw=true" alt="Error" width="80%"/>
  
Posledný krok je otvoriť si scénu **Level1**.
  
<img src="Images/02.gif?raw=true" alt="Error" width="80%"/>

## Pohyb hráča <a name="movement"></a> <img align="left" alt="hemisfera.sk" width="32px" src="Images/player.png?raw=true" />
Poďme si rozpohybovať hráča. Nájdime si, kde v projekte máme objekt hráča uložený. Mal by sa nachádzať v **priečinku prefabs**. Následne si ho rozklikneme možnosťou **open prefab**. Tento krok je dôležitý, **nepreskakuj ho!** Keďže ide o hru s pohľadom zhora, tak hráč by sa mal vedieť hýbať do všetkých smerov.  
 
>**_Prefab_** je ako uložená herná šablóna pomocou ktorej vieme do levelu vkladať objekty ako sú mince, hráč, nepriatelia. Keby sme túto šablónu nepoužívali, tak všetko čo si naprogramoval napríklad jednej minci, by si musel všetkým iným minciam naprogramovať a ponastavovať znovu.
  
Pridajme hráčovi nový komponent typu Script machine, nazvime ho Player a uložme si tento graf do súboru.
  
<img src="Images/1.gif?raw=true" alt="Error" width="80%"/>
  
**Otvorme si graf** vo Visual Scripting editore a hurá! Môžeme sa pustiť do kódenia.
 >**_Tip 1: Zoom:_** Pomocou dvojkliku vo visual editor zóne si vieš zväčšiť alebo zmenšiť okno v ktorom sa tvorí vizuálny skript. Pomôže ti to ak budeš tvoriť rozsiahlé skripty.

<img src="Images/2.gif?raw=true" alt="Error" width="80%"/>

Ako prvé musíme detekovať, kedy hráč stlačil klávesy na pohyb postavy. Najlepši spôsob je použiť príkaz **Get Axis Raw**. V ňom upresníme, či sa chceme snímať **horizontálny**(vľavo-vpravo) alebo **vertikálny**(hore-dole) pohyb. V našom prípade chceme oba typy sledovať, pretože hráč sa vie pohybovať do všetkých smerov.

>**_Príkaz: GetAxisRaw("Horizontal")_** funguje tak, že ak je stlačená šípka vpravo, tak príkaz da výslednu hodnotu 1. Naopak ak je stlačená šípka  vľavo, tak príkaz da výslednu hodnotu -1. To je pre nás užitočné lebo hodnotu použijeme na posun po X osy. Rovnako to platí pre vertikálny smer.

>**_Príkaz: Vector3 Create_** nám vytvorí Vektor, ktorí hovorí o **smere a veľkosti** posunu pre ľubovolný herný objekt. Používať ho budeme vždy keď budeme chcieť hýbať objektami. 
  
Výsledok príkazov si uložíme do nového **Vectoru3**(alebo Vectoru2, aj ten by fungoval správne, keďže robíme 2D hru).

<img src="Images/p1.gif?raw=true" alt="Error" width="80%"/>

Teraz keby si zavrel visual scripting okno a vrátil sa do hernej scény, môžeš hru pustiť. Všimni si, že hráč sa vie hýbať do všetkých smerov, akurat sa hýbe príšerne pomaly. Rýchlosť pohybu závisi od veľkosti vektora, ktorý posunieme do komponentu **RigidBody2D** *Set Velocity*. My mu teraz posúvame hodnoty -1, 1 poďla toho aké klávesy su stlačené.

>**_Component RigidBody2D_** je spôsob akým vieme povedať nástroju Unity aby aplikoval fyzikálne pravidlá na daný herný objekt. My ho využívame iba na to aby sme mu priradili rýchlosť a pohli hráčom v danom smere pokiaľ nám neprekáža nejaký pevný objekt. V inom type hry by mohli byť užitočne aj iné vlastnosti *Rigidbody* komponentu ako gravitácia(napríklad pri platformer hre) alebo hmotnosť(pri zrážke dvoch rovnako rýchlych objektov odletí ďalej ten čo ma menšiu hmotnosť).
  
<img width="25%" src="Images/rigdbody.PNG?raw=true" />

Ak chceme hráča zrýchliť, prenásobme hodnoty *Vectora3* napríklad číslom 3. Uvidíme podstatné zrýchlenie. 
  
Dobrou praxou je si hodnotu 3 ktorou chceme prenásobiť rýchlosť hráča uložiť do **hernej premennej**. Tú nazveme napríklad **speed**. Ak by niekto pozeral náš skript tak bude lepšie rozumieť slovu speed ako náhodnemu číslu 3. Predtým ako vytvoríme premennú, povieme si aké typy v Unity používame:
  
**Typy premenných:**
- **Float** predstavuje desatinné čísla naprílad: 0.5, -0.123, 1669, ...
- **Integer** predstavuje celé čísla: -1, 0, 1, 2, 3...
- **String** predstavuje textové reťazce: "Hello, World!", "Flying type", "Walking type" ...
- **Boolean** predstavuje logické hodnoty *True* alebo *False*. 
- **Iné:** Unity nám dovoľuje vytvárať premenné aj komplikovanejších typov ako napríklad *Vector3*, *GameObject*...

>**_Tip 2: Zrušenie prepojenia v grafe:_** ak chceš **zrušiť prepojenie** dvoch príkazov, tak jednoducho klikni **pravým tlačidlom myšky** na začiatok alebo koniec prepájacej čiary.

>**_Tip 3: Pomenovanie premenných:_** prográmatori sa dohodli, že herné premenné budú vždy nazývať malým písmenom. Ak ide o zloženie slov napríklad *playerLife*, tak prvé slovo je malým písmenom a každé ďaľšie slovo začína veľkým. Medzeri v názve nesmú byť!
  
<img src="Images/p2.gif?raw=true" alt="Error" width="80%"/>
  
Rýchlosť hráča máme vyriešenú, pokiaľ chceš možeš mu zmeniť hodnotu rýchlosti podľa pocitu. Ešte takým vizuálnym vylepšením by bolo otočiť obrázok hráča do smeru v ktoróm sa pohybuje. Najlepší spôsob riešenia je použitím komponentu **Sprite Renderer**. A to pomocou premennej **Flip X**. Ak hodnotu premennej označíš v editore ako pravdivú, hráčová postava sa bude pozerať opačným smerom.
  
<img width="25%" src="Images/sprite.PNG?raw=true" />
  
Teraz podobnú vec spravíme vo visual scripte. Pomocou príkazu **if** rozdelíme hlavný tok programu na vetvu v ktorej hráč kráča smmerom vľavo a vetvu v ktorej kráča vpravo. Aby program vedel podľa čoho si má vetvu vybrať tak porovnáme veľkosť **X súracnice** vektoru pohybu s hodnotou 0. Porovnávanie vieme spraviť príkazom *less* alebo *greater*. **Výsledok porovnania** potom vložíme ako vstup do príkazu **if**.
  
<img src="Images/p3.gif?raw=true" alt="Error" width="80%"/>

>**_Tip 4: Kopírovanie príkazov:_** najľahší spôsob ako kopírovať je pomocou **označenia príkazu na kopírovanie** a klávesovej skratky **Ctrl + D**.

### Bonus 
Základ pohybu už by sme mali, ale ak ho chceš vylepšit, tak ešte musíme opraviť jednu chybu. Keď sa postava hýbe diagonálnym smerom(napr. vľavo hore) tak sa hýbe rýchlejšie ako keď sa hýbe iba priamim smerom(vľavo, vpravo, hore, dole). Na to sa používa technika nazývaná [normalizácia vektora](https://www.youtube.com/watch?v=oCU8Ew1XTbs). Pointa je, že vektor zmenšíme tak, aby sme **zachovali jeho smer**. Výsledná veľkosť vektora bude vždy 1. Vektor bude mať hodnotu 1 pre priamy pohyb, aj pre diagonálny pohyb. Následne ho jednoducho prenásobime rýchlosťou(premenná speed) a chybu sme odstránili. 

### Výsledný skript:  
<img src="Images/p4.PNG?raw=true" alt="Error" width="80%"/>

## Kľúč <a name="key"></a> <img align="left" alt="hemisfera.sk" width="32px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/key.png?raw=true" />
Ako ďalší herný prvok si naprogramujeme kľúč. Jeho jedinou úlohou je pri dotyku s hráčom otvoriť príslušné dvere a uvoľniť hráčovi cestu. Pre začiatok si **otvoríme prefab kľúča** a pridáme **Script Machine** komponent podobne ako sme robili pri hráčovi.
  
<img src="Images/k0.gif?raw=true" alt="Error" width="80%"/>
  
Pre detekovanie dotyku kľuča s hráčom použijeme udalosť **On Trigger Enter 2D**. Takýto typ udalosti vzniká ak sa dotknú dva herné objekty a aspoň jeden z nich ma **collider** typu **trigger**. Trigger vpodstate znamená, že cez herný objekt sa dá prechádzať a pri prechode sa aktivuje spomenutá udalosť. 

<img src="Images/Trigger.PNG?raw=true" alt="Error" width="30%"/>

>**_Component Collider2D:_** Ak do hernej scény vložíme ľubovolný obrázok kameňa, slnka, hocičoho, nemôžeme čakať, že Unity bude samo od seba vedieť či ide o pevný objekt alebo len o grafiku, ktorá vypĺňa pozadie. Aby sme vedeli pevné objekty odlíšiť musíme objektu pridať *Collider2D*. Tento komponent vie mať rôzne tvary, ktoré nám pomáhaju približne ohraničiť herný objekt. Najčastejšie nám však stačí tvar krabice(BoxCollider2D), lebo je efektívny pre náš processor. V tomto projekte su collideri pridané za teba, však vo vlastnej hre si ich musíš popridávať sám. 
    
Udalosť **On Trigger Enter 2D** nám na výstupnom bode ponúka informáciu o tom, aký objekt narazil do kľuča. My sa chceme spýtať, či sa objekt, ktorý do nás narazil volá Player. Na identifikáciu sa v Unity nezvykne používať meno objektu, ale existuje niečo ako **tag**. Totiž dva objekty nemôžu mať rovnaké meno, môžu však byť označené jedným tágom. Ak by sme sa pozreli na hráčov objekt tak jeho tag vidíme tu:

<img src="Images/tag.PNG?raw=true" alt="Error" width="30%"/>
  
Keď spojíme všetky tieto znalosti a doplníme ešte príkaz pre zničenie objektu, tak vieme vytvoriť následovný skript pre kľuč:
  
<img src="Images/k1.PNG?raw=true" alt="Error" width="80%"/>
  
Teraz keď hráč narazí na kľuč, tak by sa mal zničiť. Druhá časť je zničenie dverí. Každým kľučom chceme ovoriť(zničiť) dvere do ktorých kľuč pasuje. Preto musíme vedieť priradiť herný objekt dverí. Vieme to spraviť tak, že vytvoríme **Object Variable**. Je to rovnaká premenná ako sme použili na rýchlosť v hráčovi, akurát ju vieme nastavovať zvlášť pre každý objekt. 

<img src="Images/k2.gif?raw=true" alt="Error" width="80%"/>
  
Priradenie dverí spravíme priamo v hernej scéne. Naštastie máme herné objekty dobre pomenované tak jednoducho každému kľúču priraď dvere s rovnakým číslom. Postup najdeš tu:
  
<img src="Images/k3.gif?raw=true" alt="Error" width="80%"/>
  
Správne priradenie si otestuj a ak si nikde nesparavil chybu tak kľuč máš hotoví!

### Výsledný skript:  
<img src="Images/k4.PNG?raw=true" alt="Error" width="80%"/>
  
>**_Tip 5: Warning:_** príkaz **Game Object Destroy** je žltou farbou označený preto, že ide o varovanie. Varovanie neznamená, že ide nutne o chybu, ale že si máme dať pozor, lebo by chyba mohla nastať. Varuje nás preto, lebo hodnota premennej *dvere* **nie je definovaná**. Ak by sme v editore nepriradili ku každému kľuču jeho dvere, tak by nám Script Machine pre daný kľúč ohlásíl chybu a nastal by v hre **bug**(slovíčko pre nežiadané alebo chybné správanie).
## Coin <a name="coin"></a> <img align="left" alt="hemisfera.sk" width="32px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/coin.png?raw=true" />

Našou ďaľšou úlohou je spraviť si zberateľný coin. Coin bude predstavovať hráčové skóre a jeho cieľom bude nie len prejsť level, ale aj pozbierať čo najviac mincí. Aby sme začali, tak nájdi si coin prefab v priečinku Prefabs. Otvor ho a podobne, ako v predchádzajúcich prípadoch ho edituj. Vytvor **Script Machine** komponent a nový graf s názvom **coin**.
  
<img src="Images/c0.PNG?raw=true" alt="Error" width="80%"/>
    
Kolíziu coinu a hráča vyriešime podobne ako kľúč. Ak ľubovolny objekt narazí do coinu, tak skontrolujeme, či jeho tag je *Player*. Ak áno tak coin zničíme. 
  
<img src="Images/c1.PNG?raw=true" alt="Error" width="80%"/>
  
Aby sme vedeli coiny ukladať a zobrazovať hráčovi potrebujeme dve premenné. Prvá bude **coinTxt** a bude typu Text. **Text** je objekt ktorý nám umoňuje zobrazovať texty na hernú obrazovku. Druhá premenná bude **coins** a bude typu **Integer**. Špecialitou tejto premennej je to, že ju spravvíme ako **Scene Variable**. Takýmto spôosobom ju budu vedieť zdieľať všetky objekty v danom levely. My ju potrebujeme, aby sme ju mohli zdielať pre každý coin.
  
<img src="Images/c2.gif?raw=true" alt="Error" width="30%"/>
  
Teraz musíme priradiť Text vytvorený v našej scéne do premennej **coinTxt**. Daný text nájdeš ak si rozklikneš objekt Canvas. **Canvas** sa v Unity používa vždy keď chceme zobraziť tlačidlá, texty, ikonky a podobne. Jeho výhoda je okrem iného, že sa vie prispôsobiť veľkosti hernej obrazovky, ale aj, že počas pohybu hráča zostávajú zobrazené texty nehybné.
  
<img src="Images/c3.PNG?raw=true" alt="Error" width="80%"/>
  
Herný objekt textu nájdeme pomocou príkazu **Game Object Find** a z neho získame samotný Text pomocou **Get Component**, kde **type = Text**. Následne si hodnotu uložíme do premennnej coinText, ktorú sme si v minulom kroku vytvorili. 

>**_Príkaz: Get Component:_** Tento príkaz budeš časom používať často. Každý herný objekt je v Unity zložený z kombinácie komponentov ako **Transform** na uloženie pozície objektu v scéne, **Sprite Renderer** na vykreslenie 2D grafiky, **Rigidbody2D** na aplikovanie fyziky a výnimkou nie je ani **Text** na zobrazenie textov. Ak chceme meniť vlasnosti ľubovolného komponentu z herného objektu, vieme si komponent získať pomocou tohto príkazu a následne s nim pracovať ako potrebujeme.
  
<img src="Images/c4.gif?raw=true" alt="Error" width="80%"/>
  
Ostáva nám spraviť samotné propočítanie získanej mince do celkového počtu mincí. Proces je trochu komplikovaný, pretože musíme: 
1. získať súčasný počet mincí a pripočítať hodnotu 1,
2. uložiť nový počet mincí do premennej coins,
3. konvertovať číselnu hodnotú mincí na string(textový reťazec),
4. uložiť vytvorený string do Textu aby ho hráč videl.
  
<img src="Images/c5.gif?raw=true" alt="Error" width="80%"/>
  
Ak všetko spravíš správne, tak máme hotovo a vieme zbierať mince. :)

### Výsledný skript:  
<img src="Images/c6.PNG?raw=true" alt="Error" width="80%"/>

## Pasca <a name="trap"></a> <img align="left" alt="hemisfera.sk" width="32px" src="Images/trap.png?raw=true" />
Zatiaľ pre hráče v hre neexistuje žiadna hrozba a to je na čase zmeniť. Poďme si vytvoriť pascu, ktorá sa striedavo aktivuje a deaktivuje v časovom intervale. Nájdi si **trap prefab**, otvor ho, pridaj mu Script Machine component a môžeme editovať. 
  
Ako prvé spravíme animáciu. O animácie sa v Unity stará component s názvom **Animator**. My už ho máme v pasci pridaný a nastavili sme mu aj jednotlivé animácie. Tvojou úlohou je iba prepínať animácie pomocou premennej **isActive**, ktorú som ja ako tvorca návodu vytvoril v animátore. Ak je premmená **isActive** typu **bool** nastavená na hodnotu *True*, tak sa zapne animácia **TrapOn**, naopak ak je hodnota premennej *False* tak pasca sa sa prepne do **TrapOff**.
  
<img src="Images/t0.PNG?raw=true" alt="Error" width="80%"/>

>**_Component Animator:_** funguje ako správca všetkých animácii, ktoré vytvoríme pre daný herný objekt. Ide o podobný typ grafu ako používame pri Visual scriptingu, akurat miesto príkazov hovoríme o **stavoch**. V Každom stave je herný objekt v nejakej animácii. Šípky medzi stavmi sú prechody a je v nich definované, že kedy sa ma animácia zmeniť a aké su možnosti. Ak si rozklikneš šípky v našom animátore uvidíš že je na nich podmienka s premennou **isActive**.

Prepínanie animácie chceme robiť napríklad každé 3 sekundy. Preto si chceme vedieť v Unity sledovať, že kedy tie 3 sekundy prešli. Najjednoduchší spôsob je vytvoriť si pomocnú premennú **timePassed** typu *float* a čas si budeme ukladať do nej.  
    
    
<img src="Images/tp.PNG?raw=true" alt="Error" width="30%"/>
  
Ak používame funkciu **On Update** tak na počítanie prejdeného času môžeme použiť príkaz **Time Get Delta Time**. Ten nám vráti čas od posledného vykonania všetkých príkazov v **On Update**. Ten sa vykonáva zvyčajne od 60 do 120 krát za sekundu. Záleži aký máme výkonný počítač. Cele počítanie času vyzerá takto:
  
<img src="Images/t1.PNG?raw=true" alt="Error" width="80%"/>
  
Teraz môžeme pomocou príkazov **greater** a **if** kontrolovať či už prešlo viac ako 3 sekundy. Ak prešli, tak zmeníme animáciu a zresetujeme napočítanú hodnotu v **timePassed** na 0. 
   
<img src="Images/t2.PNG?raw=true" alt="Error" width="80%"/>
     
Túto sa skript pre pascu končí. Ostáva však spraviť **kolíziu hráča s pascou** a **hráčovVo u smrť**. Túto časť by sme vedeli spraviť tiež ako súčasť skriptu pre pascu, ale ak použijeme vhodný tag("Enemy") a naprogramujeme to do hráčového skriptu, tak bude vedieť hráča zabiť akýkoľvek herný objekt s týmto označením. Automaticky keď potom spravíme pohybujúceho sa nepriateľa, tak zabije hráča pri dotyku. Vytvor a nastav teda pasci tag Enemy ak ho už nema nastavený.

<img src="Images/t3.PNG?raw=true" alt="Error" width="30%"/>

  
Otvor hráčov skript a pridajme novu udalosť **On Trigger Enter 2D**.
1. Porovnáme či hráč narazil na objekt s tagom *Enemy*. 
2. Pridáme podmienku **if** aby sme program rozdelili na vetvu kedy hráč do nepriateľa narazil a vetvu kedy nenarazil. 
3. Vo vetve **True** reštartujeme scénu pomocou **Scene Managera** a príkazu **Load Scene**. 
4. Ako vstup do príkazu **Load Scene** vložíme meno aktívnej scény, teda levelu v ktorom sa hráč aktúalne nachádza. Takto zariadíme reštart správnej sceny. Použijeme príkazy **Get Active scene** a **Get Name**.
5. Otestujeme, či všetko správne funguje a máme hotovo!
  
Ak si všimneš tak pasca hráča zabije iba keď je aktivovaná, pritom mi sme nič takéto neprogramovali. Pointa je v tom, že v samotnej animácii sme nastavili collider tak aby pri obrázku bez ostňov bol collider pasce vypnutý a v obrázku s ostňami zapnutý. Týmto spôsobom sme ti zjedodušili tvoj kód. 

>**_Component Scene Manager:_** slúži v Unity na prepínanie sa medzi scénami. Najčastejšie ho budeš využívať iba na získanie informácii o aktívnej scéne alebo na prepínanie sa medzi scénami.

### Výsledný skript:  
Doplnok do **player** scriptu:
  
<img src="Images/t4.PNG?raw=true" alt="Error" width="80%"/>
  
Samotný kód pre **pascu**: 
  
<img src="Images/t2.PNG?raw=true" alt="Error" width="80%"/>

Zvyšok návodu je ešte v procese výroby. Ak už máš všetko hotové tak skus do hráča pridať podmienku aby ho kontakt s pascou zabil. Rada: použi on Trigger enter 2D. Ak nastane kontakt tak znovu načítaj level. Prípadne skus spraviť aby nefungovali všetky pasce naraz, ale každá mala svoj vlasný počiatočný čas a maximálny čas.
