# Como executar os notebooks do trabalho

Este guia explica como abrir e rodar os notebooks deste trabalho, do zero, num computador que ainda não tem nada configurado.

## Sobre o trabalho

Estes notebooks são a resolução do *Trabalho de Cálculo II: Modelagem Computacional* (UFAM, Engenharia de Software). O enunciado completo está no PDF desta pasta.

Cada questão do trabalho está num **notebook separado**. Em todos eles, cada item segue a mesma estrutura:

- **Análise na mão ✍️** (células de texto): a resolução matemática, explicada passo a passo;
- **Código 💻** (células de código): os gráficos, os controles interativos e a conferência numérica dos resultados.

## Arquivos da pasta

| Arquivo | Conteúdo | Situação |
|---|---|---|
| `questao1.ipynb` | Questão 1: Domínio, imagem e curvas de nível | ✅ pronto |
| `questao2.ipynb` | Questão 2: Limites e continuidade | 🚧 em desenvolvimento |
| `questao3.ipynb` | Questão 3: Derivadas parciais, diferenciabilidade e continuidade | ✅ implementado e verificado localmente |
| `questao4.ipynb` | Questão 4: Plano tangente e reta normal | ✅ implementado e verificado localmente |
| `requirements.txt` | lista das bibliotecas Python usadas por todos os notebooks | |
| `COMO_EXECUTAR.md` | este guia | |
| `Trabalho_Calculo_II_...pdf` | o enunciado do trabalho | |

## Passo 1: instalar o Python

É preciso ter o **Python 3.10 ou mais recente**. A Questão 1 foi originalmente testada com Python 3.10.12; as Questões 3 e 4 foram executadas e verificadas localmente com Python 3.14.4.

Para conferir se já está instalado, abra um terminal (no Windows, o "Prompt de Comando" ou o "PowerShell") e digite:

```bash
python3 --version     # Linux / macOS
python --version      # Windows
```

Se aparecer algo como `Python 3.10.12`, está tudo certo. Se der erro ou a versão for menor que 3.10, baixe o Python em <https://www.python.org/downloads/>. No Windows, marque a opção **"Add Python to PATH"** durante a instalação.

> Nos comandos abaixo, use `python3` no Linux e no macOS e `python` no Windows.

## Passo 2: instalar as bibliotecas

Este passo é feito **uma vez só** e vale para todos os notebooks.

No terminal, entre na pasta do projeto (a que contém os arquivos `.ipynb`) e instale as bibliotecas listadas no `requirements.txt`.

**Opção recomendada: ambiente virtual.** As bibliotecas ficam isoladas nesta pasta e não interferem no resto do computador.

```bash
# Linux / macOS
cd "caminho/para/a/pasta"
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

```powershell
# Windows (PowerShell)
cd "caminho\para\a\pasta"
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

**Opção simples: sem ambiente virtual.**

```bash
python3 -m pip install --user -r requirements.txt
```

O que cada biblioteca faz:

| Biblioteca | Uso |
|---|---|
| `numpy` | contas numéricas e grades de pontos no plano |
| `matplotlib` | gráficos 2D |
| `plotly` + `nbformat` | gráficos 3D giráveis e sliders |
| `ipywidgets` | caixas de texto, botões e outros controles interativos |
| `sympy` | cálculo simbólico e exato (sem erro de arredondamento) |
| `ipykernel` | permite que o editor rode o código Python dos notebooks |

> Se uma questão nova passar a usar outra biblioteca, ela será acrescentada ao `requirements.txt`. Depois de atualizar os arquivos, rode o `pip install -r requirements.txt` de novo.

## Passo 3: abrir um notebook

Escolha **uma** das duas formas.

### Forma A: VS Code (recomendada)

1. Instale o **VS Code**: <https://code.visualstudio.com/>
2. No VS Code, abra a aba de extensões (`Ctrl+Shift+X`) e instale as extensões **Python** e **Jupyter**, ambas da Microsoft.
3. Abra a pasta do projeto (`Arquivo > Abrir Pasta...`) e clique no notebook da questão desejada, por exemplo `questao1.ipynb`.
4. No canto superior direito do notebook, clique em **"Select Kernel"** (ou no nome do Python que aparecer ali) e escolha o Python onde as bibliotecas foram instaladas:
   - se usou o ambiente virtual, escolha o que aparece como **`.venv`**;
   - senão, escolha o Python 3.10 ou mais recente do sistema.

   Essa escolha precisa ser feita uma vez em cada notebook.

