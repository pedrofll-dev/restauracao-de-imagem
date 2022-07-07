# `Restauracao e melhoramento de imagem `
# `Image enhancement and restoration`

## Apresentação

O presente projeto foi originado no contexto das atividades da disciplina de pós-graduação *EA979A - Introdução a Computação Gráfica e Processamento de Imagens*, 
oferecida no primeiro semestre de 2022, na Unicamp, sob supervisão da Profa. Dra. Paula Dornhofer Paro Costa, do Departamento de Engenharia de Computação e Automação (DCA) da Faculdade de Engenharia Elétrica e de Computação (FEEC).

> |Nome  | RA | Curso|
> |--|--|--|
> | Pedro Felipe Lucena Lima  | 204536  | Eng. Elétrica|


## Descrição do Projeto
> O projeto tem finalidade de desenvolver e aplicar tecnicas de restauracao de imagens, em especial com uso de machine learning (Neural upscale),para imagens de baixa resolução ou de qualidade gráfica pobre.
> O principal encorajamento desse projeto é a popularização do uso de IA para o upscaling de imagens (Nvidia DLSS,AMD FSR,NIS,etc.) para reduzir o custo computacional de processamento de imagem ou simples melhora gráfica.
> A meta final é utilizar os algoritmos desenvolvidos em imagens de baixa resolução e uma possível implementação desses para a criação de um pack de texturas em um dado videogame.
> 

