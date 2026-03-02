# AWS AI Practitioner Vizsga – Tananyag-összefoglaló

---

# DOMAIN 1: A mesterséges intelligencia és a gépi tanulás alapjai

## 1.1 Alapfogalmak és terminológia

### MI (AI), Gépi tanulás (ML), Mélytanulás (Deep Learning)

- **Mesterséges intelligencia (AI)**: A számítástechnika azon területe, amely olyan rendszereket hoz létre, amelyek emberi intelligenciát igénylő feladatokat oldanak meg (tanulás, alkotás, képfelismerés, döntéshozatal).
- **Gépi tanulás (ML)**: Az AI egyik ága – algoritmusok és statisztikai modellek segítségével a gép adatokból tanul, nem explicit programozással. Mintákat azonosít és előrejelzéseket készít.
- **Mélytanulás (Deep Learning)**: Az ML egy fajtája, amely neurális hálózatokat használ több réteggel. Különösen hatékony strukturálatlan adatoknál (képek, szöveg, hang).
- **Generatív AI**: A mélytanulás legújabb formája – új, eredeti tartalmat generál (szöveg, kép, videó, zene, kód). Transformer architektúrát és nagy nyelvi modelleket (LLM) használ.

### Adat típusok

| Típus | Leírás | Tárolás | Példa |
|-------|--------|---------|-------|
| **Strukturált** | Táblázatos, sorok és oszlopok | Amazon RDS, Redshift, S3 | CSV, SQL táblák |
| **Félig strukturált** | Nem teljesen táblázatos, eltérő attribútumok lehetségesek | DynamoDB, DocumentDB | JSON, XML |
| **Strukturálatlan** | Nem táblázatos, nincs fix séma | Amazon S3 | Képek, videók, szövegfájlok, social media posztok |
| **Idősoros (Time series)** | Időbélyeggel ellátott, szekvenciális adatok | Amazon S3 | Szenzor-adatok, teljesítménymetrikák |

> **Fontos**: Az Amazon S3 az elsődleges forrás a betanítási adatokhoz – bármilyen típusú adatot tárolhat, alacsony költségű, és gyakorlatilag korlátlan kapacitású.

### Modell-betanítás alapfogalmai

- **Algoritmus**: Matematikai kapcsolatot definiál a bemenetek és kimenetek között.
- **Jellemzők (features)**: Az adatok bemeneti tulajdonságai (oszlopok, pixelek stb.).
- **Paraméterek/súlyok (weights)**: A modell belső értékei, amelyeket a betanítás során iteratívan módosítanak a hiba minimalizálásáig.
- **Következtetés (inference)**: A betanított modell előrejelzése új adatokra – mindig valószínűségi eredmény.
- **Modell-artefaktumok**: A betanítás kimenetei (betanított paraméterek, modelldefiníció, metaadatok) – Amazon S3-ban tárolják.

### Következtetés (Inference) típusai

| Típus | Mikor használjuk? | Jellemző |
|-------|-------------------|----------|
| **Valós idejű (Real-time)** | Alacsony késleltetés, azonnali válasz szükséges | Állandóan futó végpont (endpoint) |
| **Kötegelt (Batch)** | Nagy adatmennyiség, az eredmény várhat | Erőforrások csak futás közben aktívak – költséghatékonyabb |

### Tanulási stílusok

| Típus | Adat | Jellemző | Példa |
|-------|------|----------|-------|
| **Felügyelt tanulás (Supervised)** | Címkézett (labeled) | Ismert bemenet-kimenet párokból tanul | Képosztályozás (hal/nem hal), spamszűrés |
| **Felügyelet nélküli (Unsupervised)** | Címkézetlen | Mintákat, csoportokat fedez fel | Klaszterezés, anomália-detekció |
| **Megerősítéses tanulás (Reinforcement)** | Nincs címke, van cél | Próba-hiba alapú, jutalmakkal tanul | AWS DeepRacer |

### Túltanulás, alultanulás, torzítás

- **Túltanulás (Overfitting)**: A modell a betanító adatokra túl jól illeszkedik, új adatokra rosszul teljesít. Megoldás: változatosabb betanító adat.
- **Alultanulás (Underfitting)**: A modell nem talál érdemi összefüggést. Megoldás: több adat, hosszabb betanítás.
- **Torzítás (Bias)**: A modell bizonyos csoportok számára kedvezőtlenül működik az egyoldalú betanító adat miatt. Megoldás: kiegyensúlyozott adathalmaz, jellemzők súlyának módosítása, folyamatos monitoring.

### Neurális hálózatok és mélytanulás

- Rétegekből álló csomóponthálózat: bemeneti réteg → rejtett rétegek → kimeneti réteg.
- Minden csomópont súlyokat rendel a jellemzőkhöz; az információ előrefelé áramlik.
- **Előny**: Nem kell előre megadni a fontos jellemzőket – a hálózat maga azonosítja a mintákat.
- **Hátrány**: Sokkal nagyobb számítási kapacitás és adat szükséges, drágább.
- **Hagyományos ML vs. mélytanulás**: Strukturált adathoz → hagyományos ML; strukturálatlan adathoz (kép, videó, szöveg) → mélytanulás.

### Generatív AI kulcsfogalmak

- **Transformer**: A generatív AI magja – párhuzamosan dolgozza fel a szekvenciákat (gyorsabb, mint az RNN).
- **LLM (Large Language Model)**: Milliárdnyi paraméterrel rendelkező, hatalmas szövegkorpuszon betanított modell.
- **Prompt**: A felhasználó által megadott bemenet a modell számára.
- **Completion**: A modell által generált válasz/kimenet.

---

## 1.2 Az AI gyakorlati felhasználási esetei

### Mikor ÉRDEMES AI-t használni?
- Ismétlődő, monoton feladatok automatizálása
- Hatalmas adatmennyiség elemzése nagy sebességgel
- Mintafelismerés, anomália-detekció, csalásfelderítés
- Kereslet-előrejelzés, prediktív karbantartás
- Számítógépes látás (computer vision), nyelvfeldolgozás (NLP)

