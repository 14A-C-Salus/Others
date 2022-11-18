# Specifikációk

## Funkcionális követelmények:

- A weboldalunk egy olyan webalkalmazás, ahol kcal-t tud számolni a felhasználó, recepteket tud készíteni, diétát ütemezni, elérendő célokat kitűzni, mások receptjeit értékelni, követni a naponta bevitt tápanyag mennyiségét. Ezek mellett statisztikák létrehozására, üzenőfalon kommunikálásra nyílik lehetősége. A funkciók használatához regisztráció szükséges, vagyis regisztráció nélkül a szolgáltatások egyike sem elérhető.

- **Kalória számolás**:
  - Már előre létrehozott ételekből is tud választani a felhasználó.
  - A felhasználó képes saját ételeket is elmenteni.
  - Képes a főzési, sütési metódussal járó tápanyag vesztéssel, plusz kalóriákkal is számolni.

- **Receptek készítése**:
  - Az alkalmazás lehetőséget nyújt az elmentett ételek kombinálására,
  - Mások receptjeinek elmentésére, testreszabására.

- **Diéta megadása**:
  - A felhasználó céljainak megfelelően képes a weboldal algoritmusa kiválasztani a számára legmegfelelőbb diétát.
  - A felhasználó saját diétát is megadhat, ebben az esetben a weboldal figyelembe veszi, hogy a diéta alapján milyen ételeket ajánljon.

- **Célok kitűzése**:
  - A felhasználó megadhat elérni kívánt testtömeget, amelyek elérésében az alkalmazás támogatja a felhasználót.
  - Az alkalmazás képes kiszámolni a felhasználó ideális testtömegét, és amennyiben nem tűz ki saját célt, ennek elérésére segít törekedni.

- **Mások receptjeivel interakció**:
  - A felhasználónak lehetősége nyílik mások által írt és publikált receptek letöltésére, kipróbálására, értékelésére, de akár módosítására is.

- **Bevitt tápérték naplózása**:
  - A felhasználó képes az elfogyasztott ételeinek tápértékét elmenteni rövid idő alatt, amit az alkalmazás automatikusan összehasonlít a célja eléréséhez szükséges tápanyag bevitellel, és figyelmeztet, amennyiben az meghaladja azt.
  - Utólag egy gombnyomással képes ezen értékek felezésére, harmadolására, vagy bárminemű módosítására.
  - Az alkalmazás az 5 fő étkezésen kívül 10 egyéb étkezési alkalmat tud egyszerre tárolni.
  - A bevitt tápértéken kívül az alkalmazás a felhasználó által fogyasztott folyadék mennyiségét is elmenti, összeveti a szükséges folyadék bevitellel, amit a folyadékot igénylő tápanyagok bevitele esetén növel.

- **Statisztikák**:
  - Az alkalmazás statisztikát épít testtömegváltozási adataiból, receptjei kedveltségéről és követéseiről is.

- **Üzenőfal**:
  - Mindegyik felhasználónak rendelkezésére áll a saját és mások üzenőfala kommunikációs célra.
  - Ezen üzeneteket a profil tulajdonosa bármikor eltávolíthatja, vagy reagálhat rá.
  - Az üzenőfal működése nagyban hasonlít a közösségi médiáknak köszönhetően jól ismert komment szekciójához, a különbség csupán abban rejlik, hogy itt az adott profilhoz tudja a felhasználó hozzáfűzni megjegyzéseit.

- **Böngészés a receptek között**:
  - A felhasználó elsősorban a hitelesített recepteket, ételeket találja meg keresés során, majd azt követően a mentés száma szerint sorba rendezve az összes többi lehetőséget.

- **Regisztráció**:
  - A weboldal funkcióinak használata regisztrációhoz vannak kötve.

- Az adminisztrátor számára biztosítunk lehetőséget receptek, üzenetek törlésére, amennyiben azok bizonyos előre megszabott feltételeknek nem felelnek meg. Emellett receptek hitelesítésére.

- A weboldalunk célja amellett, hogy a felhasználót segítse az egészséges életmód elérésében, fenntartásában, az az, hogy közösséget építsen ezen életmód köré.

## Nem funkcionális követelmények:

