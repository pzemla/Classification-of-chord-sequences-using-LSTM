[![en](https://img.shields.io/badge/language-EN-blue.svg)](https://github.com/pzemla/Classification-of-chord-sequences-using-LSTM/blob/main/README.md)
# Klasyfikacja sekwencji akordów wykorzystując LSTM

**Jak uruchomić**
1. Upewnij się że pliki train.pkl i test.pkl są w tym samym folderze co LSTM.ipynb
2. Uruchom LSTM.ipynb w Jupyter Notebook


**Zależności**

Python 3.9.13

matplotlib 3.8.3

notebook 7.1.2

numpy 1.24.1

pandas  2.2.1

scikit-learn 1.4.1.post1 Python 3.9.13

torch 2.2.1+cu118

## Przegląd

Celem tego projektu jest zbudowanie sieci Long Short Term Memory (LSTM) do klasyfikowania sekwencji do jednej z 5 klas. LSTM jest zaimplementowany przy użyciu Pythona z biblioteką Pytorch. Projekt ten służy jako ćwiczenie edukacyjne i praktyczne zastosowanie technik głębokiego uczenia się do zadań klasyfikacji sekwencji.

Dane treningowe i testowe są sekwencjami akordów z przypisanym kompozytorem danego utworu zapisanymi w pliku pkl. Celem sieci jest klasyfikacja sekwencji do odpowiedniego kompozytora.

Liczba sekwencji na kompozytora jest niezbalansowana (co widać na poniższym histogramie), co utrudnia wytrenowanie sieci, ponieważ ma tendencje do klasyfikowania wszystkich sekwencji do jednej klasy/kompozytora. W celu bardziej zbalansowanego trenowania sieci zastosowano wagi przypisane do klas na podstawie ich liczby sekwencji (im mniej sekwencji ma klasa tym większa waga).

![image](https://github.com/pzemla/Classification-of-chord-sequences-using-LSTM/assets/135070990/fa600388-5e6b-44b6-a052-e98630cbc7c7)

Sieć LSTM została wykorzystana, ponieważ dane są danymi sekwencyjnymi, przez co najlepszym wyborem z prostszych modeli sieci neuronowych są różne typy rekurencyjnych sieci neuronowych, a LSTM przykłada ona dużą wagę do każdego elementu sekwencji, niezależnie od tego czy znajduje się on na początku, w środku czy końcu sekwencji (w przeciwieństwie do zwykłej sieci rekurencyjnej).

Dane przed przetworzeniem wstępnym (sekwencja i przypisana klasa):
 
(array([ -1., -1., -1., ..., 78., 40., 144.]), 0)

(array([ -1., -1., 144., ..., 32., -1., -1.]), 0) 

## Optymalizator i funkcja straty

Optymalizator – Adam (learning rate=0.0001) 

funkcja straty – Cross-entropy loss 

Optymalizator Adam został wybrany ponieważ dynamicznie dostosowuje learning rate do każdego parametru podczas treningu, przez co nie trzeba dostosowywać malenia współczynnika uczenia (learning rate decay). Spośród innych optymalizatorów testowanych (Adagrad i RMSprop) zapewniał on najlepsze wyniki w datasecie testowym.

Funkcja straty entropii krzyżowej (cross-entropy loss) została wybrana ponieważ jej wynik może być interpretowany jako prawdopodobieństwo przynależności do każdej klasy, przez co często wykorzystuje się ją do modeli klasyfikujących.

## Rezultaty

Dokładność: 70% 

Dokładność poszczególnych klas: 81% 61% 28% 67% 45% 

Średnia dokładności klas: 57%

Chociaż ogólna dokładność jest stosunkowo wysoka, dokładność każdej indywidualnej klasy różni się w zależności od liczby sekwencji w danych klasowych. Bez dodawania wag do każdej klasy, LSTM zaklasyfikował większość sekwencji do pierwszej klasy, co pozwoliło uzyskać wysoką dokładność, ale średnia dokładność klasy wynosiła tylko około 20% (100% dla pierwszej klasy, 0% dla wszystkich pozostałych). Dokładność poszczególnych klas można poprawić poprzez zwiększenie wag klas, dzięki czemu klasy z mniejszą ilością danych będą miały większy wpływ na trenowanie sieci. Inną możliwą metodą mogłoby być wyrównanie ilości danych we wszystkich klasach, poprzez zmniejszenie liczby sekwencji akordów w pierwszej klasie, albo powielenie ich w innych klasach z mniejszą ilością danych.
