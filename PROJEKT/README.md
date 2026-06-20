# Admin-RAG: Lokalny asystent wspierający administrację systemami i sieciami

Projekt zrealizowany w ramach przedmiotu Sztuczna Inteligencja. 
Jest to zaawansowany system RAG (Retrieval-Augmented Generation) bazujący na lokalnym modelu LLM. Został zaprojektowany jako bezpieczne narzędzie wsparcia decyzji dla inżynierów i administratorów IT. Projekt posiada wbudowany interfejs graficzny (Web GUI) pozwalający na interaktywne odpytywanie dokumentacji.

##  Wykorzystane technologie
* **LLM:** Llama 3.2 (uruchamiana całkowicie lokalnie przez serwer Ollama - gwarancja prywatności danych infrastrukturalnych)
* **Interfejs Graficzny:** Gradio (tworzenie publicznego tunelu webowego)
* **Wektoryzacja:** `sentence-transformers` (model: paraphrase-multilingual-mpnet-base-v2)
* **Baza Wektorowa:** FAISS (Facebook AI Similarity Search)
* **Język i Środowisko:** Python / Jupyter Notebook (Google Colab)

##  Baza wiedzy (Knowledge Base)
Model jest odizolowany od ogólnej wiedzy internetowej (posiada rygorystyczny *System Prompt* zapobiegający halucynacjom). Opiera swoje odpowiedzi wyłącznie na autorskiej dokumentacji technicznej umieszczonej w katalogu `/knowledge/`, która obejmuje:
1. Procedury routingu i switchingu (Cisco OSPF, Port Security, VLAN).
2. Administracja systemami Linux (Arch/Debian, pacman, systemd, UFW).
3. Zarządzanie kontenerami (Docker) i kopiami zapasowymi baz danych (PostgreSQL).
4. Orkiestracja Kubernetes (K8s diagnostyka, skalowanie, port-forwarding).
5. Automatyzacja infrastruktury (Ansible).
6. Sieci VPN i kryptografia (WireGuard).
7. Systemy monitoringu (Prometheus, Grafana, PromQL).
8. Windows Server i Active Directory (PowerShell, GPO).

##  Jak uruchomić projekt?

### Opcja A: Środowisko Google Colab (Zalecane)
Ze względu na optymalizację sprzętową i wbudowane generowanie tunelu Gradio, zaleca się uruchomienie notatnika w chmurze:
1. Otwórz plik `Admin_RAG_Project.ipynb` w środowisku Google Colab.
2. **Ważne (Wydajność):** W górnym menu wejdź w `Środowisko wykonawcze` -> `Zmień typ środowiska wykonawczego` i wybierz akcelerator **T4 GPU**. Zapewni to natychmiastowe generowanie odpowiedzi.
3. W panelu plików po lewej stronie upewnij się, że pliki tekstowe znajdują się w folderze `knowledge/` (skrypt potrafi je również zlokalizować w `sample_data/knowledge/`).
4. Uruchom wszystkie 3 komórki kodu. Pierwsza z nich zainstaluje serwer Ollama i pobierze model w tle.
5. Po wykonaniu ostatniej komórki kliknij w wygenerowany publiczny link (np. `https://xyz.gradio.live`), aby otworzyć aplikację Web-GUI.

### Opcja B: Środowisko lokalne (JupyterLab)
1. Upewnij się, że masz uruchomioną usługę **Ollama** na swoim komputerze oraz pobrany model (`ollama pull llama3.2`).
2. Zainstaluj biblioteki: `pip install ollama pymupdf sentence-transformers faiss-cpu gradio`
3. Uruchom plik `.ipynb`. Interfejs webowy uruchomi się na lokalnym porcie (np. `http://127.0.0.1:7860`).

##  Przykładowe zapytania testowe
Aby zweryfikować precyzję modelu i brak halucynacji, można użyć poniższych zapytań w interfejsie aplikacji:
* *"Jak zabezpieczyć porty dostępowe na przełączniku przed atakami MAC Flooding?"*
* *"W jaki sposób usunąć osierocone pakiety w systemie Arch Linux używając pacmana?"*
* *"Mój pod w Kubernetesie ma status CrashLoopBackOff. Jak sprawdzić logi?"*
* *"Jak skonfigurować routing BGP?"* -> **Test odporności**: System poinformuje o braku takiej procedury w dokumentacji, zamiast wymyślać odpowiedź.
### Przykładowe pytania można znaleźć w pliku przykładowe_pytania.txt