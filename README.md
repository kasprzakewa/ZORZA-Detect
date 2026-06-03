# ZORZA-Detect: Zaawansowane Optyczne Rozpoznawanie Zagrożeń Aerokosmicznych

<table border="0" cellpadding="10" cellspacing="0" align="center" style="border-collapse: collapse; border: none;">
  <tr style="border: none;">
    <td valign="middle" style="border: none; padding-right: 20px;">
      <img width="100" height="100" alt="ZORZA-Detect logo left" src="https://github.com/user-attachments/assets/7d118478-73a8-4626-91b6-984f465a00ee" />
    </td>
    <td valign="middle" style="border: none; text-align: justify;">
      <p>Repozytorium zawiera zoptymalizowane skrypty do trenowania i walidacji modeli z rodziny YOLO (YOLOv8n / YOLO26n) w zadaniu precyzyjnej detekcji odłamków orbitalnych na niskiej orbicie okołoziemskiej (LEO).</p>
      <p>Kluczowym osiągnięciem projektu jest uodpornienie klasyfikatora na efekt <em>Earthshine</em> (odbicia światła od atmosfery i powierzchni planety) poprzez zastosowanie techniki Hard Negative Mining z użyciem tekstur Ziemi.</p>
    </td>
    <td valign="middle" style="border: none; padding-left: 20px;">
      <img width="100" height="100" alt="ZORZA-Detect logo right" src="https://github.com/user-attachments/assets/7d118478-73a8-4626-91b6-984f465a00ee" />
    </td>
  </tr>
</table>

---

## Zawartość Repozytorium

* **`train.ipynb`**
  Główny skrypt uczący, który automatycznie pobiera, formatuje i łączy surowe zbiory danych (etykiety ze śmieciami kosmicznymi oraz puste tła powierzchni Ziemi). Konfiguruje środowisko pod architekturę YOLO i przeprowadza proces optymalizacji wag z wykorzystaniem mechanizmu Early Stopping.
* **`validate.ipynb`**
  Moduł ewaluacyjny służący do oceny jakościowej i ilościowej wyuczonego modelu. Zawiera zoptymalizowane funkcje do generowania wykresów porównawczych oraz przeprowadzania płynnej inferencji na dynamicznym materiale wideo.

---

## Wykorzystane Zbiory Danych

Projekt opiera się na fuzji trzech niezależnych zbiorów danych, które należy podpiąć pod środowisko uruchomieniowe (np. Kaggle):

1. **Główny zbiór odłamków orbitalnych:** [Debris Detection Dataset (autor: Sadia Nawar)](https://www.kaggle.com/datasets/sadianawar/debris-detection-dataset)
2. **Autorski zbiór teł planetarnych:** [Earth Satellite Images 512x512 (autor: Ewa Kasprzak)](https://www.kaggle.com/datasets/ewakasprzak/earth-satellite-images-512x512)
3. **Materiał wideo do testów dynamicznych:** [Space Debris Collision Video (autor: Ewa Kasprzak)](https://www.kaggle.com/datasets/ewakasprzak/space-debris-collision)

> **Uwaga:** Skrypty domyślnie wykorzystują ścieżki platformy Kaggle (`/kaggle/input/...`). W przypadku uruchamiania kodu lokalnie, należy zaktualizować zmienne ścieżkowe w sekcjach konfiguracji.

---

## Wymagania Środowiskowe

Kod został zoptymalizowany do działania na akceleratorach GPU (np. NVIDIA Tesla T4). Do poprawnego uruchomienia wymagane są następujące biblioteki:

* `ultralytics` (silnik YOLO)
* `pandas`
* `matplotlib`
* `Pillow` (PIL)
* `opencv-python` (cv2)
* `ffmpeg` (do konwersji i wyświetlania wideo w notatnikach Jupyter/Kaggle)

---

## Instrukcja Uruchomienia

1. Zaimportuj notatniki `train.ipynb` oraz `validate.ipynb` do swojego środowiska (np. Kaggle).
2. Dodaj wymienione wyżej zbiory danych do przestrzeni roboczej.
3. W pliku `train.ipynb` uruchom wszystkie komórki, aby przetworzyć dane i wytrenować model. Zapisane wagi (`best.pt`) pojawią się w folderze wyjściowym.
4. Skopiuj ścieżkę do wytrenowanego modelu i podmień ją w pliku `validate.ipynb` w zmiennych konfiguracyjnych.
5. Uruchom `validate.ipynb`, aby wygenerować panele analityczne i przetworzyć nagranie z kolizji. Wygenerowany plik `.mp4` odtworzy się bezpośrednio w komórce notatnika.
