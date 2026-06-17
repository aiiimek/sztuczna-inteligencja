## Laboratorium 5 - Wnioski z analizy (LSTM vs GRU)

**Przeprowadzone eksperymenty (zgodnie z wytycznymi):**
- Zmiana atrybutu predykcji z `High` na `Close`.
- Zmiana optymalizatora na `Adam` (przyspieszył zbieżność względem `RMSprop`).
- Zastosowanie mechanizmu `EarlyStopping` opartego na stracie walidacyjnej (`val_loss`) ze współczynnikiem `validation_split=0.1`.
- Udało się uzyskać ostateczny błąd RMSE poniżej 2.0 dla obu architektur.

**Porównanie i obserwacje:**
1. **Szybkość uczenia:** Model zbudowany na bramkach GRU trenował się zauważalnie szybciej w przeliczeniu na pojedynczą epokę. Wynika to z faktu, że GRU ma prostszą strukturę i mniej parametrów do aktualizacji (łączy bramkę wejściową i zapominania w jedną bramkę aktualizacji).
2. **Dokładność (RMSE / MAE):** Oba modele poradziły sobie bardzo dobrze, generując błąd procentowy na poziomie poniżej 1%. Predykcje LSTM bywały nieznacznie bardziej "wygładzone", jednak GRU równie precyzyjnie reagowało na nagłe spadki cen.
3. **Najlepsza konfiguracja:** Ostatecznie najbardziej optymalną konfiguracją okazała się sieć **GRU z optymalizatorem Adam**. Posiada świetny kompromis między niższym kosztem obliczeniowym a wysoką skutecznością, a dodanie `EarlyStopping` pozwoliło uniknąć over-fittingu podczas 100 epok treningowych.