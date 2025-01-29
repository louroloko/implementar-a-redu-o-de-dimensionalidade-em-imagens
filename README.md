# implementar-a-redu-o-de-dimensionalidade-em-imagens
Vamos implementar a redução de dimensionalidade em imagens para redes neurais sem usar bibliotecas externas.
from PIL import Image

# Carregar a imagem
imagem = Image.open('caminho/para/sua/imagem.jpg')

# Converter para tons de cinza
imagem_cinza = imagem.convert('L')

# Converter a imagem para uma lista de pixels
pixels = list(imagem_cinza.getdata())

# Obter as dimensões da imagem
largura, altura = imagem_cinza.size
# Definir o tamanho do bloco
tamanho_bloco = 4

# Reduzir a resolução da imagem
pixels_reduzidos = []
for y in range(0, altura, tamanho_bloco):
    for x in range(0, largura, tamanho_bloco):
        bloco = [pixels[(y+i)*largura + (x+j)] for i in range(tamanho_bloco) for j in range(tamanho_bloco) if y+i < altura and x+j < largura]
        media_bloco = sum(bloco) // len(bloco)
        pixels_reduzidos.extend([media_bloco] * tamanho_bloco * tamanho_bloco)

# Criar uma nova imagem com a resolução reduzida
imagem_reduzida = Image.new('L', (largura, altura))
imagem_reduzida.putdata(pixels_reduzidos)
import matplotlib.pyplot as plt

# Exibir a imagem original
plt.subplot(1, 2, 1)
plt.title('Imagem Original')
plt.imshow(imagem_cinza, cmap='gray')

# Exibir a imagem reduzida
plt.subplot(1, 2, 2)
plt.title('Imagem Reduzida')
plt.imshow(imagem_reduzida, cmap='gray')

plt.show()
