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

Issue 01: executed and give me this:

-- ISSUE-01 

Pendent: encara no s'ha carregat C:\eclipse-workspace\actividad-maven-hugo-limoso\files\items.txt
Introduïu número d'empleat: 

-- ISSUE 02: 

He comprovat que els fitxers .txt er localitcen amb rutes relatives utilitzan el user.dir

-- ISSUE 03

- **Obre el fitxer amb un BufferedReader dins d'un try-with-resources:**
  S'ha fet servir un bloc `try (BufferedReader br = new BufferedReader(new FileReader(f)))`. Això va de conya perquè Java s'encarrega de tancar el fitxer automàticament en acabar (o si peta res), evitant deixar fluxos oberts innecessàriament.

- **Llegeix i tracta cada línia com a text:**
  Amb un bucle `while ((line = br.readLine()) != null)`, anem llegint el fitxer `items.txt` de dalt a baix, línia a línia i de forma seqüencial, tractant cada una simplement com un `String` de text pla sense modificar-la.

- **Deixa preparada la crida a la conversió que completaràs a RA1-ISSUE-04:**
  Dins del bucle he deixat l'estructura llesta amb un comentari a punt, a l'espera de cridar el mètode de conversió (`parseProductLine`) que farem a la següent issue. De moment no s'interpreta cap dada.

-- ISSUE 04

- **Implementa parseProductLine(String line) a Shop.java.**
  He definit aquest mètode per encarregar-se exclusivament de transformar una línia de text en un objecte, separant així la lògica de lectura de la lògica de conversió.

- **Separa camps i clau/valor, i converteix preu i estoc al tipus adequat.**
  Mitjançant `.split(";")` i `.split(":")`, tallem el text per extreure les dades de cada camp. Després, convertim el preu a un objecte `Amount` (fent un `Double.parseDouble`) i l'estoc a un nombre enter (`Integer.parseInt`) de forma controlada dins d'un `try-catch`.

- **Retorna un Product i fes que la lectura l'afegeixi quan la línia és vàlida.**
  El mètode retorna el nou `Product` creat si tot és correcte. Després, al bucle de lectura, comprovem que no sigui nul i l'afegim automàticament a l'inventari de la botiga.

-- ISSUE 05

- **Prepara un exemple de linia incompleta o amb camp invalid.**
  S'ha provat amb una línia amb un camp invàlid al preu (per exemple: `Item:Ratolí;Wholesaler Price:abc;Stock:5;`) i una altra de tallada o incompleta.

- **Detecta l'error durant la conversio.**
  Gràcies a les validacions de longitud (`parts.length`) i al bloc `try-catch` que envolta les conversions numèriques (`Double.parseDouble` / `Integer.parseInt`), detectem a l'instant si el format falla.

- **Mostra un missatge comprensible o ignora la linia de forma justificada.**
  L'aplicació captura l'excepció, mostra un avís per consola clar (indicant quina línia s'ha descartat) i retorna `null`. Així s'evita que el programa es tanqui de cop (es garanteix la robustesa) i l'inventari es carrega amb els productes correctes.
  
  -- ISSUE 06

- **Crea o utilitza una accio per afegir producte.**
  S'ha completat el mètode `addProduct()` buit que ja venia a la plantilla de `Shop.java`, connectant-lo directament amb l'opció 2 del menú principal de la consola.

- **Valida que el producte te dades minimes coherents.**
  L'aplicació demana el nom, el preu i l'estoc. A més, comprova prèviament mitjançant `findProduct()` que no s'afegeixi un producte repetit amb el mateix nom i controla que s'insereixi correctament a l'ArrayList de l'inventari.

- **Mostra el producte nou dins l'inventari en memoria.**
  Un cop introduït, el producte queda registrat a l'execució actual i es pot veure a l'instant en triar l'opció de veure l'inventari (`showInventory()`), sense necessitat de reiniciar el programa.
