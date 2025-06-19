<div style="text-align: justify">

# 11. Objektumelvű programozási nyelvek (kiegészítés OEP, EVA, szoftvertechnológia előadásokból)

## Tartalom
[Osztály](#osztály) és [objektum](#objektum).
[Egységbe zárás](#egységbe-zárás), [tagok](#tagok), [konstruktorok](#konstruktorok).
[Információ elrejtése](#információ-elrejtése).
Túlterhelés.
[Memóriakezelés](#memóriakezelés), [szemétgyűjtés](#szemétgyűjtés).
[Öröklődés](#öröklődés), [többszörös öröklődés](#többszörös-öröklődés).
Altípusosság.
Statikus és dinamikus típus, [típusellenőrzés](#típusellenőrzés).
[Felüldefiniálás](#felüldefiniálás), [dinamikus kötés](#dinamikus-kötés).
[Generikusok](#generikusok).
[Altípusos](#altípusos-polimorfizmus) és [parametrikus polimorfizmus](#parametrikus-polimorfizmus).
Objektumok összehasonlítása és [másolása](#objektumok-másolása).

#### **Típus:**
Egy adat (változó) típusának definiálásához szükség van a típus specifikációjára és annak megvalósítására.

A típus-specifikáció megadja az adat által felvehető értékek halmazát (típusértékek) és a típusértékekkel végezhető műveleteket (típusműveletek).

A típus-megvalósítás megmutatja hogyan ábrázoljuk (reprezentáljuk) a típusértékeket és milyen programok helyettesítsék (implementálják) a műveleteket.


#### **Osztály:**
Objektumok típusa. Az osztály egy objektum szerkezetének és viselkedésének a mintáját adja meg, azaz felsorolja az objektum adattagjait azok nevének, típusának, és láthatóságának (rejtett (-,#) vagy publikus (+)) megadásával, kiegészítve az esetleges típusinvariánssal, megadja az objektumra meghívható metódusokat (tagfüggvény, művelet) a nevükkel,  paraméterlistájukkal, visszatérési értékük típusával, törzsükkel, és a láthatóságukkal.

Az osztály lényegében az objektum típusa: az objektumot az osztálya alapján hozzuk létre, azaz példányosítjuk.
Tisztán objektumorientált nyelvek: minden érték bennük objektum (pl. int, string is), és minden típus egy osztály.

Egy osztályhoz több objektum is példányosítható: minden objektum rendelkezik az osztályleírás által leírt adattagokkal és metódusokkal.

Az objektumelvű tervezés során osztályként adjuk meg az egyedi, vagy ún.
felhasználói típusokat.


#### **Objektum:**
Adat és rajta értelmezett alapműveletek. Objektumnak egy feladat megoldásának azon önálló egyedként azonosított részét nevezzük, amely magába foglalja az adott részért felelős adatokat, és az ezekkel kapcsolatos műveleteket.
Egy objektumra - miután azt létrehoztuk (példányosítottuk) - csak közvetett módon, egy változó segítségével tudunk majd hivatkozni.


#### **Egységbe zárás:**
Egy adott feladatkör megvalósításához szükséges adatokat és az azokat manipuláló programrészeket a program többi részétől elkülönítve adhatjuk meg.


#### **Tagok:**
Az osztály tagjai lehetnek mezők, metódusok, események (C#), tulajdonságok (property, C#), illetve más (beágyazott) osztályok.
Minden tagnak, és az osztálynak is jelöljük a láthatóságát (public, private, protected, internal).
Minden tag a `.` operátorral érhető el.

A mezők típusból és névből állnak, illetve kaphatnak kezdőértéket.
A mezők alapértelmezett értéket kapnak, amennyiben nem inicializáljuk őket.

A metódusok visszatérési típussal (amennyiben nincs, akkor void), névvel és paraméterekkel rendelkeznek.


#### **Konstruktorok:**
Az objektum példányosítását (létrehozását) speciális metódus, a konstruktor végzi: memóriát foglal az objektum adattagjai számára (ha egy adattag maga is objektum-hivatkozás, akkor azt is példányosítja), és kezdeti értéket ad az adattagoknak.
A konstruktor neve megegyezik a típussal, a destruktort általában nem valósítjuk meg (szemétgyűjtés miatt).
Ha más konstruktort nem definiálunk, akkor is rendelkezünk egy (paraméter nélküli és üres törzsű) ún. üres konstruktorral.


#### **Információ elrejtése:**
Az egységbe zárt elemek láthatóságának korlátozása (általában az adattagok rejtettek, azok értékéhez csak közvetetten, a publikus metódusokkal férünk hozzá).

Egy objektum rejtett (privát, védett) tagjaira csak az objektum metódusainak törzsében hivatkozhatunk, máshol ezeket közvetlenül nem használhatjuk.


#### **Memóriakezelés:**
Típuskategóriák:
- Érték: érték szerint kezelendő típusok, mindig másolódnak a memóriában, és a blokk végén törlődnek.
- Referencia: biztonságos mutatókon keresztül kezelt típusok, a virtuális gép és a szemétgyűjtő felügyeli és törli őket.
- Mutató (csak C#): nem biztonságos mutatók, amelyek csak felügyeletmentes (unsafe) kódrészben használhatóak.

Az érték szerinti típusok nem vehetnek fel `null` értéket, míg a referencia szerinti típusok igen.


#### **Szemétgyűjtés:**
A referencia szerinti változók törlését a szemétgyűjtő felügyeli.
Adott algoritmussal adott időközönként pásztázza a memóriát, törli a felszabadult objektumokat.

Sok, erőforrás-igényes objektum példányosítása esetén azonban nem mindig reagál időben, így nő a memóriahasználat (C#-ban a GC osztály segítségével beavatkozhatunk a működésbe).

C#-ban manuális törlésre (destruktor futtatásra) nincs lehetőségünk felügyelt blokkban, de erőforrások felszabadítására igen, amennyiben az osztály megvalósítja az IDisposable interfészt, és benne a Dispose() metódust.

A Java és C# nyelv tartalmaz olyan blokk-kezelési technikát, amely garantálja az erőforrás-felszabadítás automatikus futtatását: `try-with-resources` (Java), `using` (C#).


#### **Öröklődés:**
Ha egy objektum más objektumokra hasonlít, azaz azokkal megegyező adattagjai és metódusai vannak, tehát örököli azok tulajdonságait (de azokat akár módosíthatja is, ki is egészítheti), akkor az osztálya a vele hasonló objektumok osztályainak mintájára alakítható ki, azaz belőlük származtatható.

A modellezés során kétféle okból használunk származtatást:
- Általánosítás: már meglévő, egymáshoz hasonló osztályoknak a közös tulajdonságait leíró ősosztályát (szuperosztály) hozzuk létre.
- Specializálás: egy osztályból származtatással hozunk létre egy alosztályt.

Osztályok már meglévő osztályokból származtathatók.
Ősosztály változójának értékül adható az alosztályának objektuma.

Az osztályok egy teljes származtatási hierarchiában vannak: minden osztály őse az Object, így megkapja annak műveleteit.

Absztrakt (abstract) osztály az, amelyből nem példányosítunk objektumokat, hanem kizárólag ősosztályként szolgál a származtatásokhoz.
Egy osztály attól lesz absztrakt, hogy a konstruktorai nem publikusak, vagy legalább egy metódusa absztrakt, azaz nem rendelkezik törzzsel, ezt a származtatás során kell majd megadni.

Interfésznek a tisztán absztrakt (pure abstract) osztályt hívjuk.
Ennek nincsenek adattagjai, és egyetlen metódusának sincs törzse.
Egy interfészből származtatott konkrét osztálynak minden absztrakt metódust implementálni kell: meg kell valósítania az interfészt.

Egy alosztály az ősosztály minden tagját örökli, de csak az ősosztály publikus és védett tagjaira hivatkozhat, a privát tagjaira nem, azokhoz csak indirekt módon, az ősosztálytól örökölt nem-privát metódusokkal férhet hozzá.


#### **Többszörös öröklődés:**
Egy osztálynak (Java, C#) csak egy őse lehet, de bármennyi interfészt megvalósíthat.


#### **Típusellenőrzés:**
Szigorúan típusos nyelv: minden értéknek fordítási időben ismert a típusa, nem enged meg értékvesztést.
Nagyobb halmazra implicit (upcast, altípusosság) típuskonverzió, kompatibilis halmazra explicit típuskonverzió (downcast) használható.


#### **Felüldefiniálás:**
Öröklődés során a műveletek és tulajdonságok felüldefiniálhatóak.
Ha egy ősosztály metódusát a leszármazott osztályban felülírjuk (override), akkor ez a metódus több alakkal is rendelkezik (polimorf).

#### **Dinamikus kötés:**
Mivel egy ősosztály típusú változónak mindig értékül adható alosztálya példányának hivatkozása, csak futási időben derülhet az ki, hogy egy ilyen a változó az ősosztálynak egy példányára vagy alosztályának egy példányára hivatkozik (késői vagy futási idejű vagy dinamikus kötés).


#### **Generikusok:**
Generikus programozásra futási időben feldolgozott sablon típusok (generic-ek) segítségével van lehetőség.
A sablon fordításra kerül, és csak a futásidejű fordításkor helyettesítődik be a konkrét értékre.

A szigorú típuskezelés miatt a sablonra csak az Object-ben értelmezett műveletek használhatóak, ezt a műveletkört növelhetjük megszorításokkal (Java: `<T extends Class>`, C#: `<T> where T : Class`).


#### **Altípusos polimorfizmus:**
Kívánatos, hogy egy felüldefiniált metódus, akár az ősosztály, akár alosztályának egy objektumára hívják is meg, a modellezett feladat elvárásainak megfelelően működjön.
Ősosztály típusú változónak értékül adható az alosztályának objektuma (többalakúság).

Ha egy ősosztály típusú változóra egy polimorf virtuális metódust hívunk meg, akkor e metódusnak azon osztályban definiált változata fut majd le, amilyen osztályú példányra hivatkozik a változó (dinamikus altípusos polimorfizmus).

Liskov substitution principle (LSP): az objektumok felcserélhetők altípusaik példányára a program viselkedésének befolyása nélkül.
Minden altípusnak biztosítania kell az ős funkcionalitását azok feltételeinek betartása mellett.


#### **Parametrikus polimorfizmus:**
Olyan osztály példányosítását is szeretnénk támogatni, amely bizonyos tagjainak típusát szabadon megválaszthatjuk.
Ehhez az osztályt (és reprezentációját is) generikussá alakítjuk: egy típus-paraméterrel jelezzük a tagok típusát.


#### **Objektumok másolása:**
Sekély másolás: a látszólag egymástól független objektumok az értékadás (`obj1 := obj2`) után már azonosak lesznek: ha az egyik változik, vele együtt változik a másik is.

Mély másolás: `Cloneable` (Java), `ICloneable` (C#) interfészek megvalósítása, vagy az osztályok másoló konstruktoraira támaszkodunk.

</div>