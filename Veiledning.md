# Raspberry pi veiledning pi

Last ned Raspberry Pi imager fra nettet til operativ systemet du bruker.

1. Sett inn sd-kortet inni pc-en din
2. Inni imageren, sett inn riktig Raspberry Pi, sett inn Ubuntu på operativ system, og last det ned på sd-kortet. Deretter trykk next.

Nå skal du sette opp Raspberryen ved å bygge den, plugge inn kablene den trengs, også gjøre klar ubuntu til det du ønsker.  
Når du har gjort klart Ubuntu, åpne Terminal med å trykke CRTL + Alt + T, også skriv:

``` console
sudo apt update
sudo apt upgrade
```
Nå skal du ha lasta ned oppdateringer den trenger.

**Sett opp brannmur med UFW:**

``` console
sudo apt install ufw
sudo ufw enable
sudo ufw allow ssh
```
Brannmuren skal være klar når du starter opp pi-en


# SSH
**Gjør klar SSH**
``` console
sudo apt install openssh-server
sudo systemtcl enable ssh
sudo systemctl start ssh
```
**Koble til ssh**  
På din pc, skriv i command prompt:
``` console
ssh brukernavn@ip 
```
Du finner ip adressen din ved å skrive: 
``` console
ip a
```
# Statisk ip
Du kan sette av en statisk ip, sånn at du ikke trenger å finne ut ip adressen hver gang du skal bruke ssh.  
**I terminalen skriv:**
``` console
sudo nmtui
```
1. Gå inn på **Edit a connection** -> **Ethernet**.
2. På IPv4 Configuration, bytt "Automatic" til "Manual".
3. På adresses, bytt til ip adressen du skal bruke.
4. På Gateway, bytt til **10.0.0.1**
5. På DNS servers, bytt til **10.0.0.10**. Du kan også legge til en til **1.1.1.1**, hvis du vil.
6. Når du er ferdig, trykk **OK** -> **Back** -> **Quit**
# Python og Git

**Installer Python, Git og MariaDB:**

``` console
sudo apt install python3-pip
sudo apt install git
sudo mysql_secure_installation
```

# MariaDB
**Sett opp MariaDB:**
``` sql
//Installer MariaDB
sudo apt install mariadb-server
//Logg inn i brukeren "root":
sudo mariadb -u root
//Lag en ny bruker (du kan velge navn og passord selv):
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
//Gi brukeren rettigheter:
GRANT ALL PRIVILEGES ON *.* TO 'username'@’localhost’ IDENTIFIED BY 'password';
//Oppdater rettighetene
FLUSH PRIVILEGES;
```
**Kjør sudo apt update og upgrade igjen**

# Telefonkatalog
Koble til Raspberry PI med ssh, og lag en mappe som heter kode.
```console
pwd
```
```console
mkdir kode
```
```console
cd kode/
```


# Database

  
**Logg inn på MariaDB , og skriv dette inn:**
```sql
CREATE DATABASE telefonkatalog;
```
```sql
USE telefonkatalog;
```
```sql
CREATE TABLE person (
 id int NOT NULL AUTO_INCREMENT,
 fornavn VARCHAR(255) NOT NULL,
 etternavn VARCHAR(255) NOT NULL,
 telefonnummer CHAR(8),
 PRIMARY KEY (id)
);
```
```sql
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Erik', 'Perik', '12345678');
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Lise', 'Pise', '22334455');
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Testus', 'Jensen', '11114444');
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Knut', 'Donald', '31415926');
```

