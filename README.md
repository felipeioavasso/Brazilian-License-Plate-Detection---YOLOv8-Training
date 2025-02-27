# YOLOv8 - Treinamento para Detecção de Placas Brasileiras

Este repositório contém o processo completo de treinamento do modelo **YOLOv8** para a detecção de placas de veículos no Brasil. O modelo é treinado utilizando um dataset específico de placas brasileiras e pode ser utilizado para reconhecimento automático de placas em imagens ou vídeos.

## 📌 Funcionalidades
✔ Treinamento do modelo **YOLOv8** para detecção de placas  
✔ Uso do Google Colab para treinamento e armazenamento no Google Drive  
✔ Extração e manipulação do dataset no formato YOLO  
✔ Avaliação do modelo treinado com métricas e gráficos  
✔ Download do modelo treinado (`best.pt`) para uso futuro  

## 📂 Estrutura do Repositório
- `dataset/` → Dataset utilizado para o treinamento  
- `training_script.ipynb` → Código utilizado para o treinamento do modelo  
- `weights/` → Modelos treinados salvos após o treinamento  

## 🌟 Como Usar
### 1️⃣ Instale as dependências
```bash
pip install ultralytics
```
### 2️⃣ Faça o upload do dataset
No Google Colab, faça upload do arquivo `.zip` contendo as imagens anotadas no formato YOLO e extraia os arquivos:
```python
import zipfile

zip_path = "/content/dataset.yolov8.zip"
extract_path = "/content/dataset"

with zipfile.ZipFile(zip_path, 'r') as zip_ref:
    zip_ref.extractall(extract_path)
```

### 3️⃣ Configure o treinamento
Carregue o modelo base YOLOv8 e inicie o treinamento:
```python
from ultralytics import YOLO

model = YOLO("yolov8n.pt")
model.train(data="/content/dataset/data.yaml", epochs=50, imgsz=640, save_period=5)
```

### 4️⃣ Avalie os resultados
Após o treinamento, visualize os gráficos gerados:
```python
import glob
from IPython.display import display
from PIL import Image

result_images = glob.glob("/content/runs/detect/train/*.png")

for img_path in result_images:
    display(Image.open(img_path))
```

### 5️⃣ Baixe o modelo treinado
Após o treinamento, faça o download do modelo `best.pt` para utilização em inferências:
```python
from google.colab import files

files.download("/content/runs/detect/train/weights/best.pt")
```

## 🎯 Aplicação
O modelo treinado pode ser usado para:  
🏎 Monitoramento de tráfego e controle de veículos  
🚳️ Segurança e fiscalização de trânsito  
🏢 Controle de acesso em estacionamentos  

## 📌 Referências
- [Documentação do Ultralytics YOLOv8](https://docs.ultralytics.com/)  
- [Dados do IBGE para validação de cidades](https://servicodados.ibge.gov.br/api/v1/localidades/municipios)  

