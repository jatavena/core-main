# ModSecurityn ja OWASP CRS:n asennus ja konfigurointi
## 1. Yleistä
### 1.1 Mikä on ModSecurity?
ModSecurity on tehokas avoimen lähdekoodin verkkosovellusten palomuuri (WAF), joka voidaan integroida Apache-palvelimeen suojaamaan sovelluksia haitallisilta pyynnöiltä. ModSecurity tarvitsee toimiakseen kokoelman sääntöjä, joidenka perusteella se hallitsee liikennettä. Tähän tarkoitukseen tässä projektissa käytetään yleisesti käytössä olevaa OWASP CRS -sääntökokoelmaa, joka suojaa järjestelmää seuraavilta hyökkäyksiltä:
- SQL Injection (SQLi)
- Cross Site Scripting (XSS)
- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)
- PHP Code Injection
- Java Code Injection
- HTTPoxy
- Shellshock
- Unix/Windows Shell Injection
- Session Fixation
- Scanner/Bot Detection
- Metadata/Error Leakages

### 1.2 OWASP CRS projektin työnkulun ja verkkokaupan ylläpidon näkökulmasta

Projektissa on pyritty mahdollisimman automatisoituun CI/CD-työnkulkuun. Automatisoinnissa on kuitenkin otettava huomioon, ettei ModSecurityn konfiguroinnin täydellinen automatisointi ole mahdollista. ModSecurityn hyödyntämät OWASP CSR -säännöt aiheuttavat - asetuksista riippuen - enemmän tai vähemmän vääriä hälytyksiä, jotka on erikseen säädettävä pois. Toisin sanoen säännöt on "kalibroitava" käytännössä. OWASP CRS hyödyntää neliportaista, ns. Paranoia Level (PS) -asetusta, joka säätää käytössä olevien sääntöjen määrää. Asetus PL 1 on kevein sisältäen vähiten sääntöjä, eikä sen pitäisi käytännössä aiheuttaa vääriä hälytyksiä, mutta toisaalta sen tarjoama suoja on alhainen. Sen sijaan järein asetus PL 4 sisältää paljon sääntöjä ja aiheuttaa erittäin todennäköisesti paljon vääriä hälytyksiä, mutta on herkkä huomaamaan hälyttävältä vaikuttavaa toimintaa. OWASP CRS:n dokumentaation mukaan verkkokaupoille suositellaan PL-asetusta 2.

Käytännössä OWASP CRS:n yksilöllinen säätäminen tuotetulle verkkokaupalle soveltuvaksi vaatii operatiivisen vaiheen työtunteja, jotka _mahdollisesti_ ovat tämän projektin alan ulkopuolella. Tarkentamaton PL-asetus 2 todennäköisesti aiheuttaa kaupan loppukäyttäjälle ongelmia, joidenka ratkaiseminen vaatii teknistä osaamista. Tämä on ristiriidassa projektin tavoitteen kanssa, jonka mukaan lopputuotteen ei tulisi vaatia kauppiaalta teknistä osaamista. 

### 1.3 Dokumentin rakenne

Dokumentin osio 2 kuvaa vaiheittain, kuinka ModSecurity 2.9 asennetaan ja konfiguroidaan Debian-pohjaiseen ympäristöön manuaalisesti, sekä kuinka siihen liitetään OWASP Core Rule Set (CRS) -säännöstö. Manuaalinen ohje on testattu Apache2-serverille kontitetussa debian-ympäristössä.

Osio 3 sisältää kolme erilaista ratkaisua moduulin asentamisen automatisoimiseksi Dockerin avulla.

Dokumentin lopussa on lista virallisesta dokumentaatiosta ja muista hyödyllisistä lähteistä ModSecurityyn liittyen.

#### Lähteitä

