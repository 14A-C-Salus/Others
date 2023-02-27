<h1 align="center"><b> Backend szolgáltatások </b></h1>
<h2> <u> Dokumentáció az AuthService-hoz: </u></h2>

Ez az osztály az autentikációhoz kapcsolódó funkciókat kezeli a rendszerben.

<b>Metódusok:</b>

-    Register(AuthRegisterRequest request): Ez a metódus egy új felhasználói fiókot hoz létre AuthRegisterRequest objektum bemeneti paraméterrel. Ellenőrzi, hogy az e-mail cím már létezik-e, és kivételt dob, ha igen. Ezután létrehoz egy új Auth objektumot, küld egy token-t, ha a RELEASE módban van, és elmenti az Auth objektumot az adatbázisba. A metódus visszaadja az Auth objektumot.
-    Login(AuthLoginRequest request): Ez a metódus bejelentkezteti a felhasználót AuthLoginRequest objektum bemeneti paraméterrel. Az átadott e-mail alapján lekéri az Auth objektumot, majd ellenőrzi a jelszót. Ha a jelszó helyes, JWT token-t generál, majd visszaadja azt.
-    Verify(string token): Ez a metódus ellenőrzi a felhasználói fiókot a token objektum bemeneti paraméterrel. Az átadott token alapján lekéri az Auth objektumot, frissíti a verifikáció dátumát, majd visszaadja az Auth objektumot.
-    ForgotPassword(string email): Ez a metódus elindítja a jelszó-visszaállítási folyamatot az email objektum bemeneti paraméterrel. Az átadott e-mail alapján lekéri az Auth objektumot, beállítja a visszaállító token-t és annak lejárati idejét, majd visszaadja az Auth objektumot.
-    ResetPassword(AuthResetPasswordRequest request): Ez a metódus visszaállítja a felhasználó jelszavát AuthResetPasswordRequest objektum bemeneti paraméterrel. Az átadott token alapján lekéri az Auth objektumot, ellenőrzi, hogy a token érvényes-e, majd frissíti az Auth objektumot az új jelszóval. A metódus visszaadja az Auth objektumot.

<b>Kivételek:</b>

-    "Username or password is not correct!" - Akkor dobódik, amikor egy felhasználó helytelen felhasználónévvel vagy jelszóval próbál bejelentkezni.
-    "Email already exists." - Akkor dobódik, amikor egy felhasználó olyan email címmel próbál regisztrálni, amely már létezik az adatbázisban.
-    "Not verified! Check your emails and verify your account!" - Akkor dobódik, amikor egy felhasználó bejelentkezni próbál, de a fiókja nincs még ellenőrizve.
-    "Invalid token!" - Akkor dobódik, amikor egy felhasználó érvénytelen tokennel próbálja ellenőrizni a fiókját.
-    "User not found!" - Akkor dobódik, amikor egy felhasználó jelszó visszaállítását kéri, de nincs felhasználó az adott email címhez társítva.
-    "Invalid Token!" - Akkor dobódik, amikor egy felhasználó érvénytelen tokennel próbálja visszaállítani a jelszavát.
-    "Invalid password!" - Akkor dobódik, amikor egy felhasználó túl rövid vagy túl hosszú jelszót próbál beállítani.
-    "Empty auth." - Akkor dobódik, amikor egy üres Auth objektumot adnak át olyan metódusnak, amelyhez szükséges.
-    "Invalid username." - Akkor dobódik, amikor egy Auth objektumban érvénytelen felhasználónév található.
-    "Invalid email." - Akkor dobódik, amikor egy Auth objektumban érvénytelen email cím található.
-    "Invalid email!" - Akkor dobódik, amikor egy felhasználó érvénytelen email címmel próbál regisztrálni.
-    "Invalid confirm password!" - Akkor dobódik, amikor egy felhasználó olyan jelszóval próbál regisztrálni, amely nem egyezik meg a megerősítő jelszóval.

<h2> <u>Dokumentáció a FoodService-hez:</u></h2>

Ez az osztály az ételekkel kapcsolatos funkciókat kezeli a rendszerben.

<b>Metódusok:</b>

