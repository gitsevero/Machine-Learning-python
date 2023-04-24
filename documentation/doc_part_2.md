## Parte 2: Detecção de Mãos e Desenho de Contornos

Essa parte do código é responsável por detectar as mãos na imagem e desenhar os contornos das mãos encontradas. Primeiramente, é aplicado um filtro na máscara para remover ruídos e depois são encontrados os contornos das regiões brancas presentes na imagem. O maior contorno encontrado é considerado como sendo o contorno da mão. Em seguida, é desenhado o contorno da mão na imagem original e calculado o ponto central da mão.

Código:
```python
contours = max(contours, key=lambda x: cv2.contourArea(x))
if contours.any():
    cnt = contours
    M = cv2.moments(cnt)
    cx = int(M['m10'] / M['m00'])
    cy = int(M['m01'] / M['m00'])
    cv2.drawContours(frame, [cnt + (100, 100)], 0, (0, 0, 255), 2)
    cv2.circle(frame, (cx + 100, cy + 100), 5, (0, 0, 255), -1)
```

### Explicação do código

- `contours = max(contours, key=lambda x: cv2.contourArea(x))`: essa linha de código encontra o maior contorno na imagem, que será considerado como sendo o contorno da mão.

- `if contours.any():`: verifica se algum contorno foi encontrado.

- `cnt = contours`: armazena o contorno encontrado na variável `cnt`.

- `M = cv2.moments(cnt)`: calcula as propriedades do contorno, como área, centroide e orientação.

- `cx = int(M['m10'] / M['m00'])` e `cy = int(M['m01'] / M['m00'])`: calculam o ponto central da mão a partir das propriedades do contorno.

- `cv2.drawContours(frame, [cnt + (100, 100)], 0, (0, 0, 255), 2)`: desenha o contorno da mão na imagem original.

- `cv2.circle(frame, (cx + 100, cy + 100), 5, (0, 0, 255), -1)`: desenha um círculo no centro da mão para indicar a posição do ponto central.

### Possíveis melhorias

Uma possível melhoria seria a utilização de técnicas de aprendizado de máquina para melhorar a detecção de mãos na imagem, como a utilização de redes neurais convolucionais. Isso poderia melhorar a precisão da detecção e permitir a detecção de mãos em diferentes posições e iluminações.