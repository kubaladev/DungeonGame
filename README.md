# Dungeon Crawler VS tutorial od [Hemisfera](https://www.hemisfera.sk). [<img align="right" alt="hemisfera.sk" width="128px" src="Images/logo.png?raw=true" />](https://www.hemisfera.sk)
  
Vitaj herný tvorca, vítam ťa vo svete Unity. Tento návod ti pomôže vytvoriť vlastnú 2D hru žánru [Dungeon Crawler](https://www.youtube.com/watch?v=FQed13kgHSE). Hráč ovláda hrdinu, ktorý sa ocitol v mysterióznej jaskyni plnej nástrah a nepriatelov. Naprogramuj ho tak, aby sa mu podarilo z jaskyne dostať a zároveň, aby to pre teba ako hráča bola výzva.
  
Ak sa zasekneš alebo si nebudeš v niektorej časti istý, tak neváhaj spýtať sa lektora alebo jedného z tvojích spolužiakov. **Držíme ti palce!**
## Inštalácia
Aby si mohol začať programovat, tak potrebuješ mať stiahnuté unity, **verziu 2021** alebo novšiu. Ak ešte Unity nemáš tak urob tak na [tomto linku](https://unity.com/download). Keby máš s inštaláciou problémy, tak skús si pozrieť [toto video](https://www.youtube.com/watch?v=9IKSJdNqzWg).
  
Ďalším krokom je stiahnuť si projekt z github stránky. Takto nebudeš musiet nahadzovať grafiku, objekty do hernej scény a môžeš sa sústrediť na programovanie. V prípade, že máš grafiku vlastnú, tak **odporúčam ti aj tak si spraviť najprv všetko s touto grafikou** a potom na záver ju **vymeniť za vlasnú**.
  
<img src="Images/0.gif?raw=true" alt="Error" width="75%"/>
  
Keď máš projekt stiahnutí otvor si ho pomocou Unity Hubu. Ak máš nainštalovaných viacero verzii daj pozor aby si ju otvoril v tej 2021. 
  
<img src="Images/01.gif?raw=true" alt="Error" width="75%"/>
  
Posledný krok je otvoriť si scénu **Level1**.
  
<img src="Images/02.gif?raw=true" alt="Error" width="75%"/>

## Pohyb hráča <img align="right" alt="hemisfera.sk" width="32px" src="Images/player.png?raw=true" />
Poďme si rozpohybovať hráča. Nájdime si, kde v projekte máme objekt hráča uložený. Mal by sa nachádzať v **priečinku prefabs**. Následne si ho rozklikneme možnosťou **open prefab**. Tento krok je dôležitý, **nepreskakuj ho!** Keďže ide o hru s pohľadom zhora, tak hráč by sa mal vedieť hýbať do všetkých smerov.  
 
>**_Prefab_** je ako uložená herná šablóna pomocou ktorej vieme do levelu vkladať objekty ako sú mince, hráč, nepriatelia. Keby sme túto šablónu nepoužívali, tak všetko čo si naprogramoval napríklad jednej minci, by si musel všetkým iným minciam naprogramovať a ponastavovať znovu.
  
Pridajme hráčovi nový komponent typu Script machine, nazvime ho Player a uložme si tento graf do súboru.
  
<img src="Images/1.gif?raw=true" alt="Error" width="75%"/>
  
**Otvorme si graf** vo Visual Scripting editore a hurá! Môžeme sa pustiť do kódenia.
 >**_Tip 1: Zoom:_** Pomocou dvojkliku vo visual editor zóne si vieš zväčšiť alebo zmenšiť okno v ktorom sa tvorí vizuálny skript. Pomôže ti to ak budeš tvoriť rozsiahlé skripty.

<img src="Images/2.gif?raw=true" alt="Error" width="75%"/>

Ako prvé musíme detekovať, kedy hráč stlačil klávesy na pohyb postavy. Najlepši spôsob je použiť príkaz **Get Axis Raw**. V ňom upresníme, či sa chceme snímať **horizontálny**(vľavo-vpravo) alebo **vertikálny**(hore-dole) pohyb. V našom prípade chceme oba typy sledovať, pretože hráč sa vie pohybovať do všetkých smerov.

>**_Príkaz: GetAxisRaw("Horizontal)_** funguje tak, že ak je stlačená šípka vpravo, tak príkaz da výslednu hodnotu 1. Naopak ak je stlačená šípka  vľavo, tak príkaz da výslednu hodnotu -1. To je pre nás užitočné lebo hodnotu použijeme na posun po X osy. Rovnako to platí pre vertikálny smer.

>**_Príkaz: Vector3 Create_** nám vytvorí Vektor, ktorí hovorí o **smere a veľkosti** posunu pre ľubovolný herný objekt. Používať ho budeme vždy keď budeme chcieť hýbať objektami. 
  
Výsledok príkazov si uložíme do nového **Vectoru3**(alebo Vectoru2, aj ten by fungoval správne, keďže robíme 2D hru).

<img src="Images/p1.gif?raw=true" alt="Error" width="75%"/>

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
  
<img src="Images/p2.gif?raw=true" alt="Error" width="75%"/>
  
Rýchlosť hráča máme vyriešenú, pokiaľ chceš možeš mu zmeniť hodnotu rýchlosti podľa pocitu. Ešte takým vizuálnym vylepšením by bolo otočiť obrázok hráča do smeru v ktoróm sa pohybuje. Najlepší spôsob riešenia je použitím komponentu **Sprite Renderer**. A to pomocou premennej **Flip X**. Ak hodnotu premennej označíš v editore ako pravdivú, hráčová postava sa bude pozerať opačným smerom.
  
<img width="25%" src="Images/sprite.PNG?raw=true" />
  
Teraz podobnú vec spravíme vo visual scripte. Pomocou príkazu **if** rozdelíme hlavný tok programu na vetvu v ktorej hráč kráča smmerom vľavo a vetvu v ktorej kráča vpravo. Aby program vedel podľa čoho si má vetvu vybrať tak porovnáme veľkosť **X súracnice** vektoru pohybu s hodnotou 0. Porovnávanie vieme spraviť príkazom *less* alebo *greater*. **Výsledok porovnania** potom vložíme ako vstup do príkazu **if**.
  
<img src="Images/p3.gif?raw=true" alt="Error" width="75%"/>

>**_Tip 4: Kopírovanie príkazov:_** najľahší spôsob ako kopírovať je pomocou **označenia príkazu na kopírovanie** a klávesovej skratky **Ctrl + D**.

### Bonus 
Základ pohybu už by sme mali, ale ak ho chceš vylepšit, tak ešte musíme opraviť jednu chybu. Keď sa postava hýbe diagonálnym smerom(napr. vľavo hore) tak sa hýbe rýchlejšie ako keď sa hýbe iba priamim smerom(vľavo, vpravo, hore, dole). Na to sa používa technika nazývaná [normalizácia vektora](https://www.youtube.com/watch?v=oCU8Ew1XTbs). Pointa je, že vektor zmenšíme tak, aby sme **zachovali jeho smer**. Výsledná veľkosť vektora bude vždy 1. Vektor bude mať hodnotu 1 pre priamy pohyb, aj pre diagonálny pohyb. Následne ho jednoducho prenásobime rýchlosťou(premenná speed) a chybu sme odstránili. 

### Výsledny skript:  
<img src="Images/p4.PNG?raw=true" alt="Error" width="75%"/>

## Kľúč <img align="right" alt="hemisfera.sk" width="32px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/key.png?raw=true" />
Ako ďalší herný prvok si naprogramujeme kľúč. Jeho jedinou úlohou je pri dotyku s hráčom otvoriť príslušné dvere a uvoľniť hráčovi cestu. Pre začiatok si **otvoríme prefab kľúča** a pridáme **Script Machine** komponent podobne ako sme robili pri hráčovi.
  
<img src="Images/k0.gif?raw=true" alt="Error" width="75%"/>
  
Pre detekovanie dotyku kľuča s hráčom použijeme udalosť **On Trigger Enter 2D**. Takýto typ udalosti vzniká ak sa dotknú dva herné objekty a aspoň jeden z nich ma **collider** typu **trigger**. Trigger vpodstate znamená, že cez herný objekt sa dá prechádzať a pri prechode sa aktivuje spomenutá udalosť. 

<img src="Images/Trigger.PNG?raw=true" alt="Error" width="25%"/>

>**_Component Collider2D:_** Ak do hernej scény vložíme ľubovolný obrázok kameňa, slnka, hocičoho, nemôžeme čakať, že Unity bude samo od seba vedieť či ide o pevný objekt alebo len o grafiku, ktorá vypĺňa pozadie. Aby sme vedeli pevné objekty odlíšiť musíme objektu pridať *Collider2D*. Tento komponent vie mať rôzne tvary, ktoré nám pomáhaju približne ohraničiť herný objekt. Najčastejšie nám však stačí tvar krabice(BoxCollider2D), lebo je efektívny pre náš processor. V tomto projekte su collideri pridané za teba, však vo vlastnej hre si ich musíš popridávať sám. 
    
Udalosť **On Trigger Enter 2D** nám na výstupnom bode ponúka informáciu o tom, aký objekt narazil do kľuča. My sa chceme spýtať, či sa objekt, ktorý do nás narazil volá Player. Na identifikáciu sa v Unity nezvykne používať meno objektu, ale existuje niečo ako **tag**. Totiž dva objekty nemôžu mať rovnaké meno, môžu však byť označené jedným tágom. Ak by sme sa pozreli na hráčov objekt tak jeho tag vidíme tu:

<img src="Images/tag.PNG?raw=true" alt="Error" width="25%"/>
  
Keď spojíme všetky tieto znalosti a doplníme ešte príkaz pre zničenie objektu, tak vieme vytvoriť následovný skript pre kľuč:
  
<img src="Images/k1.PNG?raw=true" alt="Error" width="75%"/>
  
Teraz keď hráč narazí na kľuč, tak by sa mal zničiť. Druhá časť je zničenie dverí. Každým kľučom chceme ovoriť(zničiť) dvere do ktorých kľuč pasuje. Preto musíme vedieť priradiť herný objekt dverí. Vieme to spraviť tak, že vytvoríme **Object Variable**. Je to rovnaká premenná ako sme použili na rýchlosť v hráčovi, akurát ju vieme nastavovať zvlášť pre každý objekt. 

<img src="Images/k2.gif?raw=true" alt="Error" width="75%"/>
  
Priradenie dverí spravíme priamo v hernej scéne. Naštastie máme herné objekty dobre pomenované tak jednoducho každému kľúču priraď dvere s rovnakým číslom. Postup najdeš tu:
  
<img src="Images/k3.gif?raw=true" alt="Error" width="75%"/>
  
Správne priradenie si otestuj a ak si nikde nesparavil chybu tak kľuč máš hotoví!

### Výsledny skript:  
<img src="Images/k4.PNG?raw=true" alt="Error" width="75%"/>
  
>**_Tip 5: Warning:_** príkaz **Game Object Destroy** je žltou farbou označený preto, že ide o varovanie. Varovanie neznamená, že ide nutne o chybu, ale že si máme dať pozor, lebo by chyba mohla nastať. Varuje nás preto, lebo hodnota premennej *dvere* **nie je definovaná**. Ak by sme v editore nepriradili ku každému kľuču jeho dvere, tak by nám Script Machine pre daný kľúč ohlásíl chybu a nastal by v hre **bug**(slovíčko pre nežiadané alebo chybné správanie).
## Coin  <img align="right" alt="hemisfera.sk" width="32px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/coin.png?raw=true" />

Našou ďaľšou úlohou je spraviť si zberateľný coin. Coin bude predstavovať hráčové skóre a jeho cieľom bude nie len prejsť level, ale aj pozbierať čo najviac mincí. Aby sme začali, tak nájdi si coin prefab v priečinku Prefabs. Otvor ho a podobne, ako v predchádzajúcich prípadoch ho edituj. Vytvor **Script Machine** komponent a nový graf s názvom **coin**.
  
<img src="Images/c0.PNG?raw=true" alt="Error" width="75%"/>
    
Kolíziu coinu a hráča vyriešime podobne ako kľúč. Ak ľubovolny objekt narazí do coinu, tak skontrolujeme, či jeho tag je *Player*. Ak áno tak coin zničíme. 
  
<img src="Images/c1.PNG?raw=true" alt="Error" width="75%"/>
  
Aby sme vedeli coiny ukladať a zobrazovať hráčovi potrebujeme dve premenné. Prvá bude **coinTxt** a bude typu Text. **Text** je objekt ktorý nám umoňuje zobrazovať texty na hernú obrazovku. Druhá premenná bude **coins** a bude typu **Integer**. Špecialitou tejto premennej je to, že ju spravvíme ako **Scene Variable**. Takýmto spôosobom ju budu vedieť zdieľať všetky objekty v danom levely. My ju potrebujeme, aby sme ju mohli zdielať pre každý coin.
  
<img src="Images/c2.gif?raw=true" alt="Error" width="25%"/>
  
Teraz musíme priradiť Text vytvorený v našej scéne do premmenej coinTxt. Daný text nájdeš ak si rozklikneš objekt Canvas. **Canvas** sa v Unity používa vždy keď chceme zobraziť tlačidlá, texty, ikonky a podobne. Jeho výhoda je okrem iného, že sa vie prispôsobiť veľkosti hernej obrazovky, ale aj, že počas pohybu hráča zostávajú zobrazené texty nehybné.
  
<img src="Images/c3.PNG?raw=true" alt="Error" width="75%"/>
  
