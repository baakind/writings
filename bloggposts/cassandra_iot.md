# Cassandra for IoT
Dette går kanskje i preface-delen

- Hva er Cassandra (kort)
- Hva menes med IoT/Internet of things (kort)
- Hva kjennetegner IoT i denne settingen
	- Typisk mange enheter som potensielt skriver samtidig, og ofte


## Time series data
- Hva er time series data
- Typisk data fra værsensorer, sensorer i vegkanten, logger osv.

## Hvorfor velge Cassandra?
- High availability & scalability
- Kjent for å håndtere store mengder med reads og writes (referanser!)
- Relativt moden
- Stort og aktivt community
- Brukes av mange store aktører (referanser!)
- DTCS
	- Komprimering spesialisert for time series data
	- Refere til bloggpost hos spotify (masteroppgave)
	- Låne figur (?) som viser fordeling i skriving til filerp å disk. Evt. refere til den via tekst/lenker?

## Wide column store
( Annen overskrift?)

- Hva er wide column?
- Hvordan bruke wide column?
- Primary, clustering/partition og compound key
	- Visualisere det
- Eksempel på veipasseringer 

```
// Sjekk syntaks, sjekk datatyper
CREATE TABLE passeringer (
  sensorid text,
  timestamp timestamp,
  speed double,
 PRIMARY KEY (sensorid, timestamp));
```
- Data vil sorteres kronologisk basert på timestamp
- BRuker vi DTCS i tillegg vil man minimere antall filer som brukes til lesing = bedre performance (referanser!)
- Tai bruk partition-key hvis man får veldig mange passeringer/registreringer på en sensor.
- F.eks kan man fordele dep å time, dag, måned, år etc avhengig av hyppigheten i registreringene
- Cassandra kan håndtere 2 billions/milliarder kolonner per rad

```
// Sjekk syntaks, sjekk datatyper
CREATE TABLE passeringer (
  sensorid text,
  month int,
  timestamp timestamp,
  speed double,
 PRIMARY KEY ((sensorid, month), timestamp));
```

## Oppsummering
- Kort fortalt hva Cassandra er, og hvordan det kan brukes til IoT-prosjekter og sensordata.
- Mye mer enn hva som er fortalt her