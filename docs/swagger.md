# Tartalomjegyzék:
- [Authorize](#Authorize "Authorize swagger gomb leírása")
- [Auth](#Auth "Auth controller leírása")
- [Food](#Food "Food controller leírása")
- [UserProfile](#UserProfile "UserProfile controller leírása")
- [SocialMedia](#SocialMedia "SocialMedia controller leírása")

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
  -  <ins> Visszatér egy jwt tokennel, amiben a felhasználó id-ja és role-ja szerepel.
  -  email: Az adatbázisban szereplő email.
  -  password: A regisztrálásnál megadott jelszó.
  -  Nem engedi belépni a felhasználót, ha nincs "verify"-olva az accountja.

- **verify**
  -  <ins> Elmenti a visszaigazolás időpontját.
  -  token: A regisztrációkor kapott token. 

- **forgot-password**
  -  <ins> Generál egy verification token-t, majd azt és annak a lejárati dátumát elmenti az adatbázisba.
  -  email: Az adatbázisban szereplő email.
  -  (Ha nincs hozzáférése az adatbázishoz, akkor a "forgot-password" "Response body"-ában kiírja a "token"-t, hogy tudja használni a "reset-password"-nél. Ezt az adatot későbbi fejlesztésben emailben fogjuk elküldeni magának.)

- **reset-password**
  -  <ins> Felülírja a jelszót és a hozzátartozó "salt"-ot, majd törli a "forgot-password" által generált tokent és dátumot.
  -  token: A "forgot-password"-ből kapott "token". A token 1 napig érvényes, addig lehet felhasználni.
  -  password: Egy jelszó, aminek minimum 8 és maximum 20 karakternek kell lennie.
  -  confirmPassword: Meg kell egyeznie a "password"-del.

## Food
- **get-recommended-tags**
  -  <ins> Visszatér azon tagek listájával, amit ajánl az adott ételnek.
  -  foodId: Egy az adatbázisban szereplő étel azonosítója.
  
- **create**
  -  <ins> Létrehoz egy ételt.
  -  name: Az étel neve. (5-50 karakter között.)
  -  kcal: Az étel kcal tartalma 100 grammonként, amennyiben a felhasználó nem adja meg, a program kiszámolja automatikusan. (0-100 közötti érték.)
  -  protein: Az étel fehérje tartalma 100 grammonként. (0-100 közötti érték.)
  -  fat: Az étel zsír tartalma 100 grammonként. (0-100 közötti érték.)
  -  carbohydrate: Az étel szénhidrát tartalma 100 grammonként. (0-100 közötto érték.)
  
- **update**
  -  <ins> Módosítja egy az adatbázisban szereplő étel adatait.
  -  id: Az étel azonosítója.
  -  name: Az étel neve. (5-50 karakter között.)
  -  kcal: Az étel kcal tartalma 100 grammonként, amennyiben a felhasználó nem adja meg, a program kiszámolja automatikusan. (0-100 közötti érték.)
  -  protein: Az étel fehérje tartalma 100 grammonként. (0-100 közötti érték.)
  -  fat: Az étel zsír tartalma 100 grammonként. (0-100 közötti érték.)
  -  carbohydrate: Az étel szénhidrát tartalma 100 grammonként. (0-100 közötto érték.)
  
- **verify**
  -  <ins> Egy "Admin" role-lal rendelkező felhasználó hitelesíthet egy ételt.
  -  id: Az étel azonosítója.
  
- **delete**
  -  <ins>  Egy "Admin" role-lal rendelkező felhasználó törölhet egy ételt.
  -  id: Az étel azonosítója.
  
- **add-tags**
  -  <ins> Egy ételhez tag-eket rendel.
  -  foodId: Az étel azonosítója.
  -  tagIds: A tagek azonosítói.
  
## UserProfile

- **create-profile**
  -  <ins> Lekérdezi a jwt-ből a felhasználó email címét, és ezzel azonosítva létrehozza a profilját.
  -  weight: 20 és 1000 között a testsúly kg-ban megadva.
  -  height: 40 és 250 között a testmagasság cm-ben megadva.
  -  birthDate: A születési dátuma "-"-kel elválasztva. Pl.: 2001-01-31. A dátum megadásánál kötelező olyat megadni, amely alapján 12 és 100 év közötti a felhasználó.
  -  gender: 1-3 között a nem (male, female, other).
  -  goalWeight: A cél testsúly 20 és 1000 között kg-ban megadva. (Amennyiben nem adja meg, a program meghatározza a magának megfelelőt az adatai alapján.)
  
- **update-profile**
  - A mezők úgy működnek, mint a "create-profile"-ban, de itt nem kötelező minden mező kitöltése.

- **set-profile-picture**
  -  <ins> Lekérdezi a jwt-ből a felhasználó email címét, és ezzel azonosítva frissíti a profilkép beállításait.
  -  hairIndex: 1-5 között a profilképen megjelenő haj. (Blond, brown, ginger, black, white.)
  -  skinIndex: 1-4 között a profilképen megjelenő bőrszín. (Darkest, dark, light, lightest.)
  -  eyesIndex: 1-3 között a profilképen megjelenő szemszín. (Blue, green, brown.)
  -  mouthIndex: 1-3 között a profilképen megjelenő száj. (Happy, neutral, sad.)
  -  Először minden adat kitöltése kötelező, később csak azok, amiket módosítani akar.
  
## SocialMedia
- **unfollow-follow**
  -  <ins> Használatához a követő és a követendő felhasználónak is rendelkeznie kell egy profillal. Beköveti, ha még nincs, és kiköveti, ha már be van követve email alapján az adott felhasználót a bejelentkezett felhasználó által.
  -  email: A bekövetendő felhasználó email címe.
  
- **write-comment**
  -  <ins> Hozzáfűz egy profilhoz egy hozzászólást, aminek szerzője a bejelentkezett profil, és címzette egy adott felhasználó.
  -  email: Címzett emaile.
  -  Csak olyan felhasználó írhat üzenetet, és csak olyan felhasználónak, aki rendelkezik user profile-lal.
  
- **delete-comment**
  -  <ins> Kitöröl egy commentet.
  -  commentId: A törlendő hozzászólás azonosítója.
  -  Csak a hozzászólás címzettje és írója törölheti azt.
  
- **modify-comment**
  -  <ins> Módosít egy commentet.
    -  commentId: A módosítandó hozzászólás azonosítója.
    -  Csak a hozzászólás írója módosíthatja azt.

- **get-all-comment-by-authenticated-email**
  -  <ins> A bejelentkezett felhasználóhoz címzett hozzászólásokat kilistázza.
  