-    GetRecommendedTags(int foodId): Ez a metódus egy adott ételelemhez ajánlott címkék listáját kérdezi le, az étel azonosítóját bemenő paraméterként használva. Ellenőrzi, hogy az étel létezik-e, majd lekérdezi a címkéket, amelyek ajánlottak. A metódus a címkék listáját adja vissza.
-    AddTags(AddTagsToFoodRequest request): Ez a metódus címkéket ad hozzá egy adott ételhez, az AddTagsToFoodRequest objektumot bemenő paraméterként használva. Ellenőrzi, hogy az étel létezik-e, majd lekéri a hozzáadandó címkéket. Ezután létrehoz egy új FoodsHaveTags objektumot minden címke esetében és hozzáadja azt az adatbázishoz. A metódus a frissített Étel objektumot adja vissza.
-    Create(FoodCreateRequest request): Ez a metódus egy új ételelemet hoz létre, a FoodCreateRequest objektumot bemenő paraméterként használva. Létrehoz egy új Étel objektumot, beállítja annak attribútumait és ellenőrzi az adatokat. Ezután hozzáadja az Étel objektumot az adatbázishoz és visszaadja azt.
-    Delete(int id): Ez a metódus törli az étel elemet az azonosítója alapján. Ellenőrzi, hogy az étel létezik-e, majd eltávolítja azt az adatbázisból.
-    Update(FoodUpdateRequest request): Ez a metódus frissíti egy ételelemet, a FoodUpdateRequest objektumot bemenő paraméterként használva. Lekéri az étel elemet az azonosítója alapján, frissíti annak attribútumait és ellenőrzi az adatokat. Ezután frissíti az Étel objektumot az adatbázisban és visszaadja azt.
-    VerifyUnVerify(int id): Ez a metódus ellenőrzi vagy érvényteleníti egy étel elemet, az azonosítója alapján. Lekéri az étel elemet az azonosítója alapján, frissíti az érvényesítési állapotát, majd frissíti az Étel objektumot az adatbázisban. A metódus a frissített Étel objektumot adja vissza.

<b>Kivételek:</b>

-    "Food (id:{foodId}) does not exist." - Akkor dobódik, ha az adatbázisban nem található az adott azonosítójú étel, amikor a javasolt címkéit szeretnénk lekérdezni.
-    "This food doesn't exist." - Akkor dobódik, ha az adatbázisban nem található az adott azonosítójú étel, amikor címkéket akarunk hozzáadni, frissíteni, vagy ellenőrizni/ellenőrzetlenre állítani.
-    "This tag ($id={tagId}) doesn't exist." - Akkor dobódik, ha az adatbázisban nem található az adott azonosítójú címke, amikor címkéket akarunk hozzáadni egy ételhez.
-    "This food already have this tag." - Akkor dobódik, ha az étel már rendelkezik ugyanazzal a címkével, amikor címkéket akarunk hozzáadni egy ételhez.
-    "Name can't be longer than 50 characters!" - Akkor dobódik, ha az étel neve 50 karakternél hosszabb, amikor az ételt létrehozzuk vagy frissítjük.
-    "Please enter at least 5 characters to the name field." - Akkor dobódik, ha az étel neve kevesebb, mint 5 karakter, amikor az ételt létrehozzuk vagy frissítjük.
-    "100g food can't contain more than 100g fat." - Akkor dobódik, ha az étel több, mint 100g zsírt tartalmaz 100g-onként, amikor az ételt létrehozzuk vagy frissítjük.
-    "100g food can't contain more than 100g protein." - Akkor dobódik, ha az étel több, mint 100g fehérjét tartalmaz 100g-onként, amikor az ételt létrehozzuk vagy frissítjük.
-    "100g food can't contain more than 100g carbohydrate." - Akkor dobódik, ha az étel több, mint 100g szénhidrátot tartalmaz 100g-onként, amikor az ételt létrehozzuk vagy frissítjük.
-    "Food can't contain less than 0g fat." - Akkor dobódik, ha az étel negatív mennyiségű zsírt tartalmaz, amikor az ételt létrehozzuk vagy frissítjük.
-    "Food can't contain less than 0g protein." - Akkor dobódik, ha az étel negatív mennyiségű fehérjét tartalmaz, amikor az ételt létrehozzuk vagy frissítjük.
-    "Food can't contain less than 0g carbohydrate." - Akkor dobódik, ha az étel negatív mennyiségű szénhidrátot tartalmaz, amikor az ételt létrehozzuk vagy frissítjük.

<h2><u>Dokumentáció az OilService-hez:</u></h2>

Az OilService osztály CRUD műveleteket biztosít az Oil entitáshoz.

<b>Metódusok:</b>

