# Conversor de Vídeo para Frames (converte_frame)

Este projeto contém um script Python (`main.py`) que utiliza a biblioteca OpenCV para extrair todos os frames (quadros) de um arquivo de vídeo e salvá-los como imagens individuais no formato `.png` em uma pasta de destino.

## Tecnologias Utilizadas

* **Python 3**
* **OpenCV-Python** (`cv2`): Para manipulação e leitura de vídeo.
* **OS**: Para manipulação de caminhos de arquivos de forma independente do sistema operacional.

## Instalação

Para rodar este projeto, você precisará ter o Python 3 e o Git instalados.

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/SEU-USUARIO/converte_frame.git](https://github.com/SEU-USUARIO/converte_frame.git)
    cd converte_frame
    ```
    *(Substitua `SEU-USUARIO` pelo seu nome de usuário no GitHub)*

2.  **Crie e ative um ambiente virtual:**
    ```bash
    # Criar o ambiente
    python -m venv .venv
    
    # Ativar no Windows
    .\.venv\Scripts\activate
    
    # Ativar no macOS/Linux
    source .venv/bin/activate
    ```

3.  **Instale as dependências:**
    O arquivo `requirements.txt` contém as bibliotecas necessárias.
    ```bash
    pip install -r requirements.txt
    ```

## Como Usar

1.  **Prepare os arquivos:**
    * Coloque o arquivo de vídeo que você deseja processar dentro da pasta do projeto (ex: `meu_video.mp4`).
    * Crie uma pasta para onde os frames serão salvos (ex: `frames`).

2.  **Edite o `main.py`:**
    Abra o arquivo `main.py` e altere a última linha para apontar para o seu vídeo e a sua pasta de saída:

    ```python
    # Altere esta linha no final do arquivo
    frames_de_video("meu_video.mp4", "frames") 
    ```

3.  **Execute o script:**
    Com o ambiente virtual ativo, rode o comando:
    ```bash
    python main.py
    ```

O script irá ler o vídeo e salvar cada frame (ex: `0.png`, `1.png`, `2.png`, ...) dentro da pasta `frames`.

## Explicação do Código (`main.py`)

O código é dividido em uma função principal que faz todo o processamento.

```python
import cv2
import os

# Importa as bibliotecas necessárias:
# - cv2: OpenCV, para processamento de vídeo.
# - os: Para interagir com o sistema operacional (manipular caminhos de arquivos).
```

### A Função `frames_de_video`

```python
def frames_de_video(entrada, caminho_saida):
    # 1. Abre o arquivo de vídeo para leitura
    entrada_capturada = cv2.VideoCapture(entrada)
    
    # 2. Inicializa um contador para nomear os arquivos
    cont = 0
    
    # 3. Inicia um loop que continua enquanto o vídeo estiver aberto
    while entrada_capturada.isOpened():
        
        # 4. Lê o próximo frame do vídeo
        #    retorno = True se um frame foi lido com sucesso, False se for o fim do vídeo
        #    frame   = Os dados da imagem (o frame em si)
        retorno, frame = entrada_capturada.read()
        
        # 5. Verifica se o frame foi lido com sucesso
        if retorno:
            # 6. Salva o frame como uma imagem PNG
            #    os.path.join(caminho_saida, "%d.png") cria o caminho seguro (ex: "frames/0.png")
            #    %cont formata o nome do arquivo com o número do contador
            cv2.imwrite(os.path.join(caminho_saida, "%d.png") %cont, frame)
            
            # 7. Incrementa o contador para o próximo nome de arquivo
            cont += 1
            
        else:
            # 8. Se 'retorno' for False, significa que o vídeo acabou.
            #    O loop é interrompido.
            break
            
    # 9. Libera os recursos (fecha o arquivo de vídeo)
    cv2.destroyAllWindows()
    entrada_capturada.release()
```

### Execução do Script

```python
# Esta é a linha que chama a função e inicia o processo.
# "caminho_video.mp4" é o argumento 'entrada'
# "frames" é o argumento 'caminho_saida'
frames_de_video("caminho_video.mp4", "frames")
```

## Inspiração

O desenvolvimento deste script foi inspirado pelo tutorial em vídeo do canal "Como Programar", que demonstra a extração de frames com OpenCV.

* **YouTube:** [Extrair Frames de Vídeo com Python e OpenCV](https://www.youtube.com/watch?v=hpX_L5dYh-g)