### Forma B: Jupyter no navegador

Instale o Jupyter e abra o notebook pelo terminal, na pasta do projeto e com o ambiente virtual ativado, se estiver usando um:

```bash
pip install notebook
jupyter notebook questao1.ipynb      # troque pelo notebook da questão desejada
```

O navegador abre o notebook automaticamente. Para abrir outro, use a lista de arquivos que aparece na aba inicial do Jupyter.

## Passo 4: executar

**Rode as células de cima para baixo, em ordem.** Dentro de cada notebook, as células dependem umas das outras: a primeira célula de código carrega as bibliotecas e as funções auxiliares, e os itens seguintes usam variáveis criadas nos anteriores.

O jeito mais fácil é executar tudo de uma vez:

- **VS Code:** botão **"Run All"** (ou "Executar Tudo") na barra do topo do notebook;
- **Jupyter:** menu `Run > Run All Cells` (ou `Cell > Run All`).

Os notebooks são **independentes entre si**: não é preciso rodar a Questão 1 antes da Questão 2, por exemplo. Cada um tem a própria configuração.

> Se rodar uma célula isolada e aparecer `NameError: name '...' is not defined`, é porque alguma célula anterior não foi executada. Rode tudo desde o início.

## Como usar os controles interativos

Estes controles aparecem em vários notebooks:

**Gráficos 3D (Plotly)**
- arrastar com o mouse: gira o gráfico;
- rolar a roda do mouse: zoom;
- passar o mouse sobre o gráfico: mostra as coordenadas;
- clicar num item da legenda: esconde ou mostra aquele elemento.

**Sliders (Plotly)**
- arraste o controle abaixo do gráfico para mudar o parâmetro;
- o título do gráfico explica o resultado para o valor escolhido.

**Caixas de texto e botões (ipywidgets)**
- digite os valores e clique no botão para ver o resultado;
- quando houver uma lista de **Exemplos**, escolher um caso preenche as caixas e mostra o resultado automaticamente.

## Guia de cada questão

### Questão 1: Domínio, imagem e curvas de nível (`questao1.ipynb`)

Estuda três funções de duas variáveis:

- f₁(x,y) = √(9 − x² − y²)
- f₂(x,y) = ln(4 − x² − y²)
- f₃(x,y) = 1/(x² + y² − 1)

| Seção do notebook | O que faz |
|---|---|
| Item 1: Domínio e fronteira | desenha o domínio de cada função no plano xy, com a fronteira cheia (incluída) ou tracejada (excluída) |
| Item 2: Imagem e superfície 3D | calcula a imagem e mostra a superfície em 3D |
| Itens 3 e 5: Curvas de nível | um slider para variar o nível c, mostrando à esquerda a superfície cortada pelo plano z = c e à direita a curva no plano xy; explica por que alguns valores de c não geram curva |
| Item 4: Verificar um ponto | o usuário digita um ponto (a, b) e o programa diz se ele pertence ao domínio de cada função e, se não pertencer, qual condição falhou |

**Detalhes de uso:**
- **Sliders (itens 3 e 5):** são as células mais demoradas, porque calculam as curvas para todos os valores de c antecipadamente. Mesmo assim, o notebook inteiro roda em poucos segundos.
- **Verificador de pontos (item 4):** aceita valores como `3`, `-1.5`, `1,5`, `1/2`, `sqrt(5)`, `√5`, `2*sqrt(2)` e `pi`. As contas são exatas (via `sympy`), então pontos exatamente na fronteira, como (√5, 2), são classificados corretamente.

### Questão 2: Limites e continuidade (`questao2.ipynb`)

🚧 Em desenvolvimento.

### Questão 3: Derivadas parciais, diferenciabilidade e continuidade (`questao3.ipynb`)

Compara f(x,y) = xy/√(x²+y²) e g(x,y) = xy/(x²+y²), ambas com valor zero na origem.

| Item | Conteúdo |
|---|---|
| 1 | Derivadas parciais na origem pela definição e tabela de incrementos positivos e negativos |
| 2 | Superfícies e cortes pelos eixos; diagonal como contraste |
| 3 | Aplicação linear candidata L(h,k)=0 |
| 4 | Comparador de trajetórias, valores e quocientes de erro |
| 5 | Demonstrações de continuidade, contraexemplos e relações lógicas |

