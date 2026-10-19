# Reflektion — Inlämning 1

**Namn:** Oliver Ågren  
**Datum:** 2026-10-14

---

## Vad var svårast?

Det svåraste var att få ordningen rätt när jag la in data. Jag fick felet "FOREIGN KEY constraint failed" när jag körde min SQL-fil. Det berodde på att albumen låg före artisten, så albumen pekade på en artist som inte fanns än. Jag fick flytta INSERT-raderna så att tabellerna som andra pekar på kom först. Det var också svårt att förstå JOIN när det är flera tabeller med, som när jag skulle koppla ihop låtar och genrer.

---

 Vad lärde du dig?

Jag lärde mig hur tabeller hänger ihop med primärnycklar och främmande nycklar, och hur man ritar det i ett ER-diagram. Jag lärde mig skillnaden mellan en-till-många och många-till-många, och att man löser många-till-många med en kopplingstabell. Jag lärde mig också att använda JOIN, GROUP BY, COUNT och AVG, och att UPDATE och DELETE alltid ska ha WHERE så att man inte ändrar eller tar bort alla rader.
---

## Hur använde du SQL i praktiken — vad kändes naturligt och vad var förvirrande?

SELECT, WHERE och ORDER BY kändes ganska naturligt, för det hade jag övat på innan. Det som var förvirrande var JOIN, eftersom man måste veta vilken kolumn som ska matcha vilken, till exempel Songs.Album_id mot Albums.ID. GROUP BY var också ganska nytt. Jag blev även förvirrad av att SQLite sorterar stora bokstäver före små, så att "BIRDS OF A FEATHER" kom före "Bad guy" tills jag använde COLLATE NOCASE, vilket jag sökte upp hur man gjorde.

---

## Om du hade mer tid — vad hade du lagt till eller gjort annorlunda?

Jag hade lagt till fler album och låtar. Nu har alla album exakt tre låtar, så query 7 (albumet med flest låtar) får inget tydligt svar. Med en fjärde låt på något album hade den blivit bättre. Jag hade också kollat alla låtlängder mot Spotify en gång till och lagt till en query som visar låtar tillsammans med sina genrer, så att man ser att många-till-många fungerar.

---

## (VG) Varför valde du just den här tabellstrukturen?

Jag har fem tabeller: Artists, Albums, Songs, Genres och Song_genres. Jag delade upp det så att varje sak bara lagras en gång. En artist har många album och ett album har många låtar, och det löser jag med främmande nycklar (Artist_id i Albums och Album_id i Songs). En låt kan ha flera genrer och en genre kan höra till många låtar, så där behövs kopplingstabellen Song_genres med två främmande nycklar.

Ett annat sätt hade varit att lägga allt i en enda stor tabell. Då hade artistnamn och albumtitel stått på varje låt, och om man ville ändra en titel hade man behövt ändra på flera rader. Jag hade också fått stoppa in flera genrer i samma cell, till exempel "Pop, Dance-pop", och det går emot 1NF. Ett annat alternativ hade varit en genre-kolumn i Songs. Det är enklare, men en låt kan bara få en genre, och till exempel "Bad guy" har tre i min databas.

Fördelen med min lösning är att datan inte upprepas, att den är lätt att ändra och att den går att bygga ut med fler artister. Nackdelen är att det blir fler tabeller, att man måste använda JOIN för att få fram det man vill se, och att Artists bara har en rad just nu, så den tabellen gör ingen större nytta i den här lilla databasen.