### Mikor NEM érdemes AI-t használni?
- A költségek meghaladják a várható megtakarítást
- Teljes átláthatóság / determinisztikus eredmény szükséges (→ szabályalapú rendszer)
- A modell értelmezhetősége üzleti/jogi követelmény (komplex neurális hálók → „fekete doboz")
- **Determinisztikus vs. probabilisztikus**: Szabályalapú rendszer = ugyanaz a bemenet mindig ugyanazt a kimenetet adja. ML modell = valószínűségi – azonos bemenetre eltérő eredményeket ad.

### ML problématípusok

**Felügyelt tanulás:**
- **Osztályozás (Classification)**:
  - *Bináris*: Két lehetséges kimenet (beteg/egészséges, spam/nem spam)
  - *Többosztályos (Multiclass)*: Több kategória (dokumentum témája, állatfaj)
- **Regresszió (Regression)**:
  - *Lineáris regresszió*: Folytonos érték becslése (magasság súly alapján, házárak)
  - *Logisztikus regresszió*: Esemény bekövetkezésének valószínűsége (0 és 1 között) (szívbetegség, csalás)

**Felügyelet nélküli tanulás:**
- **Klaszterezés**: Adatok csoportosítása hasonlóság alapján (ügyfélszegmentáció)
- **Anomália-detekció**: Rendellenes minták azonosítása (szenzor-meghibásodás, hálózati biztonsági incidensek)

### AWS előre betanított AI szolgáltatások

| Szolgáltatás | Funkció |
|-------------|---------|
| **Amazon Rekognition** | Képek és videók elemzése – arcfelismerés, objektumdetekció, tartalommoderáció |
| **Amazon Textract** | Szöveg, kézírás, táblázatok kinyerése szkennelt dokumentumokból |
| **Amazon Comprehend** | NLP – szövegben érzelmek, PII, entitások detektálása |
| **Amazon Lex** | Hang- és szöveges chatbotok építése (Alexa technológia) |
| **Amazon Transcribe** | Automatikus beszédfelismerés (100+ nyelv), élő és rögzített hang/videó átírata |
| **Amazon Polly** | Szöveg → természetes hangzású beszéd (több tucat nyelv) |
| **Amazon Kendra** | Intelligens vállalati keresés NLP alapon |
| **Amazon Personalize** | Személyre szabott ajánlórendszer |
| **Amazon Translate** | Szövegfordítás 75 nyelv között neurális hálózattal |
| **Amazon Fraud Detector** | Online csalás detektálása (fizetés, hamis fiókok) előre betanított modellekkel |
| **Amazon Bedrock** | Teljesen menedzselt generatív AI szolgáltatás – alapmodell (FM) választás, testreszabás, RAG |
| **Amazon SageMaker** | Egyedi ML modellek építése, betanítása, telepítése – teljes ML életciklus |

---

## 1.3 Az ML fejlesztési életciklus

### ML pipeline lépései

1. **Üzleti cél meghatározása** → mérhető sikerességi kritériumok, költség-haszon elemzés
2. **Adat gyűjtés és előkészítés** → ETL, címkézés, jellemző-kiválasztás
3. **Modell betanítása, hangolása, értékelése** → kísérletek, hiperparaméter-hangolás
4. **Telepítés (Deployment)** → valós idejű vagy kötegelt végpont
5. **Monitorozás** → adatsodródás (data drift), koncepcióváltás (concept drift) detektálás

### Adat-előkészítés AWS szolgáltatásai

| Szolgáltatás | Funkció |
|-------------|---------|
| **AWS Glue** | Teljesen menedzselt ETL szolgáltatás – adatfeltárás, transzformáció, betöltés |
| **AWS Glue Data Catalog** | Metaadat-katalógus (séma, helyszín) – kereshető és lekérdezhető |
| **AWS Glue DataBrew** | Vizuális adat-előkészítő eszköz (250+ beépített transzformáció, kód nélkül) |
| **SageMaker Ground Truth** | Adat-címkézés – gépi + emberi munkaerő (Mechanical Turk) |
| **SageMaker Canvas** | Vizuális felületű adatelőkészítés, 300+ beépített transzformáció, kód nélkül |
| **SageMaker Feature Store** | Jellemzők (feature-ök) központi tárolása, megosztása, újrafelhasználása |

### Modell betanítás és hangolás

- **SageMaker Training Job**: Betanító kód futtatása a SageMaker által menedzselt ML számítási erőforrásokon. A Docker konténerben lévő algoritmust S3-ból kapott adatokon futtatja.
- **SageMaker Experiments**: Kísérletek létrehozása, összehasonlítása, metrikák alapján legjobb modell kiválasztása.
- **SageMaker Automatic Model Tuning (AMT)**: Automatikus hiperparaméter-hangolás – a legjobb kombinációt keresi a megadott tartományon belül.

### Telepítési opciók SageMaker-ben

| Opció | Jellemző |
|-------|----------|
| **Real-time** | Állandó végpont, azonnal válaszol, auto-skálázás |
| **Batch Transform** | Offline, nagy adathalmazra, erőforrások csak futáskor aktívak |
| **Asynchronous** | Sorba állított kérések, nagy payload, nullára skáláz inaktivitáskor |
| **Serverless** | Lambda-alapú, nem kell infrastruktúrát menedzselni, fizess-amit-használsz |

### Modell monitorozás

- **SageMaker Model Monitor**: Valós idejű monitorozás, adatminőség és modellminőség összehasonlítása baseline-nal.
- **Adatsodródás (Data drift)**: Az adatok eloszlása megváltozik a betanító adathoz képest.
- **Koncepcióváltás (Concept drift)**: A célváltozó tulajdonságai változnak.
- Mindkettő modell-teljesítmény romláshoz vezet → újratanítás szükséges.

### MLOps

- Szoftvermérnöki legjobb gyakorlatok alkalmazása az ML modellekre.
- Automatizálás, verziókezelés (adat, kód, modell), monitorozás, újratanítás.
- **SageMaker Pipelines**: ML pipeline-ok összeállítása és automatizálása.
- **AWS Step Functions**: Vizuális, szerverless workflow-építő.
- **Amazon MWAA (Managed Workflows for Apache Airflow)**: Nyílt forráskódú workflow-menedzsment.

### Értékelési metrikák

**Osztályozási modellek (Confusion Matrix alapján):**

| Metrika | Képlet | Mikor használjuk? |
|---------|--------|-------------------|
| **Pontosság (Accuracy)** | (TP+TN) / Összes | Általános teljesítmény – NEM jó kiegyensúlyozatlan adatnál |
| **Precizitás (Precision)** | TP / (TP+FP) | Ha a hamis pozitívokat akarjuk minimalizálni (pl. spam szűrő) |
| **Visszahívás (Recall)** | TP / (TP+FN) | Ha a hamis negatívokat akarjuk minimalizálni (pl. betegség diagnózis) |
| **F1 Score** | 2×(Precision×Recall)/(Precision+Recall) | Precizitás és visszahívás közti egyensúly |
| **AUC (Area Under Curve)** | ROC görbe alatti terület | Bináris osztályozók összehasonlítása; 1=tökéletes, 0.5=véletlenszerű |

**Regressziós modellek:**

| Metrika | Leírás |
|---------|--------|
| **MSE (Mean Squared Error)** | Hibák négyzetének átlaga – kiugró értékeket hangsúlyozza |
| **RMSE (Root MSE)** | MSE gyöke – az eredeti mértékegységben |
| **MAE (Mean Absolute Error)** | Hibák abszolút értékének átlaga – nem hangsúlyozza a kiugrókat |

### Üzleti metrikák
- Költségcsökkentés, felhasználók/eladások növekedése, ügyfélelégedettség javulása
- ROI kiszámítása: tényleges eredmények vs. eredeti üzleti célok
- **AWS Cost Explorer + költségallokációs címkék**: AWS erőforrások tényleges költségének nyomon követése projektenként

---

# DOMAIN 2: A generatív AI alapjai

## 2.1 Generatív AI alapfogalmak

### Mi a generatív AI?
- A mélytanulás egy részhalmaza, amely **új, eredeti tartalmat** generál (szöveg, kép, hang, videó, kód).
- **Alapmodelleken (Foundation Models, FM)** alapul, amelyeket hatalmas adathalmazokon tanítottak be.
- Az FM-ek milliárdnyi paraméterrel rendelkeznek – minél több paraméter, annál többre képes a modell.

### Transformer architektúra
- A generatív AI magja – a 2017-es „Attention Is All You Need" cikkben mutatták be.
- **Párhuzamos feldolgozás**: A korábbi RNN-ekkel szemben a transformer egyszerre dolgozza fel a teljes bemeneti szekvenciát.
- **Önfigyelem (Self-attention)**: A modell súlyozza a bemenet különböző részeinek fontosságát – hosszú távú függőségek megragadása.
- **Pozíciókódolás (Positional encoding)**: A tokenek sorrendjének megőrzése.
- Részei: Encoder (kódoló) + Decoder (dekódoló), rétegekből áll.

### Kulcsfogalmak

| Fogalom | Jelentés |
|---------|---------|
| **Prompt** | A felhasználó bemenete a modell számára |
| **Completion** | A modell által generált válasz |
| **Token** | A szöveg elemi egysége (szó, szórészlet) – a modellek tokenekkel dolgoznak |
| **Tokenizáló (Tokenizer)** | Szöveget tokenekké alakít |
| **Kontextusablak (Context window)** | A maximális tokenszám, amit a modell egyszerre képes feldolgozni |
| **Beágyazás (Embedding)** | Tokenek numerikus vektoros reprezentációja – szemantikai jelentést kódol |
| **Vektor** | Számok rendezett listája, amely jellemzőket vagy fogalmakat reprezentál egy térben |
| **Kontextuson belüli tanulás (In-context learning)** | Példák megadása a promptban a jobb eredmény érdekében |

### Következtetési (inference) példatípusok

| Típus | Leírás |
|-------|--------|
| **Zero-shot** | Nincs példa a promptban – a modell az előzetes tudására támaszkodik |
| **One-shot** | Egy példa a promptban |
| **Few-shot** | Néhány példa a promptban a jobb eredmény érdekében |

### Unimodális vs. multimodális modellek
- **Unimodális**: Egyféle adattípussal dolgozik (pl. LLM = szöveg → szöveg).
- **Multimodális**: Többféle adattípust kezel egyszerre (szöveg + kép + hang) → képfeliratozás, vizuális kérdésmegválaszolás, szöveg→kép generálás.

### Diffúziós modellek
- Véletlenszerű zajból kiindulva fokozatosan tisztítják ki a képet/hangot.
- **Stabil diffúzió (Stable Diffusion)**: Csökkentett méretű latens térben dolgozik (nem pixel szinten).
- Előnyök a GAN-okkal szemben: magasabb minőség, nagyobb diverzitás, stabilabb betanítás.
- Példák: Stable Diffusion (kép), Whisper (beszédfelismerés), AudioLM (hang).

### Generatív AI felhasználási esetek
- Szöveggenerálás és -összefoglalás
- Kódgenerálás (Amazon Q Developer)
- Képgenerálás (Amazon Titan Image Generator)
- Fordítás, chatbotok, keresőmotorok
- Információ-kinyerés, osztályozás, személyre szabott ajánlások

### Generatív AI projekt-életciklus
1. **Felhasználási eset azonosítása** → a hatókör pontos definiálása
2. **Modellkiválasztás** → saját betanítás vagy meglévő FM használata
3. **Adaptálás, igazítás, bővítés** → prompt engineering, fine-tuning, RLHF
4. **Értékelés** → metrikák, benchmarkok
5. **Telepítés és iteráció**
6. **Monitorozás**

---

## 2.2 A generatív AI képességei és korlátai

### Előnyök
- Adaptálhatóság, sokféle feladatra alkalmas
- Költséghatékonyabb AI-alkalmazás fejlesztés
- Gyors reakcióidő, természetes nyelvi interakció

### Korlátok és kockázatok
- **Hallucinációk**: A modell hihető, de hamis információt generál – mindig ellenőrizni kell hiteles forrással.
- **Toxikus tartalom**: Ha a betanító adat tartalmaz sértő tartalmat, a modell is produkálhat ilyet.
- **Nem emlékezik**: Minden prompt független – a modell nem tanul a korábbi beszélgetésekből (csak fine-tuning-gal).
- **Nem gondolkodik**: Nem érvel, hanem statisztikai alapon generálja a következő tokent.

### LLM értékelési metrikák
- **ROUGE (Recall-Oriented Understudy for Gisting Evaluation)**: Összefoglaló feladatok értékelése – a generált szöveget referenciával hasonlítja össze.
- **BLEU (Bilingual Evaluation Understudy)**: Fordítási feladatok értékelése – gépi fordítás minőségének mérése.

### Modellkiválasztási szempontok
- Modell típus, teljesítmény, méret, költség, latencia
- Felhasználási eset illeszkedése
- Értelmezhetőség vs. teljesítmény kompromisszum

### Üzleti metrikák generatív AI-hoz
- Pontosság, hatékonyság, konverziós ráta, ügyfélélettartam-érték (CLTV)
- Cross-domain teljesítmény
- Hibaarány, feladat-befejezési ráta

---

## 2.3 AWS infrastruktúra és technológiák generatív AI-hoz

### Az AWS generatív AI előnyei
- Alacsony belépési küszöb, hatékonyság, költséghatékonyság
- Gyors piacra jutás, vállalati szintű biztonság és adatvédelem
- **Transfer learning**: Előre betanított modell új adathalmazra való alkalmazása – gyorsabb és olcsóbb

### AWS ML Stack – 3 réteg

| Réteg | Leírás | Példa szolgáltatások |
|-------|--------|---------------------|
| **Infrastruktúra** | Számítási erőforrások, AI chipek | EC2 Trn1 (Trainium), Inferentia, GPU-k (P4, P5, G5, G6), Nitro System |
| **ML szolgáltatások** | Modellek betanítása, hangolása, telepítése | SageMaker, Bedrock |
| **AI szolgáltatások** | Előre betanított, API-n elérhető szolgáltatások | Rekognition, Comprehend, Translate stb. |

### Kulcs AWS szolgáltatások

- **Amazon Bedrock**: Menedzselt generatív AI – több FM-hez hozzáférés API-n (Amazon Titan, Cohere, Stability AI stb.), fine-tuning, RAG, Guardrails.
- **SageMaker JumpStart**: Modell-hub – előre betanított modellek kiválasztása, fine-tuning, telepítés.
- **Amazon Titan**: Az Amazon saját alapmodellje (szöveggenerálás, képgenerálás).
- **PartyRock**: Amazon Bedrock-ra épülő playground – generatív AI alkalmazások építése tanulási célra.

### Árazási modellek
- **Token-alapú árazás**: A feldolgozott tokenek száma alapján fizetsz (bemenet + kimenet).
- **Saját infrastruktúra**: Számítási erőforrások + esetleges licencdíj.
- AWS Pay-as-you-go: Skálázható, nincs előzetes befektetés.

### Biztonsági szempontok
- **AWS Nitro System**: Speciális hardver – senki nem férhet hozzá a munkaterhelésekhez vagy adatokhoz.
- AI rendszerek sérülékenységei: prompt injection, adat-mérgezés (data poisoning), modell-inverzió.
- Titkosítás, többfaktoros hitelesítés, folyamatos monitorozás szükséges.

---

# DOMAIN 3: Alapmodellek alkalmazása

## 3.1 Tervezési szempontok alapmodellt használó alkalmazásokhoz

### Modellkiválasztási kritériumok
- **Költség**: Betanítási és üzemeltetési költség vs. pontosság kompromisszum
- **Latencia**: Valós idejű alkalmazásokhoz gyors inference szükséges
- **Modalitás**: Szöveg, kép, hang, multimodális
- **Modellméret és összetettség**: Nagyobb modell = képesebb, de drágább
- **Testreszabhatóság**: Mennyire módosítható a konkrét feladathoz
- **Bemenet/kimenet hossza**: Kontextusablak mérete
- **Többnyelvűség**: Szükséges-e több nyelv támogatása

### Értelmezhetőség vs. teljesítmény
- **Értelmezhetőség (Interpretability)**: Egyszerű modellek (lineáris regresszió, döntési fa) – átlátható, de gyengébb teljesítmény.
- **Magyarázhatóság (Explainability)**: Komplex modellek fekete dobozként kezelve – a bemenet-kimenet megfigyelésével magyarázható.
- FM-ek NEM értelmezhetőek tervezésük szerint (milliárdnyi paraméter) → „fekete doboz".

### Inference paraméterek

| Paraméter | Hatás |
|-----------|-------|
| **Temperature** | A véletlenszerűség mértéke – alacsony = determinisztikusabb, magas = kreatívabb |
| **Top K** | A legvalószínűbb K token közül választ |
| **Top P** | A kumulatív valószínűség P%-áig terjedő tokenek közül választ |
| **Válaszhossz** | A generált válasz maximális hossza |
| **Stop szekvenciák** | A generálás leállítási feltétele |

### Retrieval Augmented Generation (RAG)

- **Mi az?**: A generatív modell külső tudásbázisból kér le információt a válasz generálásakor.
- **Miért fontos?**: Csökkenti a hallucinációkat, naprakész információt biztosít, domain-specifikus tudást ad.
- **Működés**: Prompt → Query encoder → Vektor-adatbázis keresés → Releváns dokumentumok → Kiegészített prompt → LLM → Válasz.
- **Két komponens**: Retriever (kereső) + Generator (generáló).

### Vektor-adatbázisok

| Fogalom | Leírás |
|---------|--------|
| **Vektor-adatbázis** | Adatok matematikai reprezentációként (embedding vektorok) vannak tárolva |
| **Embedding** | Az adatok numerikus vektoros reprezentációja, amely a szemantikai jelentést kódolja |
| **Szemantikus keresés** | Hasonló jelentésű tartalom keresése vektorok alapján (nem kulcsszó alapon) |

**AWS vektor-adatbázis szolgáltatások:**
- Amazon OpenSearch Service (+ Serverless)
- Amazon Aurora
- Amazon Neptune
- Amazon DocumentDB (MongoDB kompatibilitás)
- Amazon RDS for PostgreSQL (pgvector kiterjesztés)
- Knowledge Bases for Amazon Bedrock (menedzselt RAG)

### Ágensek (Agents for Amazon Bedrock)
- Automatikusan lebontják a feladatokat és generálják a szükséges logikát.
- API-kon keresztül csatlakoznak adatbázisokhoz.
- Tudásbázisokat hívnak meg a válaszok pontosítására.
- Többlépéses feladatok automatizálása (pl. foglalás, rendelés feldolgozás).

---

## 3.2 Prompt engineering technikák

### Prompt komponensei
1. **Feladat/utasítás** – mit kell csinálnia a modellnek
2. **Kontextus** – háttérinformáció
3. **Bemenet** – a feldolgozandó adat
4. **Kimeneti formátum** – hogyan nézzen ki a válasz

### Prompt technikák

| Technika | Leírás |
|----------|--------|
| **Zero-shot** | Példa nélküli utasítás |
| **One-shot** | Egy példa a promptban |
| **Few-shot** | Néhány példa a pontosabb eredményért |
| **Chain-of-thought** | Gondolkodási lépésekre bontás – javítja a minőséget és koherenciát |
| **Prompt tuning** | A prompt szöveg cseréje tanulható, folyamatos embedding vektorra |
| **Prompt sablon (Template)** | Előre definiált struktúra különböző feladatokhoz |

### Latens tér (Latent Space)
- A modell kódolt tudásbázisa – az adatminták tárolása, amelyekből a válaszokat generálja.
- Ha a modell latens tere nem tartalmaz elegendő tudást egy témáról → **hallucináció** (statisztikailag helyes, de tényszerűen hibás válasz).

### Prompt engineering legjobb gyakorlatai
1. Legyél konkrét – formátum, stílus, hossz, kontextus
2. Adj példákat
3. Iteratív tesztelés
4. Ismerd a modell erősségeit és korlátait
5. Egyensúlyozz az egyszerűség és a részletesség között
6. Adj guardrail-eket (biztonsági korlátok)

### Prompt engineering kockázatai

| Kockázat | Leírás |
|----------|--------|
| **Prompt injection** | Rosszindulatú utasítások becsempészése a promptba |
| **Jailbreaking** | A guardrail-ek megkerülésének kísérlete |
| **Hijacking** | Az eredeti prompt módosítása új utasításokkal |
| **Poisoning** | Káros utasítások beágyazása üzenetekbe, weboldalakba |

### Guardrails for Amazon Bedrock
- Tartalomszűrés (gyűlölet, sértés, szexuális tartalom, erőszak) konfigurálható küszöbökkel
- Témák tiltása természetes nyelvi leírással
- PII detektálás és szerkesztés
- Prompt attack-ek (injection, jailbreak) elleni védelem

---

## 3.3 Alapmodellek betanítása és finomhangolása

### Fő módszerek

| Módszer | Leírás |
|---------|--------|
| **Előtanítás (Pre-training)** | Hatalmas, címkézetlen adaton, önfelügyelt tanulással – GPU millió óra, TB-PB adat |
| **Finomhangolás (Fine-tuning)** | Felügyelt tanulás címkézett adattal egy specifikus feladatra |
| **Folyamatos előtanítás (Continuous pre-training)** | Új adatokkal bővítjük a modell tudását idővel |

### Finomhangolás típusai

| Típus | Leírás |
|-------|--------|
| **Teljes finomhangolás** | Minden paraméter módosul – magas költség, katasztrofikus felejtés kockázata |
| **PEFT (Parameter-Efficient Fine-Tuning)** | Csak kis számú adapter réteg/paraméter módosul – kevesebb számítás, memória |
| **LoRA (Low-Rank Adaptation)** | Népszerű PEFT technika – az eredeti súlyokat fagyasztja, alacsony rangú mátrixokat tanít |
| **ReFT (Representation Fine-Tuning)** | A rejtett reprezentációkon tanul feladat-specifikus beavatkozásokat |
| **Multitask fine-tuning** | Több feladatra egyszerre finomhangol – csökkenti a katasztrofikus felejtést |
| **Domain adaptation** | Domain-specifikus adatokra adaptálja a modellt (szakzsargon, speciális terminológia) |
| **RLHF** | Emberi visszajelzéssel történő megerősítéses tanulás – a modell jobban igazodik az emberi preferenciákhoz |

### Katasztrofikus felejtés (Catastrophic Forgetting)
- Egyetlen feladatra történő finomhangoláskor az eredeti képességek romlhatnak.
- Megoldások: multitask fine-tuning, PEFT/LoRA.

### Adat-előkészítés finomhangoláshoz (AWS)
- **SageMaker Canvas**: Alacsony kódú adat-előkészítés
- **Amazon EMR + Apache Spark**: Skálázható adat-előkészítés
- **AWS Glue Interactive Sessions**: Szerverless Spark motor
- **SageMaker Feature Store**: Jellemzők tárolása és felfedezése
- **SageMaker Clarify**: Torzítás detektálás az adatban
- **SageMaker Ground Truth**: Adat-címkézés

---

## 3.4 Alapmodell teljesítmény értékelése

### Optimalizálási technikák
- Modellméret csökkentése → gyorsabb betöltés, de romolhat a teljesítmény
- Tömörebb promptok, rövidebb lekért szövegrészletek
- Inference paraméterek finomhangolása

### Értékelési metrikák

| Metrika | Feladat | Leírás |
|---------|---------|--------|
| **ROUGE** | Összefoglalás | A generált szöveget referenciával hasonlítja össze |
| **BLEU** | Fordítás | Gépi fordítás minőségének mérése emberi referenciával szemben |
| **BERTScore** | Szöveggenerálás | Szemantikai hasonlóság alapú pontszám – hallucináció és hűség értékelésére |

### Benchmark-ok (LLM-ek összehasonlítása)

| Benchmark | Mit mér? |
|-----------|----------|
| **GLUE / SuperGLUE** | Általános nyelvi feladatok (érzelem-elemzés, kérdésmegválaszolás) |
| **MMLU** | Tudás és problémamegoldás (történelem, matematika, jog, informatika stb.) |
| **BIG-bench** | Az aktuális modellek képességein túlmutató feladatok |
| **HELM** | Holisztikus értékelés – átláthatóságot javít, több metrikát kombinál |

### Értékelés AWS-en
- **SageMaker Clarify**: LLM értékelési feladatok (stereotípia, toxicitás, tényszerűség, szemantikai robusztusság, pontosság)
- **Amazon Bedrock Evaluation**: Automatikus modell-összehasonlítás, BERTScore

### Alkalmazásba integrálás – architekturális rétegek
1. **Infrastruktúra réteg**: Számítás, tárolás, hálózat – biztonság!
2. **Modell réteg**: LLM kiválasztása + inference infrastruktúra
3. **Eszközök és keretrendszerek**: Modell-hub, RAG, ágensek
4. **Felhasználói felület**: Weboldal vagy REST API – biztonsági komponensek

---

# DOMAIN 4: Felelős AI irányelvek

## 4.1 Felelős AI rendszerek fejlesztése

### A felelős AI alapdimenziói

| Dimenzió | Jelentés |
|----------|---------|
| **Méltányosság (Fairness)** | Mindenkit egyenlően kezel, függetlenül kortól, nemtől, etnikumtól |
| **Magyarázhatóság (Explainability)** | Emberi nyelven meg lehessen magyarázni, miért hozott a modell egy döntést |
| **Robusztusság** | Hibatűrés – minimalizálja a hibákat |
| **Adatvédelem és biztonság** | PII védelme, személyes adatok nem kerülhetnek ki |
| **Irányítás (Governance)** | Megfelelés ipari szabványoknak, kockázatkezelés, auditálhatóság |
| **Átláthatóság (Transparency)** | Modell képességei, korlátai, kockázatai világosak; a felhasználók tudják, hogy AI-val kommunikálnak |

### Torzítás és variancia

- **Osztály-egyensúlytalanság (Class imbalance)**: Ha egy jellemzőérték kevesebb mintát tartalmaz → a modell rosszabbul teljesít az alulreprezentált csoportokra.
- **Túltanulás**: A modell nem reprezentatív betanító adaton tanult → rosszul teljesít a való világban.
- **Alultanulás**: Bizonyos csoportokhoz nem volt elég betanító adat.
- **Demográfiai eltérés**: Egy csoport aránytalanul nagy arányban kap negatív kimenetet.

### Felelős adathalmazok jellemzői
- Inkluzivitás, diverzitás, kiegyensúlyozottság
- Gondosan válogatott adatforrások
- Adatvédelem és hozzájárulás
- Rendszeres auditálás

### Modellkiválasztási szempontok felelős AI-ban
- **Környezeti hatás**: Számítási erőforrások szénlábnyoma
- **Fenntarthatóság**: Meglévő modellek újrahasználata
- **Átláthatóság**: Képességek és korlátok kommunikálása
- **Elszámoltathatóság**: Egyértelmű felelősségi viszonyok
- **Érintettek bevonása**: Sokféle nézőpont a folyamatba

### Amazon SageMaker Clarify – Torzítás detektálás

**Betanító adaton mért metrikák:**
- Osztály-egyensúlytalanság (pl. 32% nő vs. 68% férfi)
- Címke-egyensúlytalanság (pozitív kimenetek aránya csoportonként)
- Demográfiai eltérés (elutasítások aránya csoportonként)

**Betanított modellen mért metrikák:**
- Pozitív előrejelzések arányának különbsége csoportok között
- Specificitás különbség, Recall különbség, Pontosság különbség
- Kezelési egyenlőség (hamis negatívok vs. hamis pozitívok aránya)

**Magyarázhatóság**: SageMaker Clarify fekete dobozként kezeli a modellt, Shapley-értékek segítségével meghatározza az egyes jellemzők hozzájárulását a döntéshez.

### Generatív AI kockázatai

| Kockázat | Leírás |
|----------|--------|
| **Hallucinációk** | A modell hihetőnek tűnő, de hamis információt generál |
| **Szerzői jogi problémák** | A modell szerzői jog alá eső anyagból tanulhatott; AI-generált tartalom nem szerzői jogi védett |
| **Torzított kimenetek** | Diszkriminatív vagy igazságtalan bánásmód |
| **Toxikus tartalom** | Sértő, zavaró vagy obszcén tartalom generálása |
| **Adatvédelmi kockázat** | Érzékeny adatok kiszivároghatnak a modell kimenetébe |
| **Bizalomvesztés** | Felelőtlen AI gyakorlatok reputációs kárt okozhatnak |

### Guardrails for Amazon Bedrock
- Tartalomszűrési küszöbök (gyűlölet, sértés, szexuális, erőszak)
- Témák tiltása (természetes nyelvi leírással)
- PII detektálás és szerkesztés
- Mind a promptra, mind a modellválaszra alkalmazható

### SageMaker Clarify – LLM értékelési dimenziók
1. **Prompt sztereotipizálás**: Torzítás a válaszokban (rassz, nem, kor stb.)
2. **Toxicitás**: Sértő, agresszív, fenyegető tartalom
3. **Tényszerű tudás**: A válaszok igazságtartalma
4. **Szemantikai robusztusság**: Ellenálló-e elírásoknak, formázási változtatásoknak
5. **Pontosság**: Helyes osztályozás, összefoglalás stb.

---

## 4.2 Átlátható és magyarázható modellek

### Átláthatóság két mértéke

| Mérték | Leírás | Példa modell |
|--------|--------|-------------|
| **Értelmezhetőség (Interpretability)** | A modell belső működése megérthető | Lineáris regresszió, döntési fa |
| **Magyarázhatóság (Explainability)** | A bemenet-kimenet megfigyeléséből levonható következtetés | Bármely modell (fekete doboz megközelítés) |

### Kompromisszumok
- **Teljesítmény vs. átláthatóság**: Egyszerűbb modell = átláthatóbb, de gyengébb teljesítmény.
- **Biztonság vs. átláthatóság**: Az átlátható modellek könnyebben támadhatók (visszafejthetők). Opáquabb modellek → nehezebb a hackerek dolga.
- **Adatvédelem vs. átláthatóság**: A betanító adatokról szóló részletek megosztása adatvédelmi kockázatot jelent.

### Nyílt forráskód előnyei és hátrányai
- **Előnyök**: Maximális átláthatóság, közösségi ellenőrzés, sokszínűbb fejlesztők, kisebb torzítás
- **Hátrányok**: Biztonsági aggályok – egyes cégek tiltják az open source AI használatát

### AWS eszközök az átláthatósághoz

| Eszköz | Funkció |
|--------|---------|
| **AI Service Cards** | Felelős AI dokumentáció az AWS AI szolgáltatásokhoz (felhasználási esetek, korlátok, tervezési döntések) |
| **SageMaker Model Cards** | A modell életciklusának dokumentálása (tervezés, építés, betanítás, értékelés) |
| **SageMaker Clarify** | Jellemző-hozzájárulás (Shapley-értékek), parciális függőségi grafikonok |

### Emberközpontú AI (Human-Centered AI)
- Interdiszciplináris együttműködés (pszichológusok, etikusok, domaini szakértők)
- A felhasználó bevonása a fejlesztési folyamatba
- Cél: az emberi képességek erősítése, nem kiváltása

### Amazon Augmented AI (Amazon A2I)
- Emberi felülvizsgálat beépítése az AI inferenciákba
- Alacsony konfidenciájú előrejelzéseket emberi felülvizsgálóknak küldi
- Véletlenszerű előrejelzések auditálása
- Visszajelzés → modell újratanítás

### RLHF (Reinforcement Learning from Human Feedback)
- Iparági szabvány az LLM-ek „igazítására" (truthful, harmless, helpful)
- Külön jutalommodellt (reward model) tanítanak emberi preferenciák alapján
- Az LLM a jutalommodell alapján finomítja válaszait
- SageMaker Ground Truth → emberi preferenciák gyűjtése

---

# DOMAIN 5: Biztonság, megfelelőség és irányítás AI megoldásokhoz

## 5.1 AI rendszerek védelme

### AWS Shared Responsibility Model (Megosztott felelősségi modell)
- **AWS felelőssége (Security OF the cloud)**: Fizikai adatközpontok, hálózat, hardver, infrastruktúra
- **Ügyfél felelőssége (Security IN the cloud)**: Szolgáltatások konfigurálása, hozzáférés-kezelés, titkosítás, adatvédelem
- A felelősség mértéke függ a szolgáltatástól: EC2 (több felelősség) vs. SageMaker Serverless (kevesebb)

### AWS Identity and Access Management (IAM)

| Fogalom | Leírás |
|---------|--------|
| **Root felhasználó** | Teljes hozzáférés – NE használd napi feladatokra; erős jelszó + MFA |
| **IAM felhasználó** | Egyéni identitás – alapból nincs jogosultsága, explicit hozzárendelés szükséges |
| **IAM csoport** | Felhasználók gyűjteménye – csoportszintű jogosultságok (pl. fejlesztők, QA, admin) |
| **IAM szerep (Role)** | Ideiglenes hozzáférés – személyek vagy szolgáltatások vehetik fel; automatikusan lejár |
| **IAM házirend (Policy)** | JSON dokumentum – engedélyezi vagy megtagadja a hozzáférést erőforrásokhoz |
| **Legkisebb jogosultság elve** | Csak a szükséges minimális jogosultságokat adj meg |
| **MFA** | Többfaktoros hitelesítés – mindig engedélyezd, különösen a root-nak |
| **Identitás-alapú vs. erőforrás-alapú házirendek** | Az eredő jogosultság a kettő kombinációja; explicit megtagadás felülírja az engedélyezést |

### AWS IAM Identity Center
- Központi felhasználókezelés több AWS fiókhoz
- Külső identitásszolgáltató (pl. Active Directory) használata
- Szerepalapú, ideiglenes hozzáférés (jobb, mint a tartós kulcsok)
- AWS ajánlása: használd az IAM Identity Center-t az IAM felhasználók helyett

### Naplózás és auditálás
- **AWS CloudTrail**: Minden API hívás naplózása az AWS fiókban – ki, mikor, honnan, mit csinált. SageMaker-rel integrált.

### Adatvédelem

| Terület | Megoldás |
|---------|----------|
| **Nyilvános hozzáférés blokkolása** | Amazon S3 Block Public Access (bucket vagy fiók szinten) |
| **Titkosítás nyugalmi állapotban** | Szerver oldali titkosítás (alapértelmezett: S3, DynamoDB, SageMaker). AWS KMS egyedi kulcsokhoz. |
| **Titkosítás átvitel közben** | TLS/HTTPS minden AWS szolgáltatási végpontnál |
| **SageMaker elosztott betanítás** | Csomópontok közötti forgalom titkosítása opcionálisan engedélyezhető |
| **PII detektálás** | Amazon Macie – S3 bucket-ek folyamatos vizsgálata érzékeny adatokra |

### AWS KMS (Key Management Service)
- Titkosítási kulcsok létrehozása, kezelése az AWS fiókban
- IAM házirendekkel kontrollálható, ki használhatja a kulcsot → extra védelmi réteg
- Ügyfél által kezelt kulcsok (customer-managed keys) → teljes kontroll

### Hálózatbiztonság
- **VPC (Virtual Private Cloud)**: Saját privát hálózat az AWS-en
- **SageMaker + VPC**: Ajánlott saját VPC-t megadni – kontrollálható a forgalom
- **VPC Only mód**: SageMaker nem kap internet-hozzáférést
- **VPC Interface Endpoints (PrivateLink)**: Privát hálózaton keresztüli elérés AWS szolgáltatásokhoz

### SageMaker Role Manager
- Egyszerűsíti az IAM szerepek létrehozását ML tevékenységekhez
- 3 előkonfigurált persona: Data Scientist, MLOps, SageMaker Compute
- 12 elődefiniált ML tevékenység jogosultságkészlettel

### AI rendszerek biztonsági fenyegetései

| Fenyegetés | Leírás | Védekezés |
|-----------|--------|-----------|
| **Adat-mérgezés (Data poisoning)** | Rosszindulatú adatok beszúrása a betanító adatba | Adatminőség monitorozás, hozzáférés korlátozás |
| **Ellenséges bemenetek (Adversarial inputs)** | Finoman manipulált bemenet → téves osztályozás | Adversarial training, bemenet-validálás |
| **Modell-inverzió** | A kimenetekből a betanító adatok kinyerése | Kimenet információtartalmának minimalizálása |
| **Modell lopás** | A modell visszafejtése a kimenetekből | Hozzáférés korlátozása, kevés információ a kimenetben |
| **Prompt injection** | Rosszindulatú utasítások a promptban | Bemenet-szűrés, mintafelismerés, guardrails |

### Védekezési legjobb gyakorlatok
- Legkisebb jogosultság elve + nyilvános hozzáférés blokkolása
- Adatok és artefaktumok titkosítása
- Modell hozzáférésének korlátozása
- Bemenet ellenőrzése és validálása
- Adversarial bemenettel való betanítás
- Gyakori újratanítás új adatokkal
- Validálási adathalmaz elkülönítése
- Monitorozás: SageMaker Model Monitor → adatminőség, modellminőség, drift detekció → CloudWatch riasztások

### Artefaktum-nyomon követés és verziókezelés

| Elem | AWS szolgáltatás |
|------|-----------------|
| **Forráskód** | GitHub, AWS CodeCommit |
| **Adathalmazok** | Amazon S3 (prefixekkel particionálva) |
| **Konténer-képek** | Amazon ECR |
| **Betanítási feladatok** | SageMaker (automatikus egyedi azonosító + metaadatok) |
| **Modellverziók** | SageMaker Model Registry |
| **Jellemzők** | SageMaker Feature Store |
| **Végpontok** | SageMaker (egyedi azonosító + konfiguráció) |
| **Modell-dokumentáció** | SageMaker Model Cards (életciklus dokumentálása) |
| **Lineage** | SageMaker ML Lineage Tracking (teljes munkafolyamat grafikus ábrázolása) |
| **Központi irányítópult** | SageMaker Model Dashboard (összes modell áttekintése, monitorozás, riasztások) |

---

## 5.2 AI rendszerek irányítása és megfelelőségi szabályozás

### AWS megfelelőség a megosztott felelősségi modellben
- **AWS**: A felhő megfelelőségéért felel (adatközpontok, infrastruktúra)
- **Ügyfél**: A felhőben futó munkaterhelések megfelelőségéért felel
- **AWS Artifact**: Harmadik fél által készített megfelelőségi jelentések elérhetővé tétele (SOC 2, ISO 27001 stb.)

### Megfelelőségi szabványok

| Szabvány | Leírás |
|----------|--------|
| **SOC 2** | Biztonság, rendelkezésre állás, integritás, bizalmasság, adatvédelem |
| **ISO 27001** | Nemzetközi biztonsági menedzsment szabvány |
| **ISO 42001 / ISO 23894** | AI rendszerek kockázatkezelése és felelős AI gyakorlatok (2023) |
| **EU AI Act** | Az első átfogó AI szabályozás – 3 kockázati kategória: tiltott, magas kockázat, szabályozatlan |
| **NIST AI RMF** | AI kockázatkezelési keretrendszer – 4 funkció: Govern, Map, Measure, Manage |
| **Algorithmic Accountability Act** | (US, javasolt) – AI rendszerek hatásértékelése, átláthatóság |
| **GDPR** | EU adatvédelmi rendelet – gyakran globális mércévé válik |

### EU AI Act kockázati kategóriák
1. **Elfogadhatatlan kockázat** → TILTOTT (social scoring, arcfelismerő adatbázisok scrapeléssel, érzelemfelismerés munkahelyen/iskolában)
2. **Magas kockázat** → Jogi követelmények (kockázatkezelés, adatirányítás, dokumentálás)
3. **Egyéb** → Nagyrészt szabályozatlan

### Kockázatbecslés
- **Kockázat = Valószínűség × Következmény súlyossága**
- Azonosítsd a felhasználási esetet és érintetteket → káros események azonosítása → kockázatmátrix
- **Inherens kockázat** → biztonsági kontrollokkal csökkenthető → **Reziduális kockázat** (ami marad)
- Az összesített kockázati besorolás a legmagasabb reziduális kockázatokra fókuszál

### AWS szolgáltatások a megfelelőséghez

| Szolgáltatás | Funkció |
|-------------|---------|
| **AWS Audit Manager** | Megfelelőségi követelmények összekapcsolása AWS használati adatokkal; automatikus bizonyítékgyűjtés és jelentéskészítés. Beépített keretrendszerek (Gen AI best practices, SOC 2). |
| **Guardrails for Amazon Bedrock** | Tartalomszűrés, témablokkolás, PII kezelés – alkalmazásszintű biztonsági korlátok |
| **AWS Config** | Erőforrás-konfigurációk folyamatos monitorozása; szabályellenőrzés; automatikus javítás. Conformance pack-ek: „AI és ML operatív best practices", „SageMaker biztonsági best practices" |
| **Amazon Inspector** | Alkalmazásszintű biztonsági vizsgálat – sérülékenységek, nyitott hozzáférések |
| **AWS Trusted Advisor** | Költségoptimalizálás, teljesítmény, biztonság, ellenálló képesség, működési kiválóság ellenőrzése |

### Adatirányítás (Data Governance)

**Három fő pillér:**
1. **Kurálás**: Legértékesebb adatforrások azonosítása, kezelése, minőségbiztosítás
2. **Felfedezés és megértés**: Központi adatkatalógus, kontextusban való értelmezés
3. **Védelem**: Adatvédelem, biztonság, hozzáférés-szabályozás egyensúlya

**Szerepek:**
- **Adat tulajdonos (Data owner)**: Vezetői szintű – adatpolitikai döntések, szabályozási megfelelés
- **Adat gondnok (Data steward)**: Üzleti oldal – részletes adatismeret, napi feladatok
- **IT**: Eszközök és rendszerek kezelése

**AWS szolgáltatások adatirányításhoz:**

| Szolgáltatás | Funkció |
|-------------|---------|
| **AWS Glue Data Catalog** | Metaadat-katalógus (helyszín, séma) – automatikus felfedezés crawler-ekkel |
| **AWS Glue DataBrew** | Adatprofilozás (forma, tartalom, struktúra, kapcsolatok); adatminőségi szabályok; adatszármazás (data lineage) vizuálisan |
| **AWS Glue Data Quality** | Adatminőségi szabályok definiálása és futtatása a Data Catalog objektumaira |
| **AWS Lake Formation** | Finomhangolt hozzáférés-szabályozás adattóhoz (oszlop, sor, cella szint); központi adattó kezelés |

### Amazon S3 tárolási osztályok és életciklus-kezelés

| Osztály | Használat | Költség |
|---------|----------|--------|
| **S3 Standard** | Gyakran használt adatok | Normál |
| **S3 Standard-IA** | Ritkábban használt, de gyors elérés | Alacsonyabb tárolás, magasabb lekérés |
| **S3 One Zone-IA** | Mint Standard-IA, de 1 AZ-ben | Még olcsóbb |
| **S3 Intelligent-Tiering** | Ismeretlen hozzáférési minta – automatikus költségoptimalizálás | Változó |
| **S3 Glacier / Deep Archive** | Archiválás, hosszú távú megőrzés megfelelőségi célokra | Legolcsóbb tárolás |

- **Életciklus-szabályok**: Automatikus áthelyezés olcsóbb osztályokba → törlés, ha már nem szükséges.

### AI irányítási stratégia lépései
1. **Hatókör meghatározása** (Generative AI Security Scoping Matrix: Scope 1-5)
   - Scope 1-2: Harmadik fél alkalmazás fogyasztása → legkevesebb felelősség
   - Scope 3-5: Saját AI megoldás építése → teljes felelősség (adatosztályozás, fenyegetésmodellezés, biztonsági kontrollok)
2. **AI irányítási politikák dokumentálása** és alkalmazottak képzése
3. **Monitoring mechanizmusok** definiálása (teljesítmény, megfelelőség, torzítás)
4. **Rendszeres felülvizsgálat** és politikák módosítása

> **Fő tanács**: Keress megoldást balról jobbra: először AWS AI szolgáltatások (Comprehend, Translate) → aztán Bedrock (FM + RAG) → aztán SageMaker JumpStart (fine-tuning) → végső esetben: saját modell nulláról. Minél balrább, annál kevesebb a felelősséged.

---

# KIEGÉSZÍTŐ ANYAG: Mi az a mesterséges intelligencia? (What Is AI)

## AI történelmi mérföldkövek

| Időszak | Esemény |
|---------|---------|
| 1943 | McCulloch & Pitts – mesterséges neuronok modellje |
| 1950 | Alan Turing – „Computing Machinery and Intelligence", Turing-teszt |
| 1951-1969 | SNARC (első neurális háló gép), Perceptron, ELIZA chatbot |
| 1969-1979 | Minsky a neurális hálók korlátait mutatta be → 1. „AI tél" |
| 1980-as évek | Szakértői rendszerek (pl. MYCIN), mélytanulási technikák újjáéledése |
| 1987-1997 | 2. „AI tél" (dot-com boom hatása) |
| 1997 | IBM Deep Blue legyőzi Kasparovot |
| 2007-2018 | Felhőszámítás → AlexNet, AlphaZero, mélytanulás felfutása |
| 2022 | ChatGPT széles körben ismertté válik |

## AI alkalmazási területek összefoglalása

- **Chatbotok és virtuális asszisztensek**: Kontextus-tudatos, ember-szerű beszélgetések
- **Intelligens dokumentumfeldolgozás (IDP)**: Strukturálatlan adatok (email, PDF, kép) → strukturált adatok
- **Alkalmazás teljesítmény-monitorozás (APM)**: Proaktív problémamegoldás ML alapon
- **Képgenerálás, szöveggenerálás, beszédgenerálás**: Valós idejű tartalom-előállítás
- **Multimodális AI**: Szöveg + kép + hang egyidejű feldolgozása

## AI technológiai képességek

| Képesség | Leírás |
|----------|--------|
| **Képgenerálás** | Szöveges leírásból valósághű képeket állít elő másodpercek alatt (marketing, szórakoztatás, design) |
| **Szöveggenerálás** | Emberszerű szöveg automatikus előállítása (e-mailek, jelentések, ügyfélszolgálat, marketing) |
| **Beszédgenerálás és -felismerés** | Természetes emberi beszéd létrehozása + beszélt szavak értelmezése (virtuális asszisztensek, akadálymentesítés) |
| **Multimodális AI** | Szöveg, kép és hang egyidejű integrálása és értelmezése → fejlett valós idejű elemzés (videóelemzés, önvezető járművek) |

## AI iparági transzformáció

| Iparág | AI alkalmazás |
|--------|--------------|
| **Tartalomajánlás** | Streamingszolgáltatások (Netflix, Spotify) személyre szabott ajánlásai felhasználói preferenciák alapján |
| **Személyre szabott vásárlás** | E-kereskedelmi platformok böngészési előzmények alapján adnak termékajánlásokat |
| **Egészségügy** | Fejlett diagnosztika, kezelési tervek, betegmonitorozás – orvosi képelemzés korai betegségfelismerésre |
| **Forgalomirányítás** | Valós idejű adatelemzés, forgalmi minták előrejelzése, alternatív útvonalak → csökkentett torlódás és kibocsátás |
| **Természetvédelem** | Vadon élő állatok monitorozása, erdőirtás elleni küzdelem, orvvadászat megelőzése AI-vezérelt drónokkal és műholdképekkel |

## AI üzleti előnyök

| Előny | Leírás |
|-------|--------|
| **Intelligens automatizálás** | Számlák, dokumentumok automatikus beolvasása, osztályozása, hibadetektálás – minimális emberi beavatkozással |
| **Termelékenység növelése** | Kritikus információk azonnali, kontextusban történő elérése (pl. betegnyilvántartás, járatadatok keresése) |
| **Komplex problémák megoldása** | Hatalmas adathalmazok elemzése mintafelismeréshez (prediktív karbantartás, gyógyszerkutatás) |
| **Új ügyfélélmények** | Személyre szabott, valós idejű ajánlások és megoldások ügyfélprofil-adatok alapján (pl. egyedi utazási tervek) |

## AI implementáció kihívásai

| Kihívás | Leírás |
|---------|--------|
| **AI irányítás (governance)** | Adatirányítási politikák betartása, szabályozási előírások és adatvédelmi törvények – a szervezet felelős az ügyféladatokért |
| **Technikai nehézségek** | Hatalmas számítási erőforrás-igény a mélytanuláshoz; robusztus infrastruktúra szükséges; a skálázás költséges lehet |
| **Adatkorlátok** | Elfogulatlan AI betanításához hatalmas mennyiségű, jó minőségű adatra van szükség; elegendő tárolókapacitás és adatminőség-kezelés elengedhetetlen |

## AI alkalmazási architektura – 3 réteg
1. **Adatréteg**: Adatok előkészítése az AI alkalmazásokhoz
2. **Modellréteg**: Alapmodellek (FM), LLM-ek, ML modellek – testreszabás belső adatokkal
3. **Alkalmazásréteg**: Felhasználó-felület, interakció az AI rendszerrel

## Felelős AI (Responsible AI)
- Méltányosság, átláthatóság, elszámoltathatóság
- Társadalmi és környezeti hatás figyelembe vétele
- AWS eszközök: Guardrails for Amazon Bedrock, SageMaker Clarify

---

# KIEGÉSZÍTŐ ANYAG: AWS Cloud Adoption Framework for AI (CAF-AI)

## CAF-AI célja
- Mentális modell és útmutató az AI/ML/generatív AI bevezetéséhez szervezetekben
- A szervezeti képességek érlelésének strukturálása az AI területén
- Kiindulópont a közép- és hosszú távú AI stratégiához

## AI taxonómia (hierarchia)
```
Mesterséges Intelligencia (AI)
  └── Gépi Tanulás (ML)
       └── Mélytanulás (Deep Learning)
            └── Generatív AI
```

## Kulcsgondolatok
- Az AI nem egyetlen technológia, hanem egymásra épülő részdiszciplínák összessége
- A generatív AI a mélytanulás legújabb képessége – új, potenciálisan eredeti tartalmakat hoz létre
- A felhőszámítás (cloud computing) tette lehetővé az AI széles körű alkalmazását (számítási kapacitás, adathozzáférés)
- A CAF-AI az AWS Cloud Adoption Framework (AWS CAF) AI-specifikus kibővítése

## Szervezeti érettségi szintek
- A keretrendszer leírja, hogyan fejlődnek a szervezeti képességek az AI bevezetése során
- Lépésről lépésre útmutatást ad a célállapot eléréséhez
- Üzleti értékteremtés az út minden szakaszában

## Kapcsolódó keretrendszerek
- **AWS Well-Architected Framework**: 6 pillér (megbízhatóság, biztonság, hatékonyság, költséghatékonyság, fenntarthatóság, működési kiválóság)
- **Machine Learning Lens**: ML munkaterhelések tervezése, telepítése, architektúrája a felhőben
- **AWS Architecture Center**: Referencia architektúrák és legjobb gyakorlatok

---

# AWS SZOLGÁLTATÁSOK ÖSSZESÍTŐ TÁBLÁZAT

| Szolgáltatás | Cél | Legfontosabb tudnivaló |
|-------------|-----|----------------------|
| **Amazon S3** | Objektumtárolás | Elsődleges forrás ML betanító adatokhoz – bármilyen adattípus, korlátlan kapacitás, alacsony költség. Alapértelmezett titkosítás. Életciklus-szabályokkal automatikus költségoptimalizálás. |
| **Amazon Bedrock** | Menedzselt generatív AI platform | Több FM-hez hozzáférés API-n (Amazon Titan, Cohere, Stability AI stb.); fine-tuning; RAG (Knowledge Bases); Guardrails; Agents; modellértékelés. Fizess amit használsz, nincs előzetes elköteleződés. |
| **Amazon SageMaker** | Teljes ML életciklus platform | Egyedi ML modellek építése, betanítása, telepítése. Alszolgáltatások: Training Jobs, Experiments, AMT, Pipelines, Model Monitor, Model Registry, Feature Store, Canvas, Ground Truth, Clarify, JumpStart, Model Cards, ML Lineage Tracking, Model Dashboard, Role Manager. |
| **SageMaker JumpStart** | Modell-hub előre betanított modellekkel | FM-ek és feladat-specifikus modellek választéka; fine-tuning transfer learning-gel; gyors telepítés. GPU szükséges. |
| **SageMaker Ground Truth** | Adat-címkézés | Gépi + emberi munkaerő (Amazon Mechanical Turk, vagy privát); aktív tanulás automatikus címkézéssel. RLHF preferencia-gyűjtésre is használható. |
| **SageMaker Clarify** | Torzítás és magyarázhatóság | Torzítás detektálás az adatban és a modellben; jellemző-fontosság (Shapley-értékek); LLM értékelés (stereotípia, toxicitás, tényszerűség, robusztusság, pontosság). |
| **SageMaker Canvas** | Vizuális ML és adat-előkészítés | 300+ beépített transzformáció, kód nélkül; Data Wrangler integráció. |
| **SageMaker Feature Store** | Jellemzők központi tárolása | Jellemzők megosztása, újrafelhasználása, felfedezése; point-in-time lekérdezések; lineage nyomon követés. |
| **SageMaker Model Monitor** | Modell monitorozás termelésben | Adatminőség és modellminőség összehasonlítása baseline-nal; drift és anomália detekció; CloudWatch riasztások. |
| **SageMaker Pipelines** | ML pipeline automatizálás | Reprodukálható ML munkafolyamatok; telepítés, monitorozás, lineage tracking. |
| **SageMaker Model Registry** | Modell-katalógus | Modellverziók kezelése; státusz (pending, approved, rejected); telepítés közvetlenül a registry-ből. |
| **SageMaker Model Cards** | Modell-dokumentáció | Életciklus dokumentálása; automatikus részletek kitöltése; PDF exportálás. |
| **SageMaker ML Lineage Tracking** | Munkafolyamat-nyomon követés | Teljes ML munkafolyamat grafikus ábrázolása; lekérdezések az artefaktumok kapcsolatairól. |
| **SageMaker Model Dashboard** | Központi irányítópult | Összes modell áttekintése; monitorozási eredmények; küszöbérték-megsértések azonosítása. |
| **SageMaker Role Manager** | IAM szerepek egyszerűsítése ML-hez | 3 persona (Data Scientist, MLOps, SageMaker Compute); 12 elődefiniált ML tevékenység. |
| **Amazon Rekognition** | Számítógépes látás | Arcfelismerés, objektumdetekció, tartalommoderáció, egyéni címkék – képek és videók (streaming is). |
| **Amazon Textract** | Dokumentum-feldolgozás | Szöveg, kézírás, űrlapok, táblázatok kinyerése szkennelt dokumentumokból. Több mint egyszerű OCR. |
| **Amazon Comprehend** | Természetes nyelvfeldolgozás (NLP) | Érzelem-elemzés, PII detektálás, entitás-felismerés, egyéni osztályozók. |
| **Amazon Lex** | Chatbot-építés | Alexa technológia; hang és szöveges interfészek; IVR rendszerek. |
| **Amazon Transcribe** | Beszéd → szöveg | 100+ nyelv; élő és rögzített hang/videó; valós idejű feliratozás. |
| **Amazon Polly** | Szöveg → beszéd | Természetes hangzás, több tucat nyelv; IVR rendszerek, akadálymentesítés. |
| **Amazon Translate** | Gépi fordítás | 75 nyelv; neurális hálózat alapú; teljes kontextus figyelembevétele. |
| **Amazon Kendra** | Intelligens vállalati keresés | NLP alapú kérdésmegértés; vállalati rendszerekben való keresés. |
| **Amazon Personalize** | Személyre szabott ajánlások | Termékajánlások, ügyfélszegmentáció, marketing kampányok. |
| **Amazon Fraud Detector** | Csalás detektálás | Előre betanított modellek online tranzakciókhoz, hamis fiókokhoz, fióká tvételekhez. |
| **Amazon Q Developer** | AI kódolási asszisztens | Valós idejű kódjavaslatk; kódrészletektől teljes funkciókig; kódfordítás nyelvek között. |
| **Amazon Titan** | Amazon saját alapmodellje | Szöveggenerálás (Express, Lite), képgenerálás; Amazon Bedrock-on elérhető. |
| **Amazon Augmented AI (A2I)** | Emberi felülvizsgálat beépítése | Alacsony konfidenciájú inferenciák emberi ellenőrzése; Mechanical Turk vagy privát munkaerő. |
| **AWS Glue** | ETL szolgáltatás | Adatfeltárás, transzformáció, betöltés; Data Catalog; crawler-ek; beépített transzformációk. |
| **AWS Glue DataBrew** | Vizuális adat-előkészítés | 250+ transzformáció kód nélkül; adatprofilozás; adatminőségi szabályok; data lineage. |
| **AWS Glue Data Catalog** | Metaadat-katalógus | Séma, helyszín, futásidejű metrikák; kereshető és lekérdezhető; crawler-ek automatikus feltöltése. |
| **AWS Glue Data Quality** | Adatminőség-ellenőrzés | Szabályok definiálása, ML alapú anomália-detekció, eredmények a konzolban. |
| **Amazon OpenSearch Service** | Keresés és vektortárolás | Szemantikus keresés, RAG, ajánlórendszerek; vektor-adatbázis képesség; Serverless opció. |
| **Amazon Macie** | Érzékeny adat detektálás | S3 bucket-ek automatikus vizsgálata PII-re; ML + minta-illesztés; riasztások. |
| **AWS KMS** | Titkosítási kulcsok kezelése | Kulcsok létrehozása, kezelése; IAM házirendekkel kontrollálható; extra védelmi réteg az adatokhoz. |
| **AWS CloudTrail** | API hívások naplózása | Auditálás és compliance; SageMaker-rel integrált; ki, mikor, mit csinált. |
| **AWS IAM** | Hozzáférés-kezelés | Felhasználók, csoportok, szerepek, házirendek; legkisebb jogosultság elve; MFA. |
| **AWS IAM Identity Center** | Központi identitáskezelés | Több fiókhoz; külső IdP támogatás; szerepalapú ideiglenes hozzáférés. |
| **AWS Config** | Erőforrás-konfiguráció monitorozás | Konfigurációváltozások rögzítése; szabályellenőrzés; automatikus javítás; conformance pack-ek. |
| **AWS Audit Manager** | Megfelelőségi auditálás | Automatikus bizonyítékgyűjtés; keretrendszer-alapú értékelések (Gen AI, SOC 2); audit-jelentések. |
| **AWS Artifact** | Megfelelőségi jelentések | Harmadik fél auditori jelentések (SOC, ISO stb.) elérhetővé tétele az ügyfelek számára. |
| **Amazon Inspector** | Alkalmazás-biztonsági vizsgálat | Sérülékenységek és biztonsági eltérések detektálása; prioritizált lista javítási javaslatokkal. |
| **AWS Trusted Advisor** | Best practice ellenőrzések | Költség, teljesítmény, biztonság, ellenálló képesség, működési kiválóság, szolgáltatáskorlátok. |
| **AWS Lake Formation** | Adattó hozzáférés-kezelés | Oszlop/sor/cella szintű jogosultságok; központi adattó; Glue Data Catalog integrálva. |
| **AWS Step Functions** | Szerverless workflow-kezelés | Vizuális drag-and-drop; AWS szolgáltatások és egyéni logika integrálása. |
| **Amazon MWAA** | Apache Airflow menedzselt szolgáltatás | Nyílt forráskódú workflow-menedzsment; Python alapú; skálázható. |
| **Amazon CloudWatch** | Monitorozás és riasztások | Metrikák, naplók, riasztások; SageMaker Model Monitor eredmények fogadása. |
| **Amazon ECR** | Konténer-képek tárolása | Docker konténer image-ek; SageMaker algoritmusok és egyéni konténerek tárolása. |
| **AWS DeepRacer** | Megerősítéses tanulás oktatása | Modell versenyautó; a fejlesztők RL modelleket tanítanak pályán való navigálásra. |
| **PartyRock** | Generatív AI playground | Amazon Bedrock-ra épül; ingyenes; prompt engineering tanulása interaktívan. |
| **Amazon Mechanical Turk** | Crowdsourcing munkaerő | 500,000+ független közreműködő; adatcímkézés; RLHF preferencia-gyűjtés. |
| **AI Service Cards** | Felelős AI dokumentáció | AWS AI szolgáltatások felhasználási esetei, korlátai, tervezési döntései egy helyen. |
