# Evdeki Nesnelerin Tespiti — YOLOv8n

Derin Öğrenme dersi Computer Vision ödevi. Zeynep Aslı Çakmak (25120205098)

COCO128 veri seti üzerinde önceden eğitilmiş **YOLOv8n** modeline ince ayar yapılarak evdeki günlük nesneleri tespit eden bir model geliştirildi. Model **Gradio** ile web uygulamasına dönüştürüldü ve telefonla çekilen 5 fotoğrafla test edildi.

## Sonuçlar (test kümesi, 20 görsel)

| Metrik | Değer |
|---|---|
| mAP@0.5 | 0.722 |
| mAP@0.5:0.95 | 0.570 |
| Precision | 0.595 |
| Recall | 0.642 |
| F1-score | 0.618 |
| Ortalama IoU | 0.854 |
| Eğitim süresi | 1.2 dk (Tesla T4) |
| Tahmin süresi | 9.0 ms / görsel |

## Proje bilgileri

- **Görev:** Nesne tespiti
- **Veri seti:** COCO128 (80 sınıf), 88 train / 20 validation / 20 test
- **Model:** YOLOv8n, girdi boyutu 640×640
- **Hiperparametreler:** epochs=30, batch=16, lr0=0.001, freeze=10, seed=42
- **Optimizer:** AdamW
- **Loss:** CIoU + DFL (kutu), BCE (sınıf)
- **Uygulama:** Gradio

## Dosyalar

| Dosya | Açıklama |
|---|---|
| `CNN_Odevi_YOLOv8.ipynb` | Veri hazırlama, eğitim, değerlendirme, fotoğraf testi ve Gradio uygulamasını içeren notebook |
| `best.pt` | Eğitilmiş model ağırlıkları |
| `sonuclar/` | 5 test fotoğrafının tespit çıktıları, eğitim grafikleri ve uygulama ekran görüntüsü |
| `rapor.docx` | Proje raporu |

## Nasıl çalıştırılır

1. `CNN_Odevi_YOLOv8.ipynb` dosyasını [Google Colab](https://colab.research.google.com)'da açın.
2. **Runtime → Change runtime type → T4 GPU** seçin (CPU'da da çalışır, yaklaşık 15 dakika sürer).
3. **Runtime → Run all** ile tüm hücreleri çalıştırın.

Sadece modeli denemek için:

```python
from ultralytics import YOLO
model = YOLO("best.pt")
model.predict("fotograf.jpg", save=True)
```
