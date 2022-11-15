# Tartalomjegyzék:
- [Authorize](#Authorize "Authorize swagger gomb leírása")
- [Auth](#Auth "Auth swagger leírása")
- [UserProfile](#UserProfile "UserProfile swagger leírása")
- [SocialMedia](#SocialMedia "SocialMedia swagger leírása")

## Authorize
<ins> Az "[Auth](#Auth "Auth swagger leírása")/login"-nál megszerzett jwt token felhasználásával azonosít, a [UserProfile](#UserProfile "UserProfile swagger leírása") funkció e nélkül nem használhatóak.
- Value: bearer + {jwt}
  - pl: 
```
bearer eyJhbGciOiJodHRwOi8vd3d3LnczLm9yZy8yMDAxLzA0L3htbGRzaWctbW9yZSNobWFjLXNoYTUxMiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiYXNkYXNkYXNkIiwiaHR0cDovL3NjaGVtYXMueG1sc29hcC5vcmcvd3MvMjAwNS8wNS9pZGVudGl0eS9jbGFpbXMvZW1haWxhZGRyZXNzIjoiYXNkYXNkYXNkQGV4YW1wbGUuY29tIiwiZXhwIjoxNjY4MjcyNzIzfQ.UXgKUu0ROArdKc2Rjw1pzuh1dXvlvJ6O9bFJmVrtX4t4So4tA1RfnxaANo7tM8kGYSSNJlCq-LJNRSw9XpT15w
```

## Auth

- **register**
  -  <ins> Felveszi a megadott adatokat az adatbázisba. A megadott email címre küld egy HTML email-t, ahol a "verify" gombbra kattintva visszaigazolhatja az emailjét. ***Ha nem találja a levelet, akkor nézze meg a "Spam"-ek között is!***
  -  username: 8-20 karakter hosszúság közötti string (Nem egyedi.).
  -  email: Egyedi, kötelező email formátumnak lennie (Még nem ellenőrzi, hogy létező email cím-e.).
  -  password: Egy jelszó, aminek minimum 8 és maximum 20 karakternek kell lennie.
  -  confirmPassword: Meg kell egyeznie a "password"-del.

- **login**
  -  <ins> Generál egy jwt tokent, amiben a felhasználó email címe és neve szerepel.
  -  email: Az adatbázisban szereplő email.
  -  password: A regisztrálásnál megadott jelszó.
  -  Nem engedi belépni a felhasználót, ha nincs "verify"-olva az accountja.

- **verify**
  -  <ins> Elmenti a visszaigazolás időpontját.
  -  token: A regisztrációkor kapott token. 
  -  (Ha nincs hozzáférése az adatbázishoz, és nem találta meg a regisztrációkor kapott emailt, akkor "login"-kor kiírja a "token"-ét egyelőre, hogy tesztelhesse. ***A token másolásakor a mondatvégi írásjelet ne másolja ki!***)

- **forgot-password**
  -  <ins> Generál egy verification token-t, majd azt és annak a lejárati dátumát elmenti az adatbázisba.
  -  email: Az adatbázisban szereplő email.
  -  (Ha nincs hozzáférése az adatbázishoz, akkor a "forgot-password" "Response body"-ában kiírja a "token"-t, hogy tudja használni a "reset-password"-nél. Ezt az adatot későbbi fejlesztésben emailben fogjuk elküldeni magának.)

- **reset-password**
  -  <ins> Felülírja a jelszót és a hozzátartozó "salt"-ot, majd törli a "forgot-password" által generált tokent és dátumot.
  -  token: A "forgot-password"-ből kapott "token". A token 1 napig érvényes, addig lehet felhasználni.
  -  password: Egy jelszó, aminek minimum 8 és maximum 20 karakternek kell lennie.
  -  confirmPassword: Meg kell egyeznie a "password"-del.

## UserProfile

- **set-data**
  -  <ins> Lekérdezi a jwt-ből a felhasználó email címét, és ezzel azonosítva létrehozza, vagy frissíti az adatait.
  -  weight: 20 és 1000 között a testsúly kg-ban megadva.
  -  height: 40 és 250 között a testmagasság cm-ben megadva.
  -  birthDate: A születési dátuma "-"-kel elválasztva. Pl.: 2001-01-31. A dátum megadásánál kötelező olyat megadni, amely alapján 12 és 100 év közötti a felhasználó.
  -  gender: 1-3 között a nem (male, female, other). A 0 a nondefined, amikor olyan hiba üzenetet küld a program, hogy kötelező választani. (Az ellenőrzésért egyelőre kiírja a "Response body", hogy mi az adatbázisban szereplő neme.)
  -  goalWeight: A cél testsúly 20 és 1000 között kg-ban megadva. (Amennyiben nem adja meg, a program meghatározza a magának megfelelőt az adatai alapján. Az ellenőrzésért egyelőre kiírja a "Response body", hogy mi az adatbázisban szereplő goalWeight.)
  -  Minden adat kitöltése kötelező az első alkalommal, a többi esetben csak azok az adatok kerülnek módosításra, amelyeket kitöltött. 

- **set-profile-picture**
  -  <ins> Lekérdezi a jwt-ből a felhasználó email címét, és ezzel azonosítva frissíti a profilkép beállításait.
  -  hairIndex: 1-5 között a profilképen megjelenő haj. (Blond, brown, ginger, black, white.)
  -  skinIndex: 1-4 között a profilképen megjelenő bőrszín. (Darkest, dark, light, lightest.)
  -  eyesIndex: 1-3 között a profilképen megjelenő szemszín. (Blue, green, brown.)
  -  mouthIndex: 1-3 között a profilképen megjelenő száj. (Happy, neutral, sad.)
  
  ## SocialMedia
  - **follow**
    -  <ins> Használatához a követő és a követendő felhasználónak is rendelkeznie kell egy profillal. Beköveti email alapján az adott felhasználót a bejelentkezett felhasználó által.
    -  email: A bekövetendő felhasználó email címe.
