# Admin-RAG: Lokalny asystent wspierający administrację systemami i sieciami

Projekt zrealizowany w ramach przedmiotu Sztuczna Inteligencja. 
Jest to system RAG (Retrieval-Augmented Generation) bazujący na lokalnym modelu LLM (Ollama), zaprojektowany jako narzędzie wsparcia dla inżynierów i administratorów sieci. 

## Wykorzystane technologie
* **LLM:** Llama 3.2 (uruchamiana lokalnie przez serwer Ollama - gwarancja prywatności danych)
* **Wektoryzacja:** `sentence-transformers` (paraphrase-multilingual-mpnet-base-v2)
* **Baza Wektorowa:** FAISS (Facebook AI Similarity Search)
* **Język:** Python (Jupyter Notebook / Google Colab)

##  Baza wiedzy (Knowledge Base)
Model nie korzysta z wiedzy ogólnej (został poinstruowany, aby nie halucynować), lecz opiera swoje odpowiedzi wyłącznie na dokumentacji technicznej umieszczonej w katalogu `/knowledge`:
1. Procedury routingu i switchingu (Cisco).
2. Administracja systemami Linux (Arch/Debian).
3. Zarządzanie kontenerami (Docker) i kopiami zapasowymi baz danych.

##  Jak uruchomić projekt?

### Opcja A: Środowisko lokalne (JupyterLab / Anaconda)
1. Sklonuj repozytorium na swój komputer.
2. Upewnij się, że masz zainstalowane i uruchomione narzędzie **Ollama** (https://ollama.com/) oraz pobrany model poleceniem w terminalu: `ollama pull llama3.2`.
3. Zainstaluj wymagane biblioteki: `pip install ollama pymupdf sentence-transformers faiss-cpu`
4. Uruchom plik `Admin_RAG_Project.ipynb`. System automatycznie zaciągnie pliki tekstowe z folderu `knowledge/`.

### Opcja B: Google Colab (Zalecane)
Ze względu na to, że kod instaluje serwer Ollama w tle, można go łatwo uruchomić w chmurze:
1. Otwórz plik `Admin_RAG_Project.ipynb` w środowisku Google Colab.
2. W panelu plików po lewej stronie utwórz folder o nazwie `knowledge`.
3. Prześlij pliki `.txt` (lub `.pdf`) z repozytorium do nowo utworzonego folderu `knowledge`.
4. Uruchom po kolei komórki w notatniku. Pierwsza z nich automatycznie zainstaluje niezbędne pakiety oraz pobierze serwer Ollama do wirtualnej maszyny.

##  Bezpieczeństwo i Restrykcje (Prompt Engineering)
Model posiada narzucony specjalistyczny *System Prompt*, który wymusza rolę eksperta IT i kategorycznie zabrania zmyślania komend. Jeżeli pytanie wykracza poza wgraną dokumentację, system reaguje standardowym komunikatem o braku danych.