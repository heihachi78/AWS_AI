# AWS AI Practitioner (AIF-C01) – Magyar nyelvű tananyag

## Célja

Ez a tananyag az **AWS Certified AI Practitioner (AIF-C01)** vizsgára való felkészülést segíti. Magyar nyelven foglalja össze a vizsga teljes tudásanyagát: az alapfogalmaktól kezdve a generatív AI-n és az alapmodelleken át a felelős AI gyakorlatokig és a biztonsági kérdésekig. A dokumentum célja, hogy egyetlen, áttekinthető anyagban nyújtson minden szükséges ismeretet a sikeres vizsgához.

## Felépítés

A tananyag az AWS hivatalos vizsgatematikáját követi, 5 fő fejezetre (domain-re), 2 kiegészítő anyagra és egy szolgáltatás-összesítőre tagolódik.

### Domain 1 – A mesterséges intelligencia és a gépi tanulás alapjai

- AI, ML, mélytanulás és generatív AI definíciói, hierarchiája
- Adattípusok (strukturált, félig strukturált, strukturálatlan, idősoros)
- Modell-betanítás alapfogalmai (algoritmus, jellemzők, súlyok, inference)
- Tanulási stílusok (felügyelt, felügyelet nélküli, megerősítéses)
- Túltanulás, alultanulás, torzítás
- Neurális hálózatok és mélytanulás
- AI gyakorlati felhasználási esetek és AWS előre betanított szolgáltatások (Rekognition, Textract, Comprehend, Lex, Transcribe, Polly, Kendra, Personalize, Bedrock, SageMaker stb.)
- ML fejlesztési életciklus (adat-előkészítés, betanítás, telepítés, monitorozás, MLOps)
- Értékelési metrikák (Accuracy, Precision, Recall, F1, AUC, MSE, RMSE, MAE)

### Domain 2 – A generatív AI alapjai

- Transformer architektúra, tokenizálás, embedding, kontextusablak
- Zero-shot, one-shot, few-shot következtetés
- Unimodális vs. multimodális modellek
- Diffúziós modellek (Stable Diffusion)
- Generatív AI képességei, korlátai és kockázatai (hallucinációk, toxikus tartalom)
- LLM értékelési metrikák (ROUGE, BLEU)
- AWS infrastruktúra generatív AI-hoz (ML Stack 3 rétege, Bedrock, SageMaker JumpStart, Titan, PartyRock)
- Árazási modellek és biztonsági szempontok

### Domain 3 – Alapmodellek alkalmazása

- Modellkiválasztási kritériumok (költség, latencia, modalitás, méret, testreszabhatóság)
- Inference paraméterek (temperature, top K, top P)
- RAG (Retrieval Augmented Generation) és vektor-adatbázisok
- Ágensek (Agents for Amazon Bedrock)
- Prompt engineering technikák (chain-of-thought, prompt tuning, sablonok)
- Prompt engineering kockázatai (injection, jailbreaking, hijacking, poisoning)
- Guardrails for Amazon Bedrock
- Finomhangolási módszerek (teljes, PEFT, LoRA, ReFT, RLHF, domain adaptation)
- Teljesítményértékelés és benchmark-ok (GLUE, MMLU, BIG-bench, HELM)

### Domain 4 – Felelős AI irányelvek

- A felelős AI alapdimenziói (méltányosság, magyarázhatóság, robusztusság, adatvédelem, irányítás, átláthatóság)
- Torzítás detektálás (SageMaker Clarify, Shapley-értékek)
- Generatív AI kockázatai (hallucinációk, szerzői jog, toxikus tartalom, adatvédelem)
- Átlátható és magyarázható modellek, kompromisszumok
- AWS eszközök (AI Service Cards, SageMaker Model Cards, Amazon A2I)
- RLHF (Reinforcement Learning from Human Feedback)
- Emberközpontú AI megközelítés

### Domain 5 – Biztonság, megfelelőség és irányítás

- AWS Shared Responsibility Model
- IAM (felhasználók, csoportok, szerepek, házirendek, legkisebb jogosultság elve, MFA)
- Adatvédelem (titkosítás nyugalmi állapotban és átvitel közben, AWS KMS, Amazon Macie)
- Hálózatbiztonság (VPC, PrivateLink)
- AI biztonsági fenyegetések (adat-mérgezés, adversarial inputs, modell-inverzió, prompt injection)
- Artefaktum-nyomon követés és verziókezelés
- Megfelelőségi szabványok (SOC 2, ISO 27001, ISO 42001, EU AI Act, NIST AI RMF, GDPR)
- AWS megfelelőségi szolgáltatások (Audit Manager, Config, Inspector, Trusted Advisor, Artifact)
- Adatirányítás (AWS Glue Data Catalog, Lake Formation, Data Quality)
- S3 tárolási osztályok és életciklus-kezelés
- AI irányítási stratégia (Generative AI Security Scoping Matrix)

### Kiegészítő anyagok

- **Mi az a mesterséges intelligencia?** – AI történelmi mérföldkövek (1943–2022), alkalmazási területek, technológiai képességek, iparági transzformáció, üzleti előnyök, implementációs kihívások, alkalmazási architektura, felelős AI
- **AWS Cloud Adoption Framework for AI (CAF-AI)** – AI taxonómia, szervezeti érettségi szintek, kapcsolódó keretrendszerek (Well-Architected Framework, ML Lens)

### AWS szolgáltatások összesítő táblázat

Egy helyen áttekinthető referencia az összes érintett AWS szolgáltatásról, céljáról és legfontosabb jellemzőiről.

## Fájlok

| Fájl | Tartalom |
|------|----------|
| `AWS_AI_Practitioner_Tananyag.md` | A teljes tananyag |
