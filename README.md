# Reconhecimento Facial com SVD

Projeto desenvolvido para a disciplina de **Álgebra Linear Computacional**, da Universidade Federal de Sergipe (Centro de Ciências Exatas e Tecnologia, Departamento de Matemática), com o objetivo de aplicar **Decomposição em Valores Singulares (SVD)** sobre um banco de fotos de rosto.

## Sobre o projeto

Uma imagem em tons de cinza pode ser representada como um vetor: cada posição do vetor guarda a intensidade de um pixel. O SVD encontra as direções (componentes principais) que melhor explicam como esses vetores variam entre si, permitindo:

- Representar cada foto usando muito menos números do que o total de pixels.
- Reconstruir uma foto aproximada a partir de poucas componentes.
- Usar essas coordenadas reduzidas como entrada para classificadores simples.

O notebook percorre essas ideias em etapas:

1. **Imagem média** — calcula o "rosto médio" do banco de fotos.
2. **Centralização + SVD** — subtrai a imagem média e decompõe o banco de dados em componentes principais.
3. **Reconstrução com poucas componentes** — reconstrói fotos usando só 5 componentes, ilustrando a ideia de compressão com perdas.
4. **Classificação de gênero** — treina um Perceptron sobre 2 e 3 componentes principais e compara a acurácia.
5. **Classificação de expressão (sorrindo/neutro)** — mesmo processo, usando 2 componentes.
6. **Reconstrução com muitas componentes** — projeta fotos próprias usando 400 componentes, mostrando a fidelidade da reconstrução quando se usa quase todas as dimensões disponíveis.

## Estrutura de pastas esperada

O notebook espera as imagens organizadas assim, na raiz do projeto:

```
imagens/
├── 1a.jpg, 1b.jpg, 2a.jpg, 2b.jpg, ...   # banco de fotos geral (par a/b por pessoa)
├── homens_mulheres/
│   └── 1a.jpg, 1b.jpg, ...               # subconjunto rotulado por gênero (homens primeiro, depois mulheres)
└── Minhas fotos/
    └── 1a.jpg, 1b.jpg                    # foto neutra (a) e sorrindo (b) usadas no passo final
```

> As imagens em si não estão neste repositório (dados pessoais/de terceiros). Substitua pelo seu próprio banco de fotos respeitando essa estrutura.

## Como rodar

```bash
pip install -r requirements.txt
jupyter notebook main.ipynb
```

**`requirements.txt`:**
```
numpy
pillow
matplotlib
scikit-learn
```

## Resultados e observações

- **Imagem média:** regiões que variam pouco entre as fotos (como os olhos) ficam nítidas na média; regiões mais variáveis (como a boca, por causa de expressões diferentes) ficam borradas.
- **Reconstrução com 5 componentes:** captura as variações mais fortes do banco de dados, mas perde detalhes finos de cada rosto — evidência direta da relação entre número de componentes e fidelidade da reconstrução.
- **Classificação de gênero:** com apenas 2 componentes o Perceptron tem pouca informação para separar as classes; com 3 componentes a separação melhora, mas ainda é uma fração pequena da variância total das imagens.
- **Classificação de sorriso:** a diferença entre boca aberta/fechada é uma das maiores fontes de variação nas fotos, então mesmo com 2 componentes o classificador separa bem os dois grupos.
- **Reconstrução com 400 componentes:** ao usar quase todas as componentes disponíveis, a reconstrução fica muito mais próxima da imagem original, confirmando o equilíbrio entre compressão e fidelidade.

## Possíveis melhorias futuras

- Testar outros classificadores (SVM, regressão logística) para comparar com o Perceptron.
- Avaliar a acurácia variando o número de componentes de forma sistemática (gráfico acurácia × nº de componentes).
- Validação cruzada em vez de um único split treino/validação.

## Créditos

Projeto acadêmico desenvolvido para a disciplina de Álgebra Linear Computacional (UFS), sob orientação do Prof. Evilson.
