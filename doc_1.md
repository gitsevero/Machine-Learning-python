Documentação para iniciantes - Parte 1
Inicialização e configuração de variáveis
Esta parte é responsável por importar bibliotecas necessárias e configurar as variáveis necessárias para o funcionamento do código.

python
Copy code
import cv2 
import os
import numpy as np
import math

cap = cv2.VideoCapture(0)

while 1:
    try:  
        ret, frame = cap.read()
        frame = cv2.flip(frame, 1)
        kernel = np.ones((3, 3), np.uint8)
        roi = frame[100:300, 100:300]
        cv2.rectangle(frame, (100, 100), (300, 300), (0, 255, 0), 0) 
        hsv = cv2.cvtColor(roi, cv2.COLOR_BGR2HSV) 
As bibliotecas importadas são:

cv2: biblioteca OpenCV para processamento de imagem;
os: biblioteca para interação com o sistema operacional;
numpy: biblioteca para trabalhar com matrizes e cálculos numéricos;
math: biblioteca para funções matemáticas.
As variáveis configuradas são:

cap: objeto que representa a câmera;
ret: variável booleana que indica se o frame foi lido com sucesso ou não;
frame: variável que armazena o frame lido da câmera;
kernel: matriz que representa um elemento estruturante para as operações morfológicas;
roi: região de interesse do frame (no caso, um retângulo);
hsv: imagem em escala de cores HSV (hue, saturation, value), usada para detecção de pele.
Definição da máscara de análise do objeto
python
Copy code
lower_skin = np.array([0, 20, 70], dtype=np.uint8)
upper_skin = np.array([20, 255, 255], dtype=np.uint8)
mask = cv2.inRange(hsv, lower_skin, upper_skin)
Nesta parte do código, é definida a máscara que será usada para a detecção da pele do objeto. Essa máscara é criada a partir da definição de um intervalo de cores em HSV que representa a cor da pele humana. Isso é feito usando as variáveis lower_skin e upper_skin, que representam respectivamente o limite inferior e superior do intervalo de cores que definem a pele. A função cv2.inRange cria uma máscara binária que indica quais pixels da imagem estão dentro desse intervalo de cores.

Operações morfológicas na máscara
python
Copy code
mask = cv2.dilate(mask, kernel, iterations=4)

mask = cv2.GaussianBlur(mask, (5, 5), 100)
Nesta parte do código, são aplicadas duas operações morfológicas na máscara criada anteriormente:

Dilatação: essa operação é usada para aumentar o tamanho dos objetos na imagem. Isso é útil para preencher eventuais buracos na máscara e deixá-la mais uniforme. A função cv2.dilate é usada para aplicar essa operação na máscara, usando o elemento estruturante definido pela variável kernel.
Desfoque gaussiano: essa operação é usada para suavizar a máscara e remover