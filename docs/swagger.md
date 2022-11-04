# Tartalomjegyzék:
- [Auth](#Auth "Auth swagger leírása")
- [UserProfile](#UserProfile "UserProfile swagger leírása")

## Auth

- **register**
  -  username: 8-20 karakter hosszúság közötti string (Nem egyedi.).
  -  email: Egyedi, kötelező email formátumnak lennie (Még nem ellenőrzi, hogy létező email cím-e.).
  -  password: Egy jelszó, aminek minimum 8 és maximum 20 karakternek kell lennie.
  -  confirmPassword: Meg kell egyeznie a "password"-del.

- **login**
  -  email: Az adatbázisban szereplő email.
  -  password: A regisztrálásnál megadott jelszó.
  -  Nem engedi belépni a felhasználót, ha nincs "verify"-olva az accountja.

- **verify**
  -  token: A regisztrációkor kapott token. 
  -  (Ha nincs hozzáférése az adatbázishoz, akkor "login"-kor kiírja a "token"-ét egyelőre, hogy tesztelhesse. ***A token másolásakor a mondatvégi írásjelet ne másolja ki!*** Ezt az adatot későbbi fejlesztésben emailben fogjuk elküldeni magának egy linkként, ami automatikusan "verify"-olja az accountját.)

- **forgot-password**
  -  email: Az adatbázisban szereplő email.
  -  (Ha nincs hozzáférése az adatbázishoz, akkor a "forgot-password" "Response body"-ában kiírja a "token"-t, hogy tudja használni a "reset-password"-nál. Ezt az adatot későbbi fejlesztésben emailben fogjuk elküldeni magának.)

- **reset-password**
  -  token: A "forgot-password"-ből kapott "token". A token 1 napig érvényes, addig lehet felhasználni.
  -  password: Egy jelszó, aminek minimum 8 és maximum 20 karakternek kell lennie.
  -  confirmPassword: Meg kell egyeznie a "password"-del.

## UserProfile

- **set-data**
  -  email: A fiók email címe. (Később a bejelentkezett fióktól magától lekéri az oldal, egyelőre be kell gépelni.)
  -  weight: 20 és 1000 között a testsúly kg-ban megadva.
  -  height: 40 és 250 között a testmagasság cm-ben megadva.
  -  birthDate: A születési dátuma "-"-kel elválasztva. Pl.: 2001-01-31. A dátum megadásánál kötelező olyat megadni, amely alapján 12 és 100 év közötti a felhasználó.
  -  gender: 1-3 között a nem (male, female, other). A 0 a nondefined, amikor olyan hiba üzenetet küld a program, hogy kötelező választani. (Az ellenőrzésért egyelőre kiírja a "Response body", hogy mi az adatbázisban szereplő neme.)
  -  goalWeight: A cél testsúly 20 és 1000 között kg-ban megadva. (Amennyiben nem adja meg, a program meghatározza a magának megfelelőt az adatai alapján. Az ellenőrzésért egyelőre kiírja a "Response body", hogy mi az adatbázisban szereplő goalWeight.)
  -  Minden adat kitöltése kötelező az első alkalommal, a többi esetben csak azok az adatok kerülnek módosításra, amelyeket kitöltött. 
