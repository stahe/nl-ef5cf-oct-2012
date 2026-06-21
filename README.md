# Migratie van NHibernate naar Entity Framework 5 (oktober 2012)

Dit document illustreert een **flexibele en schaalbare ASP.NET-applicatiearchitectuur**
en laat zien hoe de ORM **NHibernate** kan worden vervangen door **Entity Framework 5**
zonder de applicatielaag te wijzigen.

📄 De PDF van het document is hier beschikbaar: https://stahe.github.io/nl-ef5cf-oct-2012/nl-ef5cf-oct-2012.pdf  
🌐 De bijbehorende website is te vinden op de URL: https://stahe.github.io/nl-ef5cf-oct-2012/

---

## Achtergrond

**Entity Framework** is een ORM (Object Relational Mapper) die oorspronkelijk door Microsoft is ontwikkeld
en sinds juli 2012 open source is.

In een ASP.NET-cursus is dit document gebaseerd op een gelaagde architectuur
waardoor technologieën (ORM, DBMS) kunnen worden aangepast zonder dat dit invloed heeft op de applicatie.

---

## Algemene architectuur

Het onderstaande schema toont de architecturen die in de applicatie worden gebruikt:

![ASP.NET-architectuur met NHibernate en Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D200000183315F4E40.png)

![ASP.NET-architectuur met Entity Framework 5 en Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D7000001825B1CF7DD.png)

### Beschrijving van de lagen

- **ASP.NET-toepassing**  
  Presentatie- en applicatielogicalaag.

- **DAO (Data Access Objects)**  
  Interface voor gegevenstoegang die door de toepassing wordt gebruikt.

- **ORM (NHibernate / Entity Framework)**  
  Verantwoordelijk voor het genereren van SQL en de communicatie met ADO.NET.

- **ADO.NET**  
  Koppeling naar het DBMS.

- **DBMS**  
  Databasemanagementsysteem.

- **Spring.NET**  
  Zorgt voor de integratie van de lagen en de injectie van afhankelijkheden.

---

## Waarom een ORM gebruiken?

Door de DAO-laag rechtstreeks aan ADO.NET te koppelen, wordt de applicatie afhankelijk van het DBMS:

- verschillen in datatypes;
- strategieën voor het genereren van primaire sleutels;
- propriëtaire SQL;
- DBMS-specifieke bibliotheken.

Met een ORM komt het wisselen van DBMS in feite neer op **het wijzigen van de configuratie**
van de ORM. De DAO-laag blijft ongewijzigd.

---

## Rol van Spring.NET

Spring.NET maakt het mogelijk om:

- de ASP.NET-toepassing een verwijzing naar de DAO-laag te verkrijgen;
- deze laag aan te maken op basis van een configuratiebestand;
- een DAO-implementatie door een andere te vervangen **zonder de code te wijzigen**,
  zolang de interface identiek blijft.

---

## Doel van het document

Concreet aantonen dat de architectuur:

- **bestand is tegen wijzigingen in het DBMS**;
- **bestand is tegen wijzigingen in de ORM**;
- het mogelijk maakt om **NHibernate te vervangen door Entity Framework 5**
  zonder de ASP.NET-toepassingslaag te wijzigen.

---

## Volgde aanpak

De migratie verloopt in verschillende stappen:

1. Verkenning van **Entity Framework 5** met verschillende DBMS’en;
2. Opbouw van een nieuwe gegevenslaag (**DAO2**);
3. Koppeling van de bestaande ASP.NET-toepassing aan deze nieuwe DAO-laag.

---

## Doelgroep

- ASP.NET-ontwikkelaars
- Studenten en docenten op het gebied van softwarearchitectuur
- Iedereen die geïnteresseerd is in ontkoppelde en schaalbare architecturen

---

## Licentie en gebruik

Educatief document bedoeld voor onderwijs en demonstratie
van schaalbare applicatiearchitecturen.
