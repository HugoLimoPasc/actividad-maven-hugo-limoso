# ComputerCenterShop v0 starter

Projecte inicial visible per a la practica integradora de RA1 del modul MP0486 - Acces a dades.

## Finalitat

Aquest starter serveix per treballar la gestio d'informacio en fitxers: rutes relatives, lectura, conversio de text a objectes, modificacio en memoria, escriptura, persistencia entre execucions i tractament d'errors.

No es una solucio completa. El treball de l'alumnat consisteix a evolucionar el projecte seguint el backlog RA1.

## Estructura

- `model`: classes de domini.
- `view`: interfície grafica Swing existent.
- `main`: coordinacio principal de l'aplicacio i menu de consola.
- `dao`: acces a dades basat en fitxers.
- `files`: dades de treball en text.

## Dades principals

- `files/users.txt`: usuaris per al login simulat.
- `files/items.txt`: productes inicials de la botiga.

Credencials de prova:

- usuari `1001`, contrasenya `admin`
- usuari `1002`, contrasenya `repair`

## Tasques esperades de RA1

El backlog indica quines parts s'han de completar, corregir o demostrar:

- lectura real de `items.txt`;
- conversio robusta de linies de text a `Product`;
- modificacio de l'inventari;
- guardat de l'inventari actualitzat;
- comprovacio de persistencia entre execucions;
- gestio de fitxer absent o linia mal formada;
- README i proves finals.

## Execucio

Requisits:

- JDK 25.
- Maven 3.9.x, si es vol compilar des de linia d'ordres.

Comandes utils:

```bash
mvn compile
```

Classe principal de consola:

```text
main.Shop
```

Classe principal grafica Swing:

```text
view.LoginView
```

## Limits RA1

Aquest projecte no utilitza JDBC, SQL, ORM, MongoDB, serveis externs ni bases de dades. La persistencia ha de quedar limitada a fitxers locals.

--- ISSUE 01 ---

Pendent: encara no s'ha carregat C:\eclipse-workspace\actividad-maven-hugo-limoso\files\items.txt
Introduïu número d'empleat: 

--- ISSUE 02 --- 

He comprovat que els fitxers .txt es localitcen amb rutes relatives utilitzan el user.dir

--- ISSUE 03 ---

He obert el fitxer amb un try-with-resources per assegurar que es tanca sol, l'he anat llegint línia a línia i he deixat la crida al mètode parseProductLine a punt per a la següent issue.

--- ISSUE 04 ---

S'ha implementat el mètode parseProductLine per convertir cada línia vàlida d'text en un objecte Product i afegir-lo automàticament a l'inventari.

--- ISSUE 05 ---

S'ha afegit robustesa al mètode parseProductLine mitjançant un bloc try-catch i validacions de longitud. 
Això permet detectar línies mal formades, ignorar-les de manera controlada i mostrar un avís sense que l'aplicació es tanqui.

--- ISSUE 06 ---

S'ha desenvolupat la funcionalitat completa per afegir nous productes de manera dinàmica des de la consola sense reiniciar l'aplicació. El sistema valida pas a pas que el nom no estigui 
duplicat i que tant el preu com l'estoc siguin numèrics i coherents, evitant errors d'execució. Això garanteix la robustesa de l'inventari en memòria abans de desar-lo definitivament al fitxer.

--- ISSUE 07 ---

S'ha desenvolupat el mètode addStock() per actualitzar de manera interactiva i segura l'estoc d'un producte existent a la memòria. El programa valida pas a pas que el producte existeixi, 
que la quantitat introduïda sigui un enter vàlid i evita estocs negatius. Això permet modificar les quantitats a l'instant sense reiniciar l'aplicació ni alterar la resta de dades de l'inventari.

--- ISSUE 08 ---
 
S'ha desenvolupat el mètode removeProduct() per permetre l'eliminació d'articles de l'inventari en memòria durant l'execució. El sistema valida interactivament que el producte existeixi 
abans de procedir i utilitza el mètode .remove() de la col·lecció per esborrar-lo. Aquesta operació garanteix que l'element seleccionat desaparegui sense alterar ni corrompre la resta de 
productes emmagatzemats.

--- ISSUE 09 ---

S'ha implementat el mètode saveInventory() per persistir l'estat actual de l'inventari en memòria directament al fitxer items.txt utilitzant la ruta configurada del projecte. Mitjançant 
PrintWriter es formateja cada producte en una línia de text estructurada, assegurant que no es perdi cap dada modificada. Això permet conservar els canvis de manera permanent i 
recuperar-los automàticament al reiniciar l'aplicació.

