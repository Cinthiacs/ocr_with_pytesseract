# ocr_with_pytesseract

- Este algorítimo foi produzido para realizar a leitura de um documento de identificação e exibir sua imagem em tempo real em uma câmera.

## Sobre o projeto
- Utiliza as bibliotecas Pytesseract e OpenCV para realizar a leitura de um documento de identificação e exibir sua imagem em tempo real em uma câmera. 

## Pré-requisitos
* Certifique-se de ter as seguintes bibliotecas instaladas em sua máquina:
* Pytesseract
* OpenCV
* Você pode instalá-las usando o comando pip:

 #### !pip install pytesseract
 #### !pip install opencv-python
 
1. A primeira biblioteca é responsável pela realização do OCR (Optical Character Recognition) que reconhece os caracteres da imagem. 

2. A segunda biblioteca é utilizada para realizar o processamento de imagens e exibição da imagem em tempo real.
 
- Você precisa ter o Tesseract-OCR instalado em sua máquina. 
- Para usuários do Windows, você pode baixá-lo aqui: https://github.com/UB-Mannheim/tesseract/wiki. 
- Certifique-se de adicionar o diretório de instalação ao PATH do sistema.
 
## Como usar
1. Clone este repositório em sua máquina local.
2. Abra o arquivo main.py em sua IDE Python de sua preferência.
3. Execute o script.

## Como funciona
* O script realiza os seguintes passos:

1. Abre a câmera e começa a exibir a imagem em tempo real.
2. Aplica alguns filtros e definições de tamanho na imagem.
3. Converte a imagem para escala de cinza e aplica um limiar para obter apenas os pixels mais escuros (texto preto) na imagem.
4. Extrai o texto da imagem usando a biblioteca Pytesseract.
5. Exibe o texto extraído no console.

## Exemplo
* A seguir, é mostrado um exemplo de como a imagem é processada e como o texto é extraído:

import cv2
import pytesseract
import os
import re

# Configuração do Pytesseract
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract'

# Abre a imagem
image = cv2.imread('Rg_fake.png')

# Converte a imagem para escala de cinza e aplica um limiar
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
gray = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)[1]

# Salva a imagem em um arquivo temporário
filename = "{}.png".format(os.getpid())
cv2.imwrite(filename,gray)

# Extrai o texto da imagem
text = pytesseract.image_to_string(Image.open(filename), lang='por')

# Remove o arquivo temporário
os.remove(filename)

# Plota a imagem em escala de cinza
plt.imshow(gray)

# Exibe o texto extraído
print(type(text))
print(re.sub(r'[^\W{A-Z}]', '', text))


## Contribuição

Contribuições são sempre bem-vindas! Se você quiser adicionar alguma funcionalidade ou corrigir um problema, sinta-se à vontade para enviar um pull request.

## Autora:
Cinthia Cavalheiro.
