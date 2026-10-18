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