-    Create(OilCreateRequest request): Ez a metódus létrehoz egy új olaj objektumot a megadott névvel és kalóriatartalommal 14ml-ben, ellenőrzi az input adatokat, majd visszaadja az elkészített olaj objektumot.
-    Update(OilUpdateRequest request): Ez a metódus frissíti az olaj objektumot a megadott id alapján, ellenőrzi az input adatokat, majd visszaadja a frissített olaj objektumot.
-    Delete(int id): Ez a metódus törli az olaj objektumot a megadott id alapján.

<b>Kivételek:</b>

-    "Oil object is null." - Akkor dobódik, ha egy null Oil objektumot adnak át a CheckData() metódusnak.
-    "Name can't be longer than 50 characters!" - Akkor dobódik, ha egy Oil objektum neve hosszabb, mint 50 karakter.
-    "Oils can't contain more than 300 cal/14ml!" - Akkor dobódik, ha egy Oil objektum calIn14Ml tulajdonsága nagyobb, mint 300.
-    "Please enter at least 5 characters to the name field." - Akkor dobódik, ha egy Oil objektum neve kevesebb, mint 5 karakter.
-    "Oils can't contain less than 30 cal/14ml!" - Akkor dobódik, ha egy Oil objektum calIn14Ml tulajdonsága kevesebb, mint 30.
-    "This oil doesn't exist." - Akkor dobódik, ha a GenericService osztály Read() metódusa null értéket ad vissza.
-    "Food can't contain less than 0g carbohydrate." - Akkor dobódik, ha az étel negatív mennyiségű szénhidrátot tartalmaz, amikor az ételt létrehozzuk vagy frissítjük.

<h2><u>Dokumentáció a RecipeService-hez:</u></h2>

A RecipeService osztály CRUD műveleteket biztosít a Recipe entitáshoz.

<b>Metódusok:</b>

-    Create(WriteRecipeRequest request): Ez a metódus létrehoz egy új recept objektumot a megadott szerzővel, névvel, módszerrel, idővel és hozzávalókkal, kiszámítja a táplálkozási értékeket és létrehoz egy leírást a receptről, ellenőrzi a bemeneti adatokat és visszaadja a létrehozott recept objektumot.
-    Update(UpdateRecipeRequest request): Ez a metódus frissíti a recept objektumot a megadott azonosítóval, szerzővel, névvel, módszerrel, idővel és hozzávalókkal, kiszámítja a táplálkozási értékeket és létrehoz egy leírást a receptről, ellenőrzi a bemeneti adatokat és visszaadja a frissített recept objektumot.
-    Delete(int recipeId): Ez a metódus törli a recept objektumot a megadott azonosítóval.

<b>Kivételek:</b>

-    "This recipe doesn't exist." - Ez a kivétel akkor dobódik, ha olyan receptet próbálnak olvasni, frissíteni vagy törölni az adatbázisból, ami nem létezik.
-    "Only the author can delete the recipe." - Ez a kivétel akkor dobódik, ha a egy felhasználó, aki nem a recept szerzője megpróbálja törölni azt.
-    "Some ingredient has no portion." - Ez a kivétel akkor dobódik, ha az összetevők száma nem egyenlő az összetevő-adagok számával.
-    "You need to choose an oil, if you fry something." - Ez a kivétel akkor dobódik, ha a felhasználó valamit sütni szeretne, de nem választ olajat.
-    "Oil has no portion!" - Ez a kivétel akkor dobódik, ha a felhasználó valamit sütni szeretne, de nem ad meg mennyiséget az olajhoz.
-    "Only the author can modify the recipe, please check in the "save as" option, if you want to create a new recipe base on this one!" - Ez a kivétel akkor dobódik, ha egy felhasználó, aki nem a recept szerzője megpróbálja módosítani azt anélkül, hogy a "save as" opciót választaná. Ez az opció egy új receptet hoz létre az eredeti recept alapján.
-    "Some ingredient has no portion." - Ez a kivétel akkor dobódik, ha az összetevők száma nem egyenlő az összetevő-adagok számával.
-    "Recipe name is empty." - Ez a kivétel akkor dobódik, ha a felhasználó frissíteni próbál egy receptet anélkül, hogy megadná annak nevét.
-    "Method is not defined." - Ez a kivétel akkor dobódik, ha a felhasználó frissíteni próbál egy receptet anélkül, hogy meghatározná a készítési módszert.
-    "Ingredient or portion missing." - Ez a kivétel akkor dobódik, ha a felhasználó frissíteni próbál egy receptet anélkül, hogy meghatározná az összetevőt vagy az ahhoz tartozó adagot.

<h2><u>Dokumentáció a SocialMediaService-hez:</u></h2>