No comparador, escolha a trajetória e o lado do parâmetro. O controle **m** só atua na reta y=m x. O controle **p** marca o ponto com |t|=10⁻ᵖ; os gráficos de valores e erros mostram a sequência de aproximação completa. Arraste os gráficos 3D para girar.

A pequena região omitida da malha de g é um recurso de renderização; não é uma exclusão do domínio. O ponto na origem aparece separadamente.

Conclusões na origem: ambas têm parciais zero; f é contínua e g não é; nenhuma é diferenciável. A célula de conferências deve terminar com **OK**.

### Questão 4: Plano tangente e reta normal (`questao4.ipynb`)

Estuda o paraboloide x²+y², o cone √(x²+y²) e a função xy/√(x²+y²), definida como zero na origem.

| Item | Conteúdo |
|---|---|
| 1 | Seleção de função e ponto, com o ponto correspondente na superfície |
| 2 | Plano tangente e reta normal somente nos pontos diferenciáveis |
| 3 | Vetores T_x e T_y e normal pelo produto vetorial |
| 4 | Comparação da origem com pontos regulares e explicação das falhas |
| 5 | Zoom local, erro absoluto e erro dividido pela distância |

**Visualizador:** selecione a função, digite a e b entre −5 e 5 e clique em **Atualizar**. Os exemplos aplicam a mudança imediatamente. O zoom usa uma vizinhança de lado horizontal 10⁻ᵖ em cada direção. As caixas **Plano**, **Reta normal** e **Vetores** controlam as camadas. As setas preservam direções, com comprimento ajustado para caber no zoom; os vetores originais aparecem no texto.

Na origem do cone e da terceira função, plano e reta normal via diferencial ficam indisponíveis. Na terceira função, as setas que permanecem são apenas tangentes dos cortes coordenados. Em pontos regulares, os três modelos têm plano e normal.

**Comparador de erros:** possui seus próprios campos de função e ponto; clique em **Comparar erros**. Os gráficos estáticos acima dele também permanecem salvos. Quando o ponto não é diferenciável, z=0 é apenas uma referência diagnóstica, não um plano tangente. A célula de conferências deve terminar com **OK**.

### Material de apoio e organização das entregas

Os notebooks 3 e 4 continuam **individuais e independentes**, sem junção com as demais questões. O resumo matemático, imagens estáticas com legendas e roteiro oral estão em [apoio_relatorio/README.md](apoio_relatorio/README.md). Esse material serve ao integrante que escreve o relatório; não é um relatório final unificado.

Use o kernel do ambiente em que instalou `requirements.txt` (neste computador, `.venv`). Os resultados salvos podem ser lidos sem executar tudo, mas os controles precisam de kernel ativo. Não houve adição de dependências às sete bibliotecas previstas no projeto.

## Problemas comuns

| Problema | Solução |
|---|---|
| `ModuleNotFoundError: No module named '...'` | a biblioteca não está instalada no Python que o notebook está usando. Confira o kernel escolhido (Passo 3) e rode o `pip install -r requirements.txt` com esse mesmo Python. Depois **reinicie o kernel**. |
| Instalei uma biblioteca, mas o erro continua | reinicie o kernel: botão **"Restart"** na barra do notebook. O kernel só enxerga bibliotecas instaladas antes de ele iniciar. |
| Os gráficos 3D ou os sliders aparecem em branco | confira se `plotly` e `nbformat` estão instalados e reinicie o kernel. No VS Code, confira se a extensão **Jupyter** está instalada e atualizada. |
| As caixas de texto e os botões não aparecem (só um texto como `VBox(...)`) | o `ipywidgets` não está instalado no kernel ou o editor não carregou os widgets. Instale, reinicie o kernel e rode tudo de novo. |
| Resultados repetidos ou estranhos depois de muitas execuções | reinicie o kernel e use **"Run All"** para rodar o notebook do zero. |
| `NameError: name '...' is not defined` | alguma célula anterior não foi executada. Rode o notebook desde o início, em ordem. |
| O terminal não reconhece o comando `python3` (Windows) | no Windows use `python` em vez de `python3`. Se nenhum dos dois funcionar, reinstale o Python marcando **"Add Python to PATH"**. |