## Abordagem Adotada
> - bases de imagens: div2k(https://data.vision.ee.ethz.ch/cvl/DIV2K/), flickr2k( http://cv.snu.ac.kr/research/EDSR/Flickr2K.tar), e imagens customizadas como dataset de alta resolução(HR);
> - modelagens adotadas: Uso do ESRGAN  como modelo base de um removedor de danos de imagens;
> - Simplificações: 
Mudança do upscaling original do ESRGAN de 4x para 1x para economia de memória e maior velocidade no treinamento do modelo.
Downscaling do dataset(HR) e utilizando filtros do tipo box sem criação de artefatos ou perda de qualidade perceptivel para reduzir o uso de memória.



## Resultados Finais
> Foi obtido um modelo customizado para utilização em conjunto com o ESRGAN na restauração de danos de imagens em especial danos causados por compressão do tipo "block" ,comum em mapas texturas de videogames antigos,

## Discussão
> * Não foi possível implementar o modelo customizado para a criação de um novo conjunto de texturas de um videogame específico, foram testados os jogos Doom(1993) Doom 3 (2004) e Fallout3(2008).No caso o processo de modificação demonstrou requerer muito tempo e um conhecimento específico das engines dos jogos citados.
> * As principais dificuldades durante o projeto foram a utilização do dataset, sendo inicialmente utilizado um simples dataset de imagens customizadas de screenshoots de alta resolução de outros jogos, no qual o modelo customizado se demonstrou ineficiente (resultados deletados). Após tal incidente foi utilizado um dataset de imagens realistas.
> * Outra dificuldade foi o tempo de execução do treino dos dados sendo o tempo médio de 1000 iterações 30 min, mesmo após todas as modificações apresentadas anteriormente. Foram realizadas mais de 100000 iterações no total.
> * Limitações: bom funcionamento para danos de compressão ,mas danos do tipo dither e outras tipos de ruído não apresentam efeitos satisfatórios. Além disso, há perda de sinais de alta frequêcia nas imagens finais.

## Novos métodos

> * Utilização do modelo Real-ESRGAN/ ESRGAN como principal referência dado a utilização de texturas artificiais.
>   para criação de modelos customizados para imagens artificiais
> * Ferramenta traiNNer/Basic-sr para treino de um modelo customizado 
## Histórico & Resultados finais da pesquisa
>   teste com modelos já preestabelecidos- real-esrgan-4x e 2x
>   Aplicação baseada em [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN).
>   * mudança no tamanho do upscaling (4x para 2x) devido ao aumento significativo do tamanho dos arquivos. 
>   * teste em huds - ver pasta de imagens 
>   * problemas na criação de subimagens para um novo modelo específico (alta utilização de vram)
>   * Utilização do dataset div2k(https://data.vision.ee.ethz.ch/cvl/DIV2K/) e outras imagens customizadas como conjunto de dados de alta resolução (HR) 
>   * Downscaling do dataset(HR) utilizando filtros do tipo box sem criação de artefatos ou perda de qualidade perceptivel para reduzir o uso de memória.
>   * mudança do scaling de 2x para 1x
>   * Treino da rede ESRGAN utilizando o dataset e a ferramenta traiNNer(https://github.com/victorca25/traiNNer)/Basic-sr 
>   * Teste em imagens com dano de compressão do tipo "block"
>   * Resultados satisfatorios
### About Real-ESRGAN

![realesrgan_logo](https://github.com/xinntao/Real-ESRGAN/raw/master/assets/realesrgan_logo.png)  
Real-ESRGAN is a Practical Algorithms for General Image Restoration.

> [[Paper](https://arxiv.org/abs/2107.10833)] [[Project Page]](https://github.com/xinntao/Real-ESRGAN) &emsp; [[YouTube Video](https://www.youtube.com/watch?v=fxHWoDSSvSc)] [[Bilibili](https://www.bilibili.com/video/BV1H34y1m7sS/)] &emsp; [[Poster](https://xinntao.github.io/projects/RealESRGAN_src/RealESRGAN_poster.pdf)] [[PPT slides](https://docs.google.com/presentation/d/1QtW6Iy8rm8rGLsJ0Ldti6kP-7Qyzy6XL/edit?usp=sharing&ouid=109799856763657548160&rtpof=true&sd=true)]<br>
> [Xintao Wang](https://xinntao.github.io/), Liangbin Xie, [Chao Dong](https://scholar.google.com.hk/citations?user=OSDCB0UAAAAJ), [Ying Shan](https://scholar.google.com/citations?user=4oXBp9UAAAAJ&hl=en) <br>
> Tencent ARC Lab; Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences

![img](https://github.com/xinntao/Real-ESRGAN/raw/master/assets/teaser.jpg)
**Note that RealESRGAN may still fail in some cases as the real-world degradations are really too complex.**

### Instalação

1. Clone repo

    ```bash
    git clone https://github.com/xinntao/Real-ESRGAN.git
    cd Real-ESRGAN
    ```

1. Install dependent packages

    ```bash
    # Install basicsr - https://github.com/xinntao/BasicSR
    # We use BasicSR for both training and inference
    pip install basicsr
    # facexlib and gfpgan are for face enhancement
    pip install facexlib
    pip install gfpgan
    pip install -r requirements.txt
    python setup.py develop
    ```

## Referências Bibliográficas

Real-ESRGAN: Training Real-World Blind Super-Resolution with Pure Synthetic Data
Xintao Wang, Liangbin Xie, Chao Dong, Ying Shan
Underwater image enhancement: a comprehensive review,recent trends, challenges and applications Smitha Raveendran1 · Mukesh D. Patil2 · Gajanan K. Birajdar1

https://www.reedbeta.com/blog/understanding-bcn-texture-compression-formats/

An In-Depth Survey of Underwater Image
Enhancement and Restoration
MIAO YANG 1,2,3,5,6, (Member, IEEE), JINTONG HU1
, (Member, IEEE), CHONGYI LI 4
,GUSTAVO ROHDE 5,6, (Member, IEEE), YIXIANG DU1, AND KE HU1

Lecture 3: Image Restoration B14 Image Analysis Michaelmas 2014 A. Zisserman

Bringing Old Photos Back to Life
Ziyu Wan, Bo Zhang, Dongdong Chen, Pan Zhang, Dong Chen, Jing Liao, Fang Wen

python-demo
==============================

demo project

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