A SocialMediaService osztály metódusokat biztosít a kommenteléshez, felhasználók követéséhez/lekövetéséhez, és kommentek lekéréséhez egy adott felhasználóhoz.

<b>Metódusok:</b>

-    ModifyComment(ModifyCommentRequest request): Ez a metódus lehetővé teszi az azonosított felhasználó által készített komment szövegének módosítását. A paraméterként egy ModifyCommentRequest objektumot vesz át, amely tartalmazza a komment azonosítóját és az új szöveget. Visszatér egy Comment objektummal, amely az átalakított kommentet jelenti. 
-    CreateCommentListByAuthenticatedEmail: Ez a metódus lekéri az azonosított felhasználóhoz irányuló kommentek listáját. Egy Comment objektumokat tartalmazó listával tér vissza. 
-    DeleteCommentById(int commentId): Ez a metódus törli az azonosított felhasználó által készített kommentet. A komment azonosítóját veszi paraméterként. 
-    StartOrStopFollow(UnFollowFollowRequest request): Ez a metódus lehetővé teszi az azonosított felhasználó számára, hogy kövessen vagy lekövessen egy másik felhasználót. Egy UnFollowFollowRequest objektumot vesz paraméterként, amely tartalmazza a követni/lekövetni kívánt felhasználó e-mail címét. <!--todo:kicserélni az emaileket idra-->
-    SendComment(WriteCommentRequest request): Ez a metódus lehetővé teszi az azonosított felhasználó számára, hogy kommentet küldjön egy másik felhasználónak. Egy WriteCommentRequest objektumot vesz paraméterként, amely tartalmazza a címzett felhasználó e-mail címét és a komment szövegét. Visszatér egy Comment objektummal, amely az elküldött kommentet jelenti.

<b>Kivételek:</b>

-    "Comment doesn't exist." - Akkor dobódik, ha nem létezik megadott azonosítójú hozzászólás.
-    "You do not have permission to modify the comment." - Akkor dobódik, ha azonosított felhasználó nem rendelkezik jogosultsággal a hozzászólás módosítására.
-    "You do not have permission to delete the comment." - Akkor dobódik, ha azonosított felhasználónak nincs jogosultsága a hozzászólás törlésére.
-    "Auth to follow doesn't exist." - Akkor dobódik, ha nem létezik azonosított e-mailcímmel Auth objektum.
-    "You need to create a user profile first!" - Akkor dobódik, ha az azonosított felhasználónak nincs felhasználói profilja és olyan műveletet próbál végrehajtani, amelyhez szükséges.
-    "Invalid 'toAuth' email." - Akkor dobódik, ha az 'toAuth' paraméterként átadott e-mailcím érvénytelen.
-    "'toAuth' doesn't exist." - Akkor dobódik, ha az 'toAuth' paraméterként átadott e-mailcímmel Auth objektum nem létezik.
-    "Invalid 'toAuth' username." - Akkor dobódik, ha az 'toAuth' paraméterként átadott Auth objektum érvénytelen felhasználónevet tartalmaz.
-    "'toAuth' has no user profile!" - Akkor dobódik, ha az 'toAuth' paraméterként átadott Auth objektumhoz nincs felhasználói profil rendelve.
-    "You can't follow yourself." - Akkor dobódik, ha az azonosított felhasználó saját profilját próbálja követni a StartOrStopFollow metódusban.

Megjegyzés: Az azonosított felhasználónak felhasználói profilra van szüksége a rendszerben ahhoz, hogy használja ezeket a metódusokat.

<h2> <u>Dokumentáció a TagService-hez:</u></h2>

A TagService osztály CRUD műveleteket biztosít a Tag entitásra.

<b>Metódusok:</b>

-    Create(TagCreateRequest request): Ez a metódus létrehoz egy új tag objektumot a megadott névvel, leírással, food tulajdonsággal, maximális és minimális értékkel. Ellenőrzi az input adatok érvényességét és visszaadja a létrehozott tag objektumot.
-    Update(TagUpdateRequest request): Ez a metódus frissíti a tag objektumot a megadott azonosítóval, névvel és leírással. Ellenőrzi az input adatok érvényességét és visszaadja a frissített tag objektumot.
-    Delete(int id): Ez a metódus törli a megadott azonosítójú tag objektumot. Ha a tag objektum nem létezik, kivétel keletkezik.

<b>Kivételek</b>

