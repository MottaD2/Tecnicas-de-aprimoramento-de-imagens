# Informações sobre o repositório:
Este repositório foi desenvolvido por [Daniella Motta](http://lattes.cnpq.br/5650985365444086) para divulgação dos códigos utilizados na dissertação de mestrado intitulada "Aplicação de técnicas de aprimoramento de imagens em dados de satélitre multiespectral e geofísicos" apresentada à Universidade Federal Fluminense através do Programa de Pós- Graduação em Dinâmicas dos Oceanos e da Terra.

## Técnicas de aprimoramento de imagens

As técnicas de aprimoramento de imagens foram empregadas para produzir visualizações capazes de realçar características relevantes dos dados e apoiar a interpretação geológica em diferentes escalas e contextos geofísicos. Neste trabalho, três técnicas de realce foram reproduzidas e adaptadas, com implementação em linguagem de programação Python visando à reprodutibilidade dos procedimentos e à possibilidade de reaplicação em novos conjuntos de dados. As técnicas foram aplicadas a dados multiespectrais, dados gravimétricos, magnetométricos, gammaespectrométricos e sísmicos, de modo a considerar as particularidades de resolução, ruído, contraste e resposta espectral/geométrica de cada um. Os resultados indicaram que as abordagens adotadas contribuíram para destacar feições e estruturas geológicas, melhorar a continuidade e a identificação de lineamentos e tendências, reduzir ambiguidades interpretativas e aumentar a legibilidade dos produtos finais.

### Técnicas de aprimoramento de imagens utilizadas:

 - ***Structurally Enhanced RGB (seRGB)***

 - ***Structured-Sharpened Continuous RGB (SRGB)***

 - ***Red Relief Image Map (RRIM)***

## **Structurally Enhanced RGB (seRGB)**
O método *Structurally Enhanced RGB*, proposto por [Laake *et al.*(2011)](https://doi.org/10.1144/1354-079310-014), foi desenvolvido para o processamento e a interpretação de imagens de satélite, com o objetivo de aprimorar o contraste estrutural e facilitar o mapeamento geológico. No estudo em questão, os autores empregaram imagens do sensor Landsat 7 ETM+ e utilizaram a técnica para realçar feições geológicas, como descontinuidades e lineamentos, tornando-as mais evidentes na composição RGB e, assim, apoiando a interpretação visual e a extração de informações geológicas a partir dos dados orbitais. O *Structurally Enhanced RGB* funciona como uma etapa de pré-interpretação, capaz de direcionar o mapeamento geológico e estrutural em imagens de satélite, reduzindo ambiguidades e aumentando a confiabilidade das interpretações quando comparadas ao uso exclusivo de composições RGB convencionais.

Em termos gerais, a metodologia parte de uma composição no visível (RGB 321) como referência e incorpora informações do infravermelho e do termal (comportamentos distintos de materiais e condições superficiais), além de um componente de maior resolução espacial (banda pancromática). As etapas principais que constituem esta metodologia são:

     - Carregar a imagem da área de interesse do produto Landsat 7 ETM +;
     - Organizar as bandas para a composição RGB 321, que são as bandas que representam o vermelho (R), o verde (G) e o azul (B), nesta ordem;
     - Criar uma composição a partir das bandas 123 (BGR), que são as bandas na ordem azul (B), verde (G) e vermelho (R);
     - Gerar a imagem da diferença das composições 675 - 321, onde a banda 6 representa a banda termal, a 7 o infravermelho médio, 5 infravermelho de onda curta, 3 o vermelho, 2 o verde e 1 o azul;
     - Obter a razão das bandas 6/8, com a banda 6 sendo a banda termal e a 8 a banda pancromática.

[*Structurally Enhanced RGB - Versão Colab Notebook*](https://colab.research.google.com/drive/1dROCNAXyvyVTtqZNrSS1RbWyD-y-dKSo?usp=sharing)

[*Structurally Enhanced RGB - Versão VsCode*](https://drive.google.com/file/d/11jaE-Foj-w_MbsMpQVTNivACis_MhGd3/view?usp=sharing)


## **Structured-Sharpened Continuous RGB (SRGB)**
O método *Structured-Sharpened Continuous RGB (SRGB)*, proposto por [Laake (2015)](https://doi.org/10.1190/int-2014-0041.1) constitui uma metodologia voltada para a interpretação de dados sísmicos. O procedimento parte de um cubo sísmico e utiliza atributos extraídos do volume para construir uma composição RGB contínua, que é combinada para formar uma imagem RGB aprimorada, voltada a realçar padrões e descontinuidades de interesse interpretativo. A aplicação do método SRGB a volumes sísmicos pode melhorar a representação e a visualização de características geológicas de interesse interpretativo. Ao integrar diferentes atributos em uma composição RGB contínua e aplicar realces estruturais, o SRGB tende a aumentar o contraste e a continuidade espacial de feições, tornando-as mais distinguíveis no volume. Entre os alvos citados pelos autores estão falhas, canais e corpos salinos, que podem ser melhor delineados e acompanhados lateralmente quando comparados à inspeção direta dos dados sísmicos ou de atributos isolados.

De modo geral, o procedimento combina uma codificação em RGB com etapas de aprimoramento de contraste e extração de informações estruturais (via conversão para HSV e realce de bordas), resultando em uma imagem final mais nítida e interpretável. As principais etapas do método SRGB são:

     - Carregamento de dados sísmicos, onde são adquiridas três fatias adjacentes de profundidade dos dados de amplitude sísmica que são carregadas em um cubo, no qual atribuimos um componente de cor para cada fatia, sendo: vermelho (n - 1), verde (n) e azul (n + 1);
     - Projeção em RGB, onde cada fatia é considerada uma das 3 bandas RGB (vermelho, verde e azul) para gerar a composição final;
     - Ajustes no contraste: aprimoramento do contraste da imagem RGB para revelar mais características dos dados;
     - Conversão de RGB para HSV, etapa em que a imagem RGB é convertida para a representação de cor em HSV(hue, saturation and value);
     - A extração do componente saturação, através da imagem HSV, extrai o componente saturação (S) que representa as estruturas geológicas;
     - Detecção de bordas, etapa em que usamos o filtro Sobel para detectar as bordas da imagem e identificar os limites das estruturas geológicas;
     - Geração da imagem RGB, etapa em que combinamos a imagem RGB aprimorada com o contraste e a renderização em escala de cinza, que é o produto da detecção de bordas e forma a imagem SRGB. 

Em síntese, o SRGB se destaca por integrar múltiplos atributos sísmicos em uma única visualização colorida e estruturalmente realçada, reduzindo a dependência de inspeções separadas de dezenas de volumes e mapas de atributos. Ao concentrar informações espectrais (cor), texturais (saturação) e estruturais (realce de bordas) em um produto único, a metodologia favorece uma interpretação mais rápida e consistente, sobretudo na detecção de descontinuidades e na delimitação de geometrias complexas. Assim, o SRGB pode ser entendido como uma ferramenta de apoio à interpretação e à validação de hipóteses geológicas, servindo como ponte entre a exploração qualitativa do volume e etapas subsequentes de mapeamento e integração com outros dados.

[*Structured-Sharpened Continuous RGB (SRGB) - Colab Notebook*]()

## **Red Relief Image Map (RRIM)**
O método *Red Relief Image Map*, ou RRIM, é um método que foi desenvolvido para visualizar mudanças na superfície terrestre a partir de dados derivados de LiDAR. Proposto por [Chiba, Kaneta e Suzuki (2008)](https://www.researchgate.net/publication/237517308_Red_relief_image_map_New_visualization_method_for_three_dimensional_data), [Yokoyama Ryzo; Shirasawa (2002)](https://www.researchgate.net/publication/242390231_Visualizing_Topography_by_Openness_A_New_Application_of_Image_Processing_to_Digital_Elevation_Models) o conceito básico do RRIM consiste na combinação (por meio da multiplicação) de três camadas que descrevem elementos do relevo: a inclinação topográfica e as medidas de aberturas positivas e negativas.
Enquanto a inclinação sintetiza a variação de declividade, as aberturas expressam a geometria local da superfície a partir de diferentes perspectivas: a abertura negativa está associada a porções côncavas do terreno, ao passo que a abertura positiva está associada a porções convexas. A integração dessas camadas tende a aumentar o contraste de feições sutis, favorecendo a identificação de bordas, cristas, depressões e lineamentos, inclusive em áreas onde as variações altimétricas são pouco pronunciadas. Quanto à visualização, o produto final é comumente apresentado em uma escala cromática que parte do branco e incorpora tons de cinza e, principalmente, de vermelho. De modo geral, as áreas mais claras representam superfícies convexas, enquanto as áreas mais escuras representam superfícies côncavas.

Esta metodologia aplica-se tanto a dados topográficos quanto ao Modelo Digital de Elevação, como a dados potenciais, como os magnetométricos, gravimétricos e gamaespectrométricos, que também foram reproduzidos na sísmica. Em ambos os casos, os procedimentos adotados são os mesmos, consistindo em:

    - Leitura e validação dos dados de entrada, com verificação das dimensões da malha, da resolução espacial e do intervalo de altitudes (ou amplitudes), assegurando a consistência do conjunto de dados;
    - Cálculo da inclinação do terreno a partir das derivadas nas direções x e y (gradientes), obtendo-se o módulo do gradiente e convertendo-o posteriormente para valores em graus;
    - Cálculo da abertura topográfica Openness, no qual, para cada ponto, a variação do relevo é avaliada em oito direções ao redor do pixel em função da distância, caracterizando a geometria local da superfície;
    - Determinação dos ângulos máximos e mínimos de visibilidade do terreno a partir dessas variações, os quais representam, respectivamente, as componentes de abertura positiva e negativa;
    - Geração da imagem RRIM, etapa em que os valores de inclinação e de abertura são utilizados como índices no mapa de cores; ao combinar esses atributos, atribui-se uma cor a cada pixel, produzindo a imagem final.


Para viabilizar a aplicação da metodologia a dados sísmicos, foi necessária a adaptação da técnica por meio do emprego de atributos sísmicos, de modo a garantir resultados representativos nesse domínio. Nessa adaptação, os atributos de curvatura e inclinação foram adotados como os principais descritores, sendo integrados às demais etapas do fluxo metodológico. As etapas de desenvolvimento do método *Red Relief Image Map (RRIM)* para dados sísmicos, após sua adaptação, foram:

    - Carregamento de Dados sísmicos;
    - Calcular as derivadas de primeira ordem;
    - Calcular as derivadas de segunda ordem;
    - Gerar as curvaturas máxima e mínima;
    - Calcular a inclinação;
    - Calcular o RRIM através da subtração da curvatura máxima e mínima, que será dividida por 2;
    - Combinar o resultado do RRIM com o slope para obter a imagem com a inclinação;
    - Adaptar o brilho e o contraste do dado gerado para obter uma melhor visualização do RRIM e aplicar a escala de cor vermelha para obter o efeito do *Red Relief Image Map*

O *Red Relief Image Map (RRIM)* é uma técnica eficaz para evidenciar concavidades e convexidades, realçando feições e estruturas presentes em dados topográficos e facilitando a interpretação de padrões morfológicos que podem ser pouco perceptíveis em representações tradicionais. Ao enfatizar contrastes locais associados à geometria do relevo, o método contribui para a identificação de lineamentos, bordas e descontinuidades, além de apoiar análises em diferentes escalas. No entanto, visando ampliar o potencial de realce e avaliar sua aplicabilidade, nesta pesquisa, o método não foi restrito a um Modelo Digital de Elevação (MDE); ele foi adaptado para ser empregado também em dados sísmicos, gravimétricos, magnetométricos e gamaespectrométricos, permitindo explorar até que ponto a metodologia consegue destacar tendências, estruturas e variações espaciais nesses domínios, bem como reconhecer suas limitações e condições de uso.

# Tutorial: Criando um novo ambiente Conda no VS Code e instalando as bibliotecas

## 1. Abrir o Anaconda Prompt

Abra o **Anaconda Prompt** (ou Miniforge Prompt, se você usa Miniforge).

Verifique se o Conda está funcionando:

```bash
conda --version
```

---

## 2. Criar um novo ambiente

Como o RichDEM funciona melhor em versões mais antigas do Python, crie um ambiente com Python 3.10:

```bash
conda create -n richdem_env python=3.10
```

Digite `y` quando solicitado.

---

## 3. Ativar o ambiente

```bash
conda activate richdem_env
```

Verifique a versão do Python:

```bash
python --version
```

O resultado deve ser parecido com:

```text
Python 3.10.x
```

---

## 4. Atualizar pip

```bash
python -m pip install --upgrade pip
```

---

## 5. Instalar GDAL

Primeiro instale o GDAL pelo Conda:

```bash
conda install -c conda-forge gdal
```

Teste:

```bash
python -c "from osgeo import gdal; print(gdal.VersionInfo())"
```

---

## 6. Instalar RichDEM

```bash
pip install richdem
```

Teste:

```bash
python -c "import richdem as rd; print(rd.__version__)"
```

---

## 7. Instalar OpenCV

```bash
pip install opencv-python
```

Teste:

```bash
python -c "import cv2; print(cv2.__version__)"
```

---

## 8. Instalar RVT

```bash
pip install rvt-py
```

Teste:

```bash
python -c "import rvt.vis"
```

---

## 9. Instalar Alive Progress

```bash
pip install alive-progress
```

Teste:

```bash
python -c "from alive_progress import alive_bar"
```

---

## 10. Instalar NumPy

Normalmente ele já vem instalado, mas você pode garantir:

```bash
pip install numpy
```

Teste:

```bash
python -c "import numpy as np; print(np.__version__)"
```

---

## 11. Verificar todos os imports

Crie um arquivo chamado `teste.py` com:

```python
import cv2
import numpy as np
import richdem as rd
from osgeo import gdal
import rvt.vis
import time
import os
from alive_progress import alive_bar

print("Todas as bibliotecas foram carregadas com sucesso.")
```

Execute:

```bash
python teste.py
```

Se aparecer:

```text
Todas as bibliotecas foram carregadas com sucesso.
```

a instalação foi concluída.

---

## 12. Configurar o VS Code

Abra o VS Code.

Pressione:

```text
Ctrl + Shift + P
```

Digite:

```text
Python: Select Interpreter
```

Selecione:

```text
richdem_env
```

ou o caminho correspondente ao ambiente criado.

---



# Resumo dos comandos

```bash
conda create -n richdem_env python=3.10
conda activate richdem_env

python -m pip install --upgrade pip

conda install -c conda-forge gdal

pip install richdem
pip install opencv-python
pip install rvt-py
pip install alive-progress
pip install numpy
```


[*Red Relief Image Map - Colab Notebook*]()

[*Red Relief Image Map - Colab Notebook*]()

[*Red Relief Image Map - Colab Notebook*]()

[*Red Relief Image Map - Colab Notebook*]()