ModSecurityn virallinen [Reference Manual](https://github.com/owasp-modsecurity/ModSecurity/wiki/Reference-Manual-(v2.x)).

OWASP CRS:n virallinen dokumentaatio löytyy [täältä](https://coreruleset.org/docs/2-how-crs-works/).

## 2. ModSecurity 2.9 asennus Apache2:lle manuaalisesti

**2.1** Aloita asentamalla ModSecurity Apache-moduuli seuraavalla komennolla:

```bash
apt install libapache2-mod-security2
```
**2.2** Aseta ModSecurityn suositeltu peruskonfiguraatio käyttöön kopioimalla modsecurity.conf-recommended varsinaiseen konfiguraatiotiedostoon modsecurity.conf:

```bash
cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
```


**2.3** Muokkaa ModSecurityn asetustiedostoa /etc/modsecurity/modsecurity.conf niin, että sääntömoottori on päällä:
```bash
nano /etc/modsecurity/modsecurity.conf
```
Vaihda rivi:
```apache
SecRuleEngine DetectionOnly
```
muotoon:
```apache
SecRuleEngine On
```
>**HUOM!** Suosituksena on jättää SecRuleEngine DetectionOnly testausympäristössä ainakin aluksi voimaan. Tuotantoympäristössä tämä muutos on tehtävä, jotta Modsec pysäyttää liikennettä.

**2.4** Lataa OWASP Core Rule Set -säännöt GitHubista:
```bash
git clone https://github.com/coreruleset/coreruleset.git /etc/modsecurity/owasp-crs
```
**2.5** Siirry kansioon, johon OWASP-säännöt ladattiin ja ota oletuskonfiguraatio käyttöön:
```bash
cd /etc/modsecurity/owasp-crs
cp crs-setup.conf.example crs-setup.conf
```
**2.6** Avaa moduulin Apache-konfiguraatiotiedosto muokattavaksi:
```bash
nano /etc/apache2/mods-enabled/security2.conf
```
**2.7** Muokkaa konfiguraatio-tiedoston sisältö vastaamaan tätä:
```apache
<IfModule security2_module>
        # Default Debian dir for modsecurity's persistent data
        SecDataDir /var/cache/modsecurity

        # Include all the *.conf files in /etc/modsecurity.
        # Keeping your local configuration in that directory
        # will allow for an easy upgrade of THIS file and
        # make your life easier
        IncludeOptional /etc/modsecurity/*.conf

        # Include OWASP ModSecurity CRS rules if installed
        # IncludeOptional /usr/share/modsecurity-crs/*.load
        IncludeOptional /etc/modsecurity/owasp-crs/crs-setup.conf
        IncludeOptional /etc/modsecurity/owasp-crs/rules/*.conf
</IfModule>
```

>⚠️ **HUOM!** Varmista, että polut ovat oikein. Virheelliset polut voivat kaataa Apache-palvelimen ja tehdä kontin käyttökelvottomaksi. Voit poistaa kommentoidun rivin, jossa lisätään .load-päätteinen tiedosto.

<br>

**2.8** Tarkista Apache-konfiguraation syntaksi:

```bash
apachectl configtest
```
**2.9** Jos tulos on Syntax OK, lataa Apache uudelleen:

```bash
service apache2 reload
```

**2.10** Testaa, että ModSecurity toimii esimerkiksi tällä komennolla:

```bash
curl "http://localhost/?id=3+or+1=1" -I
```
Jos vastaus on kuten alla, ModSecurity ja OWASP-säännöt ovat toiminnassa:
```bash
HTTP/1.1 403 Forbidden
Date: Tue, 15 Jul 2025 08:47:28 GMT
Server: Apache/2.4.62 (Debian)
Content-Type: text/html; charset=iso-8859-1

```

## 3. ModSecurityn asentaminen ja konfigurointi Dockerin avulla
### 3.1 Yksinkertainen Debian + Apache2 + ModSecurity -kontti
Alla oleva Dockerfile rakentaa imagen, jonka pohjalta voi käynnistää Debian-pohjaisen kontin + Apache2-serverin ja ModSecurity-moduulin valmiiksi konfiguroituna.

Huomioi, että Dockerin täytyy _kopioida_ valmiiksi muokattu ja erikseen tallennettu security2.conf -tiedosto (kts. yllä kohta 2.7) imageen. Kyseinen tiedosto löytyy kontista ilman kopiointiakin, mutta sen muokkaamista ei voi automatisoida esimerkiksi RUN -komennoilla tässä tapauksessa; Kontti käynnistyy ja tiedoston sisältö vaikuttaa olevan oikein, mutta siitä huolimatta ModSecurity ei toimi oikein. On myös mahdollista, että tämä aiheuttaa ongelmia serverin toimintaan. Tämä ongelma liittyy Dockerin toimintaan ja on kierrettävissä kopioimalla valmiiksi muokattu tiedosto imageen.
>⚠️**HUOM!** Tämän dockerfilen käyttämä virallinen php:8.2-apache -baseimage ei vastaa projektin tuotantoympäristöä. Ratkaisua ei ole testattu yhteensopivalla imagella.
```dockerfile
FROM php:8.2-apache

# Päivitä pakettilista ja asenna apache2, mod-security ja git
RUN apt-get update && apt-get install -y \
    git \
    libapache2-mod-security2\
    && rm -rf /var/lib/apt/lists/*

# Ota tarvittavat apache-moduulit käyttöön
RUN a2enmod rewrite headers ssl

# HUOM! SECRULE DETECTION VOI JÄÄDÄ PÄÄLLE TESTAUSYMPÄRISTÖÖN
RUN cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf && \
    sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf

RUN git clone https://github.com/coreruleset/coreruleset.git /etc/modsecurity/owasp-crs && \
    cp /etc/modsecurity/owasp-crs/crs-setup.conf.example /etc/modsecurity/owasp-crs/crs-setup.conf

# VAIHDA TÄHÄN ESIMERKIKSI GITLABIIN LISÄTTY CONFIG-TIEDOSTO
COPY config/security2.conf /etc/apache2/mods-available/security2.conf 

# Run
CMD ["apachectl", "-D", "FOREGROUND"]
```

### 3.2 ModSecurityn asennuksen ja konfiguroinnin integrointi CI/CD-putkeen
Alla on versio tämän hetkisestä CI/CD-putken presta-shop-base-image Dockerfilesta, johon on lisätty ModSecurityn asennus ja konfigurointi.
> ⚠️**HUOM!** Tätä ei ole vielä testattu käytännössä ja voi aiheuttaa serverin kaatumisen.
```Dockerfile
FROM php:7.4-apache
LABEL maintainer="PrestaShop Core Team <coreteam@prestashop.com>"

ENV PS_DOMAIN="<to be defined>" \
DB_SERVER="<to be defined>" \
DB_PORT=3306 \
DB_NAME=prestashop \
DB_USER=root \
DB_PASSWD=admin \
DB_PREFIX=ps_ \
ADMIN_MAIL=demo@prestashop.com \
ADMIN_PASSWD=prestashop_demo \
PS_LANGUAGE=en \
PS_COUNTRY=GB \
PS_ALL_LANGUAGES=0 \
PS_INSTALL_AUTO=0 \
PS_ERASE_DB=0 \
PS_INSTALL_DB=0 \
PS_DEV_MODE=0 \
PS_HOST_MODE=0 \
PS_DEMO_MODE=0 \
PS_ENABLE_SSL=0 \
PS_HANDLE_DYNAMIC_DOMAIN=0 \
PS_FOLDER_ADMIN=admin \
PS_FOLDER_INSTALL=install

# LISÄTTY GIT & MODSECURITY
RUN apt-get update \
    && apt-get install -y libmcrypt-dev \
        libjpeg62-turbo-dev \
        libpcre3-dev \
        libpng-dev \
        libwebp-dev \
        libfreetype6-dev \
        libxml2-dev \
        libicu-dev \
        libzip-dev \
        default-mysql-client \
        wget \
        unzip \
        libonig-dev \
        git \
        libapache2-mod-security2

RUN rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ --with-webp=/usr/include
RUN docker-php-ext-install iconv intl pdo_mysql mbstring soap gd zip bcmath

RUN docker-php-source extract \
    && if [ -d "/usr/src/php/ext/mysql" ]; then docker-php-ext-install mysql; fi \
    && if [ -d "/usr/src/php/ext/mcrypt" ]; then docker-php-ext-install mcrypt; fi \
    && if [ -d "/usr/src/php/ext/opcache" ]; then docker-php-ext-install opcache; fi \
    && docker-php-source delete

# Prepare install and CMD script
COPY config_files/ps-extractor.sh config_files/docker_run.sh config_files/docker_nightly_run.sh /tmp/

# If handle dynamic domain
COPY config_files/docker_updt_ps_domains.php /tmp/

# PHP env for dev / demo modes
COPY config_files/defines_custom.inc.php /tmp/
RUN chown www-data:www-data /tmp/defines_custom.inc.php

# Apache configuration
RUN if [ -x "$(command -v apache2-foreground)" ]; then a2enmod rewrite; fi

# PHP configuration
COPY config_files/php.ini /usr/local/etc/php/

# Setting up ModSecurity for Apache2
RUN cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf && \
    sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf

RUN git clone https://github.com/coreruleset/coreruleset.git /etc/modsecurity/owasp-crs && \
    cp /etc/modsecurity/owasp-crs/crs-setup.conf.example /etc/modsecurity/owasp-crs/crs-setup.conf

# Note! Change the config-file path
COPY config/security2.conf /etc/apache2/mods-available/security2.conf 


# Allow exection for entrypoint
RUN ["chmod", "+x", "/tmp/docker_run.sh"]

# Run
CMD ["/tmp/docker_run.sh"]


# For Debugging purposes only
# CMD ["sleep","3600"]
```

### 3.3 ModSecurityn asentaminen erillisenä konttina
Toinen vaihtoehto on käyttää virallista CRS-konttia. Kontti sisältää Apache-serverin ja oikean ModSecurityn version konfiguroituna.

Käynnissä olevan verkkopalvelimen suojaamiseen riittää, että suojattavan kontin konfiguraatiomuuttujat asetetaan niin, että WAF (ModSecurity-kontti) vastaanottaa pyynnöt ja ohjaa ne taustapalvelimelle.

Alla on esimerkki docker-compose-tiedostosta, jolla voi ladata tarvittavat konttikuvat. Ainoastaan BACKEND-muuttuja täytyy muuttaa, jotta WAF ohjaa liikenteen oikeaan taustapalvelimeen.
```yaml
docker-compose
services:
  modsec2-apache:
    container_name: modsec2-apache
    image: owasp/modsecurity-crs:apache
    environment:
      SERVERNAME: modsec2-apache
      BACKEND: http://<backend server>
      PORT: "80"
      MODSEC_RULE_ENGINE: DetectionOnly
      BLOCKING_PARANOIA: 2
      TZ: "${TZ}"
      ERRORLOG: "/var/log/error.log"
      ACCESSLOG: "/var/log/access.log"
      MODSEC_AUDIT_LOG_FORMAT: Native
      MODSEC_AUDIT_LOG_TYPE: Serial
      MODSEC_AUDIT_LOG: "/var/log/modsec_audit.log"
      MODSEC_TMP_DIR: "/tmp"
      MODSEC_RESP_BODY_ACCESS: "On"
      MODSEC_RESP_BODY_MIMETYPE: "text/plain text/html text/xml application/json"
      COMBINED_FILE_SIZES: "65535"
    volumes:
    ports:
      - "80:80"
```

## Lähteitä
ModSecurityn virallinen [Reference Manual](https://github.com/owasp-modsecurity/ModSecurity/wiki/Reference-Manual-(v2.x)).

OWASP CRS:n virallinen [dokumentaatio](https://coreruleset.org/docs/2-how-crs-works/).

[Ohje](https://www.netnea.com/cms/apache-tutorial-8_handling-false-positives-modsecurity-core-rule-set/) OWASP CRS -sääntöjen säätämiseen.