-    "Name can't be longer than 50 character!" - Akkor dobódik, amikor a Tag objektum neve hosszabb, mint 50 karakter és azt az adatellenőrző CheckData metódusba átadott objektum esetében észleli.
-    "Description can't be longer than 500 character!" - Akkor dobódik, amikor a Tag objektum leírása hosszabb, mint 500 karakter és azt az adatellenőrző CheckData metódusba átadott objektum esetében észleli.
-    "Please enter at least 3 character to the name field." - Akkor dobódik, amikor a Tag objektum neve rövidebb, mint 3 karakter és azt az adatellenőrző CheckData metódusba átadott objektum esetében észleli.
-    "Please enter at least 10 character to the description field." - Akkor dobódik, amikor a Tag objektum leírása rövidebb, mint 10 karakter és azt az adatellenőrző CheckData metódusba átadott objektum esetében észleli.
-    "You can't give value to min or max, if you don't choose a property." - Akkor dobódik, amikor a Tag objektum foodProperty tulajdonsága null és a min vagy a max tulajdonságok közül legalább az egyik értéke nem null.
-    "Please enter a number between 0 and 100 to do max field!" - Akkor dobódik, amikor a Tag objektum max tulajdonságának értéke nem esik az 0 és 100 közé.
-    "Please enter a number between 0 and 100 to do min field!" - Akkor dobódik, amikor a Tag objektum min tulajdonságának értéke nem esik az 0 és 100 közé.
-    "This tag doesn't exist." - Akkor dobódik, amikor a megadott azonosítóval nem található Tag objektum az adatbázisban.

<h2> <u> Dokumentáció a UserProfileService-hez:</u></h2>

A UserProfileService osztály műveleteket biztosít a felhasználói profilok kezeléséhez.

<b>Metódusok:</b>

-    SetProfilePicture(UserSetProfilePictureRequset request): Ez a metódus frissíti a felhasználó profilképét a megadott haj, bőr, szem és száj indexekkel. Ellenőrzi a bemeneti adatok érvényességét és visszaadja a frissített felhasználói profil objektumot.
-    CreateProfile(UserSetDatasRequest request): Ez a metódus létrehoz egy új felhasználói profil objektumot a megadott súly, magasság, születési dátum, nem és cél súly alapján. Ha a cél súly nincs megadva, automatikusan beállítódik a felhasználó magasságának és súlyának alapján. Ellenőrzi a bemeneti adatok érvényességét és visszaadja a létrehozott felhasználói profil objektumot.
-    ModifyProfile(UserSetDatasRequest request): Ez a metódus frissíti a felhasználói profil objektumot a megadott súly, magasság, születési dátum, nem és cél súly alapján. Ha valamelyik mező nincs megadva, annak értéke nem változik. Ha a cél súly nincs megadva, automatikusan beállítódik a felhasználó magasságának és súlyának alapján. Ellenőrzi a bemeneti adatok érvényességét és visszaadja a frissített felhasználói profil objektumot.

<b>Kivételek:</b>

-    "You must log in first." - Akkor dobódik, ha az auth értéke null.
-    "The user must be between 12 and 100 years old!" - Akkor dobódik, ha a felhasználó életkora kevesebb, mint 12, vagy több, mint 100.
-    "The user weight must be over 20 and 1000!" - Akkor dobódik, ha a felhasználó súlya kevesebb, mint 20, vagy több, mint 1000.
-    "The user height must be between 40 and 250 cm!" - Akkor dobódik, ha a felhasználó magassága kevesebb, mint 40, vagy több, mint 250.
-    "You must select your gender!" - Akkor dobódik, ha a felhasználó nem határozta meg a nemét.
-    "Invalid gender!" - Akkor dobódik, ha a felhasználó neme nem határozható meg.
-    "The user goal weight must be over 20 and 1000!" - Akkor dobódik, ha a felhasználó cél súlya kevesebb, mint 20, vagy több, mint 1000.
-    "Invalid hair!" - Akkor dobódik, ha a felhasználó hajIndexe kevesebb, mint nondefined vagy nagyobb, mint a white.
-    "Invalid skin color!" - Akkor dobódik, ha a felhasználó bőrIndexe kevesebb, mint nondefined vagy nagyobb, mint a lightest.
-    "Invalid eye color!" - Akkor dobódik, ha a felhasználó szemIndexe kevesebb, mint nondefined vagy nagyobb, mint a brown.
-    "Invalid mouth!" - Akkor dobódik, ha a felhasználó szájIndexe kevesebb, mint nondefined vagy nagyobb, mint a smiling.
