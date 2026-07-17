# 🐧 PengIA - Telegram AI Assistant & RAG Engine

https://github.com/user-attachments/assets/671baf6b-06a9-4f9a-848f-a5590d7548ae


PengIA è un assistente virtuale avanzato integrato su Telegram, progettato per gestire sia conversazioni generaliste che interrogazioni specifiche su documenti aziendali (Knowledge Base NSE). L'intera architettura è orchestrata tramite **n8n** e sfrutta un approccio ibrido: AI cloud-based per il ragionamento elastico e AI locale per la vettorializzazione sicura dei dati.

---

## 🎯 Architettura e Funzionalità Core

Il flusso di lavoro non si limita a interrogare un LLM, ma ottimizza le risorse e i tempi di risposta attraverso diverse fasi logiche:

### 1. Routing Intelligente
Il sistema riconosce automaticamente il contesto della richiesta. Utilizzando il comando dedicato `/nse`, il flusso viene instradato verso un agente specializzato nella documentazione aziendale.

### 2. Semantic Caching (A Costo Zero)
Per abbattere i costi delle API e azzerare la latenza, PengIA interroga **Qdrant** prima di generare una nuova risposta. Se una domanda semanticamente identica (con un livello di confidenza >= 0.85) è già stata posta, il bot restituisce la risposta direttamente dalla cache.

### 3. Retrieval-Augmented Generation (RAG)
I documenti aziendali (PDF, TXT, DOCX) vengono ingeriti tramite un'interfaccia web dedicata, vettorializzati localmente tramite Ollama (`nomic-embed-text`) e salvati su Qdrant. L'LLM analizza i frammenti estratti per generare risposte precise e contestualizzate sull'ecosistema NSE.

### 4. Gestione UX Asincrona
Per garantire un'ottima esperienza utente su Telegram, il bot invia un messaggio di stato ("Sto analizzando la tua richiesta... ⏳") che viene dinamicamente eliminato tramite API non appena la risposta elaborata è pronta per la consegna.

---

## 🛠️ Stack Tecnologico

L'ecosistema è containerizzato e suddiviso tra servizi locali e in cloud:

* **Orchestrazione:** [n8n](https://n8n.io/)
* **Vector Database:** [Qdrant](https://qdrant.tech/)
* **Cloud LLM:** Google Gemini 3.1 Flash Lite (Scelto per l'ampia context window e la velocità)
* **Local Embeddings:** Ollama (`nomic-embed-text`)
* **Front-end Ingestion:** HTML5 / CSS3 / JavaScript (Form Multipart per l'invio batch)
* **Infrastruttura:** Docker & Docker Compose

---

## 🚀 Installazione e Setup

Se desideri replicare l'ambiente di sviluppo in locale:

1. **Clona la repository:**
   ```bash
   git clone [https://github.com/MatteoCoding06/PengIA.git](https://github.com/MatteoCoding06/PengIA.git)
   cd PengIA
