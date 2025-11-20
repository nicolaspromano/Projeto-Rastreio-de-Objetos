# 🎥 Detector de Movimento em Tempo Real com OpenCV e Tkinter

Este projeto é uma aplicação do conteúdo abordado na disciplina de Processamento Digital de Sinais. Ele utiliza a biblioteca **OpenCV** para detectar movimento em arquivos de vídeo (MP4, AVI, MOV) usando a técnica de **Subtração de Background Baseada em Diferença de Frames**.

O software inclui uma interface gráfica (GUI) desenvolvida com **Tkinter** para permitir ao usuário ajustar e comparar diferentes conjuntos de parâmetros de processamento.

## 🧠 Metodologia de Detecção (Visão Computacional)

O núcleo do projeto é a função `processar_video`, que aplica uma sequência de filtros para isolar e quantificar o movimento:

1.  ### **Pré-Processamento (Ruído)**
    * A imagem é convertida para **Escala de Cinza** (`cv2.cvtColor`).
    * Aplica-se o **Filtro Gaussiano** (`cv2.GaussianBlur`) para reduzir o ruído e suavizar a imagem. O **Tamanho de Suavização (Blur Size)** é um parâmetro chave aqui, afetando a retenção de detalhes.

2.  ### **Diferença de Frames**
    * A função `cv2.absdiff` calcula a diferença absoluta de pixel entre o **frame atual** e o **frame imediatamente anterior**.
    * **Resultado:** Uma imagem de diferença, onde apenas os pixels que mudaram de posição (o movimento) possuem valores altos.

3.  ### **Binarização (Máscara de Movimento)**
    * Aplica-se a **Limiarização** (`cv2.threshold`) sobre a imagem de diferença, convertendo-a em uma **máscara binária**.
    * Pixels acima do **Limiar de Binarização** tornam-se brancos (movimento); o restante, preto (fundo). Este limiar controla a sensibilidade do detector.

4.  ### **Detecção e Quantificação**
    * Aplica-se a **Dilatação** (`cv2.dilate`) para preencher pequenas lacunas e unir regiões de movimento.
    * **Contornos:** `cv2.findContours` identifica regiões conectadas na máscara binária.
    * Aplica-se o filtro **Área Mínima do Contorno** para ignorar pequenos ruídos e movimentos irrelevantes.
    * O movimento é quantificado contando o número total de **pixels brancos** na máscara em cada frame.



---

## 💻 Interface Gráfica (Tkinter)

A GUI permite a fácil configuração dos principais parâmetros do algoritmo e a visualização dos resultados.

### Parâmetros Ajustáveis:

| Parâmetro | Função | Dica de Uso |
| :--- | :--- | :--- |
| **Tamanho de Suavização** | Tamanho do kernel do Filtro Gaussiano. | **Maior** = Mais Suavização (bom para vídeo granulado). |
| **Limiar de Binarização** | Limite de sensibilidade para detectar mudança. | **Menor** = Mais Sensível (risco de falsos positivos). |
| **Área Mínima** | Tamanho mínimo (em pixels) de uma área para ser considerada movimento. | Filtra pequenos ruídos ou objetos irrelevantes. |

### Botões:

* **Selecionar Vídeo:** Abre uma caixa de diálogo para carregar o arquivo.
* **Executar Teste:** Inicia o processamento do vídeo com os parâmetros selecionados, exibindo as janelas do OpenCV e gerando um gráfico de movimento.
* **Gerar Relatório:** Cria um gráfico de barras comparando a **Média de Pixels em Movimento** de todos os testes realizados e salva os resultados em um arquivo `relatorio_deteccao_movimento.csv`.

---

## 🚀 Como Rodar o Projeto

### 1. Pré-requisitos

O projeto requer as seguintes bibliotecas. A **OpenCV** é a dependência principal para o PDI.

```bash
pip install numpy pandas matplotlib opencv-python
```

### 2. Execução

Salve o código como um arquivo Python e execute-o:

```bash
python [nome_do_arquivo].py
```
---
## Autores

Nicolas Romano

Maria Eduarda Romana

Vitor Luiz Viana
