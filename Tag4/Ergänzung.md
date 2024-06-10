# Ergänzung ALTER TABLE tbl ADD Constraint

Fremdschlüssel hinzufügen:<br>
```
ALTER TABLE <DetailTab>
  ADD CONSTRAINT <Constraint> FOREIGN KEY (<Fremdschlüssel>)
  REFERENCES <MasterTab> (Primärschlüssel);

```
![Tabelle](image-3.png)

Unique Schlüssel hinzufügen:<br>
```
ALTER TABLE <Tabelle>
  ADD UNIQUE (<FS_Name>); 
```

Fragen:<br>
Fügen Sie ein paar Daten in die Tabellen tbl_Projekt,tbl_Passagier, tbl_Bus, tbl_Fahrer und tbl_Ausweis ein und überprüfen Sie die Beziehungen.

```
-- Einfügen von Daten in tbl_Projekt

INSERT INTO `tbl_Projekt` (`Bezeichnung`, `Budget`, `tbl_Projekt_ID_Projekt`) VALUES ('Projekt A', 1000, 1);

INSERT INTO `tbl_Projekt` (`Bezeichnung`, `Budget`, `tbl_Projekt_ID_Projekt`) VALUES ('Projekt B', 2000, 2);
 
-- Einfügen von Daten in tbl_Fahrer

INSERT INTO `tbl_Fahrer` (`ID_Fahrer`, `Vorname`, `Nachname`, `Geb.datum`) VALUES (1, 'Max', 'Mustermann', '1980-01-01');

INSERT INTO `tbl_Fahrer` (`ID_Fahrer`, `Vorname`, `Nachname`, `Geb.datum`) VALUES (2, 'Erika', 'Mustermann', '1985-02-02');
 
-- Einfügen von Daten in tbl_Bus

INSERT INTO `tbl_Bus` (`Bezeichnung`, `Kennzeichen`, `Anzahl_Plätze`, `tbl_Fahrer_ID_Fahrer`) VALUES ('Bus 1', 'ABC123', '50', 1);

INSERT INTO `tbl_Bus` (`Bezeichnung`, `Kennzeichen`, `Anzahl_Plätze`, `tbl_Fahrer_ID_Fahrer`) VALUES ('Bus 2', 'DEF456', '60', 2);
 
-- Einfügen von Daten in tbl_Ausweis

INSERT INTO `tbl_Ausweis` (`ID_Ausweis`, `Nummer`, `Art`, `tbl_Fahrer_ID_Fahrer`) VALUES (1, 'A123', 1, 1);

INSERT INTO `tbl_Ausweis` (`ID_Ausweis`, `Nummer`, `Art`, `tbl_Fahrer_ID_Fahrer`) VALUES (2, 'B456', 2, 2);
 
-- Einfügen von Daten in tbl_Passagier

INSERT INTO `tbl_Passagier` (`Name`, `Platznummer`, `tbl_Bus_ID_Bus`) VALUES ('Hans Müller', '1A', 1);

INSERT INTO `tbl_Passagier` (`Name`, `Platznummer`, `tbl_Bus_ID_Bus`) VALUES ('Anna Schmidt', '2B', 2);
 
-- Versuch, einen doppelten Fremdschlüsselwert in tbl_Projekt einzufügen

INSERT INTO `tbl_Projekt` (`Bezeichnung`, `Budget`, `tbl_Projekt_ID_Projekt`) VALUES ('Projekt C', 3000, 1);

-- Dies wird aufgrund des Unique Constraints auf tbl_Projekt_ID_Projekt fehlschlagen und eine Fehlermeldung auslösen.
 
-- Versuch, NULL als Fremdschlüsselwert in tbl_Passagier einzufügen

INSERT INTO `tbl_Passagier` (`Name`, `Platznummer`, `tbl_Bus_ID_Bus`) VALUES ('Karl Meier', '3C', NULL);

-- Dies wird erfolgreich sein, da tbl_Bus_ID_Bus als INT NOT NULL deklariert ist, was bedeutet, dass NULL-Werte nicht erlaubt sind.
[14:41] Zurbrügg Dexter
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;

SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;

SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------

-- Schema mydb

-- -----------------------------------------------------

DROP SCHEMA IF EXISTS `mydb` ;

-- -----------------------------------------------------

-- Schema mydb

-- -----------------------------------------------------

CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;

USE `mydb` ;

-- -----------------------------------------------------

-- Table `tbl_Projekt`

-- -----------------------------------------------------

DROP TABLE IF EXISTS `tbl_Projekt` ;

CREATE TABLE IF NOT EXISTS `tbl_Projekt` (

  `ID_Projekt` INT NOT NULL AUTO_INCREMENT,

  `Bezeichnung` VARCHAR(30) NOT NULL,

  `Budget` DECIMAL(10) NULL,

  `tbl_Projekt_ID_Projekt` INT NOT NULL,

  PRIMARY KEY (`ID_Projekt`),

  CONSTRAINT `fk_tbl_Projekt_tbl_Projekt`

    FOREIGN KEY (`tbl_Projekt_ID_Projekt`)

    REFERENCES `tbl_Projekt` (`ID_Projekt`)

    ON DELETE NO ACTION

    ON UPDATE NO ACTION)

ENGINE = InnoDB;

CREATE INDEX `fk_tbl_Projekt_tbl_Projekt_idx` ON `tbl_Projekt` (`tbl_Projekt_ID_Projekt` ASC) VISIBLE;
 
-- -----------------------------------------------------

-- Table `tbl_Fahrer`

-- -----------------------------------------------------

DROP TABLE IF EXISTS `tbl_Fahrer` ;

CREATE TABLE IF NOT EXISTS `tbl_Fahrer` (

  `ID_Fahrer` INT NOT NULL,

  `Vorname` VARCHAR(30) NOT NULL,

  `Nachname` VARCHAR(30) NOT NULL,

  `Geb.datum` DATE NOT NULL,

  PRIMARY KEY (`ID_Fahrer`))

ENGINE = InnoDB;


-- -----------------------------------------------------

-- Table `tbl_Bus`

-- -----------------------------------------------------

DROP TABLE IF EXISTS `tbl_Bus` ;

CREATE TABLE IF NOT EXISTS `tbl_Bus` (

  `ID_Bus` INT NOT NULL AUTO_INCREMENT,

  `Bezeichnung` VARCHAR(30) NOT NULL,

  `Kennzeichen` VARCHAR(30) NOT NULL,

  `Anzahl_Plätze` VARCHAR(30) NOT NULL,

  `tbl_Fahrer_ID_Fahrer` INT NOT NULL,

  PRIMARY KEY (`ID_Bus`),

  CONSTRAINT `fk_tbl_Bus_tbl_Fahrer1`

    FOREIGN KEY (`tbl_Fahrer_ID_Fahrer`)

    REFERENCES `tbl_Fahrer` (`ID_Fahrer`)

    ON DELETE NO ACTION

    ON UPDATE NO ACTION)

ENGINE = InnoDB;

CREATE INDEX `fk_tbl_Bus_tbl_Fahrer1_idx` ON `tbl_Bus` (`tbl_Fahrer_ID_Fahrer` ASC) VISIBLE;


-- -----------------------------------------------------

-- Table `tbl_Ausweis`

-- -----------------------------------------------------

DROP TABLE IF EXISTS `tbl_Ausweis` ;

CREATE TABLE IF NOT EXISTS `tbl_Ausweis` (

  `ID_Ausweis` INT NOT NULL,

  `Nummer` VARCHAR(30) NULL,

  `Art` INT NULL,

  `tbl_Fahrer_ID_Fahrer` INT NOT NULL,

  PRIMARY KEY (`ID_Ausweis`, `tbl_Fahrer_ID_Fahrer`),

  CONSTRAINT `fk_tbl_Ausweis_tbl_Fahrer1`

    FOREIGN KEY (`tbl_Fahrer_ID_Fahrer`)

    REFERENCES `tbl_Fahrer` (`ID_Fahrer`)

    ON DELETE NO ACTION

    ON UPDATE NO ACTION)

ENGINE = InnoDB;

CREATE INDEX `fk_tbl_Ausweis_tbl_Fahrer1_idx` ON `tbl_Ausweis` (`tbl_Fahrer_ID_Fahrer` ASC) VISIBLE;


-- -----------------------------------------------------

-- Table `tbl_Passagier`

-- -----------------------------------------------------

DROP TABLE IF EXISTS `tbl_Passagier` ;

CREATE TABLE IF NOT EXISTS `tbl_Passagier` (

  `ID_Passagier` INT NOT NULL AUTO_INCREMENT,

  `Name` VARCHAR(30) NOT NULL,

  `Platznummer` VARCHAR(30) NULL,

  `tbl_Bus_ID_Bus` INT NOT NULL,

  PRIMARY KEY (`ID_Passagier`),

  CONSTRAINT `fk_tbl_Passagier_tbl_Bus1`

    FOREIGN KEY (`tbl_Bus_ID_Bus`)

    REFERENCES `tbl_Bus` (`ID_Bus`)

    ON DELETE NO ACTION

    ON UPDATE NO ACTION)

ENGINE = InnoDB;

CREATE INDEX `fk_tbl_Passagier_tbl_Bus1_idx` ON `tbl_Passagier` (`tbl_Bus_ID_Bus` ASC) VISIBLE;


SET SQL_MODE=@OLD_SQL_MODE;

SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;

SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
```
```
-- Angenommen tbl_Projekt_ID_Projekt hat einen Unique-Constraint
INSERT INTO tbl_Projekt (ID_Projekt, Bezeichnung, Budget)
VALUES (1, 'Projekt C', 30000);
```
```
INSERT INTO tbl_Projekt (ID_Projekt, Bezeichnung, Budget)
VALUES (1, 'Projekt A', 10000),
       (2, 'Projekt B', 20000);

INSERT INTO tbl_Bus (ID_Bus, Bezeichnung, Kennzeichen, Anzahl_Plaetze)
VALUES (1, 'Bus 1', 'XYZ 123', '50'),
       (2, 'Bus 2', 'ABC 456', '60');

INSERT INTO tbl_Fahrer (ID_Fahrer, Vorname, Nachname)
VALUES (1, 'Max', 'Mustermann'),
       (2, 'Erika', 'Musterfrau');

INSERT INTO tbl_Ausweis (ID_Ausweis, Nummer, Art, tbl_Fahrer_ID_Fahrer)
VALUES (1, '123456', 1, 1),
       (2, '789012', 2, 2);

INSERT INTO tbl_Passagier (ID_Passagier, Name, Platznummer, tbl_Bus_ID_Bus)
VALUES (1, 'Hans', '1A', 1),
       (2, 'Anna', '1B', 1),
       (3, 'Peter', '2A', 2);
```

Was geschieht, wenn Sie z.B. bei einer 1:c Beziehung zwei gleiche Fremdschlüsselwerte angeben?
Es gibt einen Fehler, wenn ein unique Constraint vorhanden ist

Was geschieht, wenn Sie z.B. bei einer 1:mc Beziehung NULL als FS-Wert angeben?
Es wird ein Datensatz ohne Zuordnung erstellt
Bei NOT NULL gibt es aber einen Fehler