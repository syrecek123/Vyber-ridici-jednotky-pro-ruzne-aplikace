[Co dodělat ]: #
[pojmy ]: #

# Výběr řídící jednotky pro různé aplikace

$${\color{#FFA500}E9 \space \color{#4682B4}A1 }$$

## Cíle

- **Kategorizovat a porovnat** architektury řídicích systémů (MCU, MPU, embedded systémy, PLC, iPC, programovatelná relé) podle výkonu, paměti, determinismu a spolehlivosti.
- **Analyzovat provozní prostředí a vnější vlivy** (krytí IP, teplotní rozsah, EMC rušení, vibrace) a stanovit požadavky na mechanickou a elektrickou odolnost hardware.
- **Sestavit I/O bilanci** a navrhnout optimální řídicí jednotku z reálných katalogů výrobců pro konkrétní průmyslovou či IoT aplikaci včetně projektové rezervy.
- **Vypracovat vícekriteriální rozhodovací matici** a obhájit zvolenou platformu z technického a ekonomického hlediska (pořizovací cena, náročnost vývoje, údržba a spolehlivost).
- **Provést kritický technický audit (troubleshooting)** nevhodného návrhu řízení, identifikovat bezpečnostní a provozní rizika a navrhnout certifikované řešení v souladu s průmyslovými standardy.

## Ověření cílů

Výběr řídící jednotky pro různé aplikace

1. Příklady řídících jednotek
2. Jejich základní vlastnosti z hlediska výpočetního výkonu a velikosti paměťového prostoru
3. A z hlediska odolnosti
4. Příklady použití v praxi (kde se používají MCU, a kde ř. j. s MPU)

<!--
1. Správné vysvětlení pojmů, architektur a zkratek z oblasti řídicích systémů. 
2. Schopnost posoudit vliv prostředí na výběr hardwaru a dešifrovat IP kód. 
3. Vypracování rozhodovací matice pro volbu vhodné platformy (MCU vs. PLC vs. iPC). 
4. Návrh konkrétní konfigurace řídicí jednotky na základě zadané I/O bilance a provozních podmínek. 
5. Kritická technická oponentura (audit) nevhodně navrženého řešení. 
-->


---

## Úlohy


### 1. Základní pojmy a architektury řídicích jednotek

*Časová dotace: 10–15 minut | Úvodní orientační úloha*

Doplňte do níže uvedené tabulky význam zkratek, základní princip a typický příklad reálného nasazení nebo zástupce:

| Zkratka / Pojem          | Co zkratka znamená (česky / anglicky) | Základní charakteristika (architektura, kde běží program)                                            | Typický zástupce (konkrétní rodina / model) | Příklad reálného nasazení                |
| :----------------------- | :------------------------------------ | :--------------------------------------------------------------------------------------------------- | :------------------------------------------ | :--------------------------------------- |
| **MCU**                  |            Microcontroller Unit/ mikrokontrolér                           | Integrovaný čip (CPU + RAM + Flash na jednom substrátu), deterministický běh bez OS nebo RTOS        | např. ESP32, PIC16LF1xxx, RP2040            |     Chytré termostaty, čidla IoT, dálková ovládání, drobná elektronika                                        |
| **MPU**                  |           microprocessor unit / mikroprocesorová jednotka                               | Samostatný procesor vyžadující externí RAM a úložiště, zpravidla běží plnohodnotný OS (Linux)        |         např. Broadcom BCM2711 (Raspberry Pi 4), NXP i.MX8, Intel Atom                                       |           Routery, multimediální přehrávače, pokladní systémy (POS), smartphony                                  |
| **Embedded**             |         Embedded System / vestavěný systém                                 |         Jednoúčelový počítačový systém zabudovaný do většího zařízení, navržený pro konkrétní řídicí funkce                                                                                                | Embedded PLC, Embedded PC                   | Bílá technika, bankomaty, regulace kotlů |
| **PLC**                  |          Programmable Logic Controller / programovatelný logický automat                                | Průmyslový automat pro cyklické deterministické řízení procesů, vysoká odolnost, modulární/kompaktní |                                  Siemens SIMATIC S7-1200/1500, Allen-Bradley ControlLogix              |     Řízení výrobních linek, balicí stroje, automatizace čističek odpadních vod                                        |
| **iPC**                  |        Industrial PC / průmyslové PC                               |              Vizualizace procesů (SCADA), strojové vidění, pokročilé řízení robotických pracovišť                                                                                        |                                     Beckhoff C60xx, Advantech UNO, Siemens Microbox           |                                          |
| **Programovatelné relé** |     Programmable Relay / programovatelné relé                                  | Zjednodušené kompaktní PLC pro méně náročné úlohy, nahrazuje časovací relé a stykačové kombinace     |                                    LOGO! (Siemens), Zelio Logic (Schneider Electric), EASY (Eaton)         |                  Řízení osvětlení a žaluzií, automatické otevírání bran, malé čerpací stanice                           |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **SoC (System on Chip):** Integrovaný obvod sdružující všechny klíčové elektronické obvody a komponenty celého počítače či elektronického systému na jediném křemíkovém čipu. 
> 	 Systém na čipu. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-06-07 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Syst%C3%A9m_na_%C4%8Dipu
> - **DSP (Digital Signal Processor):** Specializovaný mikroprocesor architektury Harvard optimalizovaný pro matematické výpočty v reálném čase (rychlá Fourierova transformace FFT, filtrace šumu, digitální vektorové řízení střídavých motorů). 
> 	Digitální signálový procesor. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2006, poslední editace 28. 2. 2026 [cit. 2026-09-14]. Dostupné z: [Digitální signálový procesor – Wikipedie](https://cs.wikipedia.org/wiki/Digit%C3%A1ln%C3%AD_sign%C3%A1lov%C3%BD_procesor)
> - **FPGA (Field-Programmable Gate Array):** Programovatelné logické hradlové pole, jehož vnitřní struktura logických bloků a propojení je konfigurovatelná až u zákazníka. Umožňuje masivní paralelní zpracování s hardwarovou latencí v řádu nanosekund. 
> 	Programovatelné hradlové pole. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-01-10 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Programovateln%C3%A9_hradlov%C3%A9_pole


<details>
<summary> :bulb: Tip k doplnění tabulky: </summary>
<p>Zaměřte se na čas náběhu a architekturu: U MCU je kód ve vnitřní paměti Flash procesoru a vykonává se okamžitě po přivedení napájení (řádově milisekundy). U systémů s MPU a iPC musí BIOS/bootloader nejprve zavést jádro operačního systému (OS Linux, Windows) z disku/eMMC/SD karty do operační paměti RAM, což trvá desítky sekund.</p>
</details>

:star2: **Bonusová otázka k úloze 1:**
Proč se u kritických aplikací v letectví (např. systém řízení letu Fly-by-Wire) nebo v jaderné energetice stále upřednostňují jednoduché deterministické mikrořadiče s několika desítkami kilobajtů paměti nebo obvody FPGA před moderními vícejádrovými gigahertzovými procesory s gigabajty RAM?

*Vaše odpověď:*
`...`

---

### 2. Parametry, paměti a provozní odolnost (IP krytí)

*Časová dotace: max. 15 minut | Mírně náročnější úloha propojující parametry a praxi*

1. **Typy pamětí v řídicích jednotkách:**
   - Doplňte porovnání pamětí z hlediska stálosti dat a rychlosti:
     - **RAM:** 
	     - **Je volatilní (energeticky závislá)?** [**Ano** / Ne]
	     - **Rychlost zápisu:** Velmi vysoká (řádově nanosekundy) 
	     - **K čemu se využívá v PLC/MCU:** K ukládání proměnných, se kterými program aktivně pracuje během svého běhu (zásobník, mezivýsledky výpočtů, mezipaměť vstupů a výstupů).
     - **Flash (ROM):** 
	     - **Je volatilní?** [Ano / **Ne**]
	     - **K čemu se využívá v PLC/MCU:** Ke permanentnímu ukládání samotného řídicího programu (firmware) a konstanta/konfiguračních dat, které se neztrácejí ani po vypnutí napájení.
     - **EEPROM / NVRAM:** 
	     - **Je volatilní?** [Ano / **Ne**]
	     - **K čemu se využívá v PLC/MCU:** Ke spolehlivému ukládání provozních dat a nastavení, která se mění jen občas, ale musí zůstat zachována i při výpadku napájení.
   - **Otázka z praxe: Kam se v průmyslovém PLC ukládají aktuální provozní proměnné (např. čítače vyrobených kusů nebo motohodiny), aby se při nečekaném výpadku napájení neztratily (tzv. remanentní / retain data)?**
     - **Odpověď:** Ukládají se do NVRAM (nebo do speciální zálohované RAM pomocí baterie či superkondenzátoru, případně zápisem do EEPROM/Flash při detekci poklesu napětí).

2. **Reálný čas a determinismus (Hard vs. Soft Real-Time):**
   - **Proč pro reakci na nouzové zastavení lisu (požadavek reakce do 5 ms) použijeme PLC či mikrokontrolér s RTOS, a nikoliv běžné Raspberry Pi s operačním systémem Raspberry Pi OS (standardní Linux)?**
     - **Odpověď:** PLC a RTOS zaručují hard real-time (deterministické) chování, což znamená, že reakce proběhne vždy v přesně definovaném časovém limitu. Standardní Linux v Raspberry Pi je soft real-time systém – přeplánování procesů, plánovač OS nebo obsluha přerušení mohou způsobit nepředvídatelné zpoždění (jitter) přesahující 5 ms, což je u bezpečnostních funkcí nepřípustné.

# 2. Parametry, paměti a provozní odolnost (IP krytí)

### Typy pamětí v řídicích jednotkách

* **RAM:**
  * **Je volatilní (energeticky závislá)?** **Ano**
  * **Rychlost zápisu:** **Velmi vysoká** (řádově nanosekundy).
  * **K čemu se využívá v PLC/MCU:** K ukládání proměnných, se kterými program aktivně pracuje během svého běhu (zásobník, mezivýsledky výpočtů, mezipaměť vstupů a výstupů).
* **Flash (ROM):**
  * **Je volatilní?** **Ne**
  * **K čemu se využívá v PLC/MCU:** Ke permanentnímu ukládání samotného **řídicího programu (firmware)** a konstant/konfiguračních dat, které se neztrácejí ani po vypnutí napájení.
* **EEPROM / NVRAM:**
  * **Je volatilní?** **Ne**
  * **K čemu se využívá v PLC/MCU:** Ke spolehlivému ukládání provozních dat a nastavení, která se mění jen občas, ale **musí zůstat zachována i při výpadku napájení**.
* **Otázka z praxe:** Kam se v průmyslovém PLC ukládají aktuální provozní proměnné (např. čítače vyrobených kusů nebo motohodiny), aby se při nečekaném výpadku napájení neztratily (tzv. remanentní / retain data)?
  * **Odpověď:** Ukládají se do **NVRAM** (případně do **zálohované RAM** pomocí baterie/superkondenzátoru, nebo zápisem do **EEPROM/Flash** při detekci poklesu napětí).

---

### Reálný čas a determinismus (Hard vs. Soft Real-Time)

* **Proč pro reakci na nouzové zastavení lisu (požadavek reakce do 5 ms) použijeme PLC či mikrokontrolér s RTOS, a nikoliv běžné Raspberry Pi s operačním systémem Raspberry Pi OS (standardní Linux)?**
  * **Odpověď:** PLC a RTOS zaručují **hard real-time (deterministické)** chování, což znamená, že reakce proběhne **vždy** v přesně definovaném časovém limitu. Standardní Linux v Raspberry Pi je **soft real-time** systém – plánovač OS nebo obsluha přerušení mohou způsobit nepředvídatelné zpoždění (*jitter*) přesahující 5 ms, což je u bezpečnostních funkcí **nepřípustné**.

---

### Odolnost vůči vlivům prostředí a dešifrování kódu IP

* **Dešifrujte kód IP68:**
  * **První číslice (6):** Úplná ochrana před nebezpečným dotykem a **úplná prachotěsnost**.
  * **Druhá číslice (8):** Ochrana proti **trvalému ponoření do vody** za podmínek určených výrobcem.
* **Jaké minimální krytí IP musí mít rozváděč umístěný ve venkovním nekrytém prostředí, kde na něj přímo dopadá déšť a fouká polétavý prach?**
  * **Volba:** `[X] IP65`
  * **Zdůvodnění:** Třída **IP65** poskytuje **úplnou ochranu před prachem** (první číslice 6) a **ochranu proti tryskající vodě** ze všech směrů (druhá číslice 5). Třída IP44 chrání pouze před stříkající vodou a částicemi >1 mm, což pro přímý venkovní déšť a jemný polétavý prach nestačí.

---

### Konstrukční rozdíly kancelářského PC vs. průmyslového iPC

* **Chlazení:**
  * **Kancelářské PC:** Aktivní (ventilátory nasávající prach, náchylné k mechanickému opotřebení).
  * **vs. iPC:** **Pasivní (fanless)**, teplo je odváděno hliníkovým/kovovým šasi.
* **Napájecí napětí a filtrace:**
  * **Kancelářské PC:** Standardní střídavé napětí (230 V AC) bez pokročilé filtrace.
  * **vs. iPC:** Průmyslové **stejnosměrné napájení (24 V DC)** s integrovanou filtrací rušení a ochranou proti přepětí/přepólování.
* **Odolnost proti otřesům a vibracím:**
  * **Kancelářské PC:** Nízká (využívá pohyblivé díly jako HDD a běžné konektory).
  * **vs. iPC:** **Vysoká** (využívá výhradně SSD/eMMC úložiště, zpevněné plošné spoje a zajištěné konektory).
* **Způsob montáže:**
  * **Kancelářské PC:** Na stůl / pod stůl.
  * **vs. iPC:** **Na DIN lištu**, VESA držák nebo do 19" racku rozváděče.

---
---

# 3. Rozhodovací matice platforem (MCU vs. PLC vs. iPC)

| Kritérium hodnocení | Vzorová aplikace 0 (Vjezdová závora) | Aplikace A (Pokojový termostat) | Aplikace B (Balicí linka) | Aplikace C (Kamerová kontrola svarů) |
| :--- | :--- | :--- | :--- | :--- |
| **Doporučená platforma** | **Programovatelné relé / kompaktní PLC** | **MCU / Embedded SoC** | **Modulární PLC** | **Průmyslové PC (iPC)** |
| **Pořizovací cena HW na 1 ks** | **Střední** (cca 3 500 – 6 000 Kč) | **Nízká** (< 500 Kč, cca 100–250 Kč při 10 000 ks) | **Střední** (cca 15 000 – 30 000 Kč) | **Vysoká** (> 50 000 Kč) |
| **Primární programovací jazyk** | **FBD / LAD** (IEC 61131-3) | **C / C++ / MicroPython** (s RTOS) | **IEC 61131-3** (LAD / ST / FBD) | **Python / C++ / C#** (pod OS Linux/Windows) |
| **Klíčový technický argument pro volbu** | Montáž na DIN lištu, integrovaný displej, robustní relé, bez nutnosti vývoje PCB. | Extrémně **nízká spotřeba** (bateriový provoz), nízká cena při velké sérii (10k ks), integrované RF rozhraní (ZigBee/Wi-Fi). | **Deterministické řízení** v reálném čase, vysoká spolehlivost (24/7), modulární I/O, diagnostické LED, snadný servis. | Obrovský **výpočetně-grafický výkon (GPU/NPU pro AI)**, podpora GigE Vision kamer, přímá konektivita k SQL/MES databázím. |
| **Hlavní riziko při volbě špatné platformy** | **MCU:** Nutnost vývoje PCB, rušení.<br>**iPC:** Zbytečně vysoká cena, pomalý start. | **PLC:** Nelze napájet z baterie, obrovské rozměry a cena.<br>**iPC:** Extremně vysoká cena a spotřeba. | **MCU:** Špatná servisovatelnost, rušení na lince, dlouhý vývoj.<br>**iPC:** Chybějící garance determinismu bez SoftPLC. | **MCU:** Nedostatek paměti a výkonu pro 4K snímky a AI.<br>**PLC:** Neschopnost zpracovat obrazová data a spouštět neuronové sítě. |

### 🌟 Bonusová otázka k úloze 3
**Co je to tzv. SoftPLC a jak umožňuje průmyslovému PC (iPC) kombinovat výhody operačního systému Windows/Linux a deterministického řízení reálného času?**

> **Odpověď:**  
> **SoftPLC** je softwarový emulátor / hypervizor, který běží na iPC a vyhražuje jedno nebo více jader procesoru **výhradně pro deterministický běh řídicího programu reálného času (Hard Real-Time)**. Odděluje tím časově kritické řízení od běžného operačního systému (Windows/Linux). Pokud OS Windows zhavaruje (tzv. "modrá obrazovka"), vyhrazené jádro se SoftPLC dál běží bez přerušení a bezpečně řídí stroj.

---
---

# 4. Návrh a konfigurace řídicí jednotky pro čerpací stanici

### I/O bilance a výpočet rezervy (+20 %)

| Typ signálu | Požadavek aplikace (kusy) | Popis signálů v aplikaci | Počet po započtení rezervy (+20 %) |
| :--- | :--- | :--- | :--- |
| **Digitální vstup (DI)** | **4 ks** | 3× plovákový spínač, 1× termistorové ochranné relé | **5 ks** *(po zaokrouhlení)* |
| **Digitální výstup (DO) – reléový** | **2 ks** | 2× cívka spínacího stykače motorů (230 V AC) | **3 ks** *(po zaokrouhlení)* |
| **Digitální výstup (DO) – tranzistorový** | **1 ks** | 1× opticko-akustický maják (24 V DC) | **2 ks** *(po zaokrouhlení)* |
| **Analogový vstup (AI)** | **1 ks** | 1× hydrostatická ponorná sonda (4–20 mA) | **2 ks** *(po zaokrouhlení)* |
| **Analogový výstup (AO)** | **1 ks** | 1× řízení otáček frekvenčního měniče (0–10 V) | **2 ks** *(po zaokrouhlení)* |

---

### Výběr konkrétního hardwaru z katalogu výrobce

* **Výrobce a přesný model CPU:** Siemens SIMATIC S7-1200, CPU 1212C DC/DC/Rly
* **Objednací kód (Part Number):** `6ES7212-1HE40-0XB0`
* **Rozšiřující moduly:** **SM 1234 AI 4 x 13 bit / AO 2 x 14 bit** (Objednací kód: `6ES7234-4HE32-0XB0`) – poskytuje vstupy pro 4–20 mA i výstupy 0–10 V.
* **Napájecí napětí zvolené jednotky:** 24 V DC
* **Odesílání dat na dispečink:** Pomocí integrovaného PROFINET/Ethernet portu na CPU s protokolem **Modbus TCP** (případně doplněním komunikačního modulu **CP 1243-1** pro LTE přenos).
* **Odkaz na technický list (datasheet):** [Siemens Industry Mall - CPU 1212C DC/DC/Rly](https://mall.industry.siemens.com/)

---

### Technické ověření z datasheetu

* **Garantovaný provoz při -20 °C:**  
  * Dle technického listu S7-1200 je rozsah provozních teplot **-20 °C až +60 °C** (při horizontální montáži). Jednotka tento provoz plně podporuje.
* **Spínání cívky stykače 230 V AC:**  
  * Cívky spínáme **přes pomocná pultová/paticová relé (24 V DC / 230 V AC)**, nikoliv přímo výstupy PLC.
  * **Zdůvodnění:** Cívka stykače je indukční zátěž generující při vypnutí napěťové špičky, které opotřebovávají kontakty vestavěného relé v PLC. Pomocné relé slouží jako levně vyměnitelný prvek a zajišťuje **galvanické oddělení**.

---

### Krytí rozváděče a teplotní management

* **Zvolené krytí rozváděče:** **IP65 / IP66** (oceloplechový nebo sklolaminátový rozváděč s litým těsněním).
* **Teplotní management skříně:**
  * **Zima (-20 °C):** Instalace odporového **topného tělesa s termostatem** (např. STEGO 50–100 W).
  * **Léto (+45 °C):** Použití stínicí stříšky (ochrana před přímým sluncem) + **filtroventilační jednotka s termostatem** (případně Peltierův chladicí modul s krytím IP65).

---

### 🌟 Bonusová otázka k úloze 4
**Proč se u čerpadel v čistírnách odpadních vod striktně upřednostňuje měření hladiny pomocí proudového signálu 4–20 mA před napěťovým 0–10 V a proč se do jímky nepoužívá ultrazvukový senzor, pokud v ní vzniká hustá pěna?**

> **Odpověď:**  
> 1. **Proudová smyčka 4–20 mA vs. 0–10 V:** Proudový signál je imunní vůči úbytkům napětí na dlouhém vedení a vůči elektromagnetickému rušení. Navíc princip **„živé nuly“ (4 mA)** umožňuje PLC okamžitě detekovat přerušení vodiče (pokud je proud 0 mA, jde o poruchu).  
> 2. **Ultrazvuk a pěna:** Hustá pěna pohlcuje nebo nekontrolovaně rozptyluje ultrazvukové impulsy. Senzor pak vyhodnocuje falešné odrazy od vrstvy pěny namísto reálné hladiny kapaliny.

---
---

# 5. Technický audit a oponentura nevhodného návrhu

### Protokol o zjištěných vadách

| Oblast auditu | Zjištěná vada v amatérském návrhu | Fyzikální mechanismus selhání | Následek pro stroj nebo obsluhu |
| :--- | :--- | :--- | :--- |
| **Elektromagnetická kompatibilita (EMC)** | Použití Arduina a čínských relé bez odrušení. | Napěťové špičky z indukční zátěže ventilů se indukují do nestíněných vodičů MCU, což způsobí zarušení sběrnic a **přetékání paměti / restart MCU**. | Ztráta kontroly nad lisem, neočekávaný pohyb nebo zamrznutí v mezipoloze. |
| **Mechanická a teplotní odolnost** | Krabička z PLA vytištěná na 3D tiskárně přišroubovaná přímo na lis. | Skelný přechod PLA je již kolem **60 °C**. Vibrace lisu deformují plast a dynamické namáhání ničí cesty plošného spoje. | Rozpad krytu, zkrat vývodů o konstrukci a mechanické zničení elektroniky. |
| **Konektivita a propojení vodičů** | Propojení pomocí nepájených DuPont propojovacích kabelů. | Vibrace lisu způsobí vytřesení pinů z konektorů, vznik mikrooblouků, oxidaci a **studené spoje**. | Náhodné výpadky signálů, přerušení řízení a riziko vzniku požáru. |
| **Funkční bezpečnost (Safety)** | E-Stop je zapojen přímo do pinu D2 Arduina jako softwarové přerušení. | Při zamrznutí programu nebo zacyklení procesor **přerušení vůbec neobslouží**. | **Fatální selhání:** Nejsou odpojeny akční členy a lis přimáčkne obsluhu bez možnosti zastavení. |

---

### Návrh profesionálního nápravného řešení

* **Náhrada řídicí jednotky:** Certifikované průmyslové PLC / programovatelné relé (např. **Siemens LOGO! 24RCE** nebo **Siemens S7-1200**) s montáží na DIN lištu v samostatném rozváděči.
* **Náhrada napájecího zdroje:** Průmyslový spínaný zdroj **24 V DC na DIN lištu** (např. **Mean Well NDR-120-24**) s integrovaným EMC filtrem a přepěťovou ochranou.
* **Způsob zapojení bezpečnostního okruhu (Safety):**
  * Tlačítko E-Stop **nesmí** spoléhat na software mikrokontroléru.
  * *Zapojení:* Dvoukanálové zapojení tlačítka E-Stop do **hardwarového bezpečnostního relé** (např. *Pilz PNOZ* nebo *Schneider Preventa*). Toto relé **přímo galvanicky odpojuje silové napájení** ventilů hydrauliky. PLC dostává pouze pomocný informační vstup.

---

### 🌟 Bonusová otázka k úloze 5
**Proč hobby reléové moduly určené pro Arduino v průmyslovém rozváděči často shoří nebo způsobí trvalé sepnutí zátěže (tzv. přivaření kontaktů), i když jmenovitý proud relé je 10 A a cívka stykače odebírá jen 0,5 A?**

> **Odpověď:**  
> Hobby relé používají nekvalitní materiály kontaktů bez zhasínacích komor. Cívka stykače představuje **silnou indukční zátěž**. Při rozpojení obvodu vzniká elektrický oblouk s vysokou teplotou, který odpaří materiál kontaktů a **přivaří je k sobě (mikrosvár)**. Relé pak zůstane trvale sepnuté i po odpojení řídicího napětí.

---
---

# 6. TCO a životní cyklus v automatizaci

### Srovnání variant z hlediska životního cyklu (10–15 let)

| Aspekt životního cyklu | Varianta 1 (Custom Embedded MCU) | Varianta 2 (Průmyslové PLC) |
| :--- | :--- | :--- |
| **Dostupnost náhradních dílů za 10 let** | **Velmi nízká.** Čipy se přestávají vyrábět, deska se nedá koupit, nutný kompletní re-design PCB. | **Vysoká.** Výrobci garantují dostupnost náhradních dílů a kompatibilitu **10–20 let**. |
| **Servisovatelnost podnikovým elektrikářem** | **Nulová.** Elektrikář nemůže upravit C/C++ kód ani vyměnit diskrétní součástky na PCB. | **Vysoká.** Elektrikář vymění modul kus za kus a kód upraví v normovaném IDE (LAD). |
| **Doba odstávky linky při poruše CPU** | **Dny až týdny.** Čekání na vývoj nového HW, ruční pájení a nahrávání kódu bez dokumentace. | **Desítky minut.** Pouhá výměna zálohovaného modulu na DIN liště a nahrání programu. |
| **Cena vývojových nástrojů a licencí IDE** | **Nízká / Zdarma** (open-source kompilátory GCC, VS Code). | **Střední až vysoká** (licence TIA Portal / RSLogix / EcoStruxure). |
| **Závěrečné doporučení** | **Nevhodné:** Extrémní riziko nákladných odstávek zničí jakoukoliv úsporu na pořizovací ceně HW. | **Jednoznačná volba:** Vyšší počáteční CAPEX bude v horizontu let vyvážen nízkým OPEX a vysokou spolehlivostí (nízké TCO). |

---

### 🌟 Bonusová otázka k úloze 6
**Co znamená pojem MTBF (Mean Time Between Failures) v datasheetech průmyslových řídicích jednotek a jaký vliv má okolní teplota v rozváděči na tuto hodnotu (tzv. Arrheniovo pravidlo)?**

> **Odpověď:**  
> * **MTBF (Mean Time Between Failures):** Střední doba mezi poruchami – Udává statistickou provozní spolehlivost a životnost zařízení v hodinách.
> * **Arrheniovo pravidlo:** Rychlost chemických a fyzikálních degradačních procesů v elektronice roste s teplotou. Pravidlo říká, že **každý nárůst provozní teploty o 10 °C zkracuje životnost elektronických součástek (a tedy hodnotu MTBF) přibližně na polovinu**.
