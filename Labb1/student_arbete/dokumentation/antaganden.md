# Antaganden och designval (Labb 1)

Här är de antaganden och beslut som jag har utgått ifrån baserat på verksamhetsbeskrivningen när jag skapade ER-diagrammet.

## Kopplingar till butik
* **Medlemmar och Anställda:** Enligt texten tillhör en medlem endast en butik, även om deras medlemsnummer är unikt i hela systemet. Jag har antagit att samma logik gäller för de anställda. För designen innebär detta att vi får en direkt relation (en-till-många) där en butik kan ha flera medlemmar och anställda, men en specifik medlem eller anställd bara kan vara kopplad till exakt en butik i diagrammet.

## Butikens sortiment och priser
* **Lager per butik:** Eftersom pris, hyllplats och antal kopior av en film varierar beroende på butik, kan dessa uppgifter inte ligga direkt på filmen. Därför har jag skapat en koppling mellan butik och film där dessa värden sparas.

## Uthyrning och Betyg
* **Unikt ID för uthyrning:** Eftersom texten kräver att en medlem ska kunna hyra samma film igen vid ett senare tillfälle, har jag gett uthyrningen ett eget unikt ID. Utan detta hade systemet inte kunnat skilja på de olika tillfällena.
* **Betygsättning som attribut:** Instruktionen anger att betyget ska kopplas till den specifika uthyrningen, därför ligger betyg och betygsdatum som attribut där. Ett antagande här är att systemet accepterar risken att en medlem kan hyra samma film flera gånger och därmed betygsätta den flera gånger, vilket teoretiskt kan manipulera filmens medelbetyg.

## Reservationer och Uthyrningar
* **Transaktion mot specifik butik:** Även om en medlem registreras på en specifik hemmabutik, antar jag att de kan hyra och reservera filmer i företagets alla butiker i landet (till exempel om de är ute och reser). Därför måste varje specifik uthyrning och reservation kopplas direkt till filmen i den butik där utlåningen faktiskt sker, istället för att bara förlita sig på medlemmens hemmabutik. På så sätt vet systemet alltid vilken butiks lagersaldo som ska uppdateras.

## Roller
* **Filmarbetare och deras uppdrag:** Eftersom flera personer kan ha samma namn har jag lagt till ett unikt ID för varje filmarbetare. Texten anger också att en person kan ha flera roller i samma film (tex både skådespelare och regissör). I ER-diagrammet löser jag detta genom att skapa en egen kopplingsentitet mellan filmen och filmarbetaren. Istället för en direkt relation pekar båda mot denna nya entitet där attributet "Roll" sparas. Detta designval gör att systemet kan skapa flera kopplingar för en och samma person i samma film.

## Beräknade värden
* **Status och Medelbetyg:** Statusen (om filmen finns i lager) och medelbetyget för en film i en viss butik räknas ut i systemet baserat på aktuella uthyrningar och tidigare betyg. Dessa markeras som härledda attribut.

## Genrer
* **Flera genrer per film:** Instruktionen anger att en film kan tillhöra en eller flera genrer. För designen innebär detta en många-till-många-relation mellan film och genre, så att systemet kan koppla samma film till exempelvis både "Drama" och "Komedi".