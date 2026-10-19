<img src="Cabeçalho - Ilum.png" width="100%"/>

# Tiamat - Aprendizado de Máquina
Trabalho final da disciplina de Aprendizado de Máquina (ATP-203), ministrada pelo professor Dr. Daniel Roberto Cassar.
<br> Ilum Escola de Ciência (CNPEM)

**Aluno**: Caio Guimarães Marino - T26
<br> Este repositório de Aprendizado de Máquina contém a captura da criatura lendária Tiamat, do Reino de Lumi.

## **Objetivo**
*Escolher um conjunto de dados, comparar o desempenho de pelo menos 3 algoritmos/pipelines de aprendizado de máquina (sem contar o baseline) e testar pelo menos 100 conjuntos de hiperparâmetros diferentes para cada um deles, utilizando o `optuna`.*

O objetivo deste trabalho é prever a temperatura crítica de materiais supercondutores (a temperatura abaixo da qual o material conduz corrente elétrica sem resistência) a partir da sua composição química. Trata-se de um problema de regressão em dados tabulares, com $81$ atributos numéricos e um target (`critical_temp`, em kelvin).

Foram comparados 5 algoritmos/pipelines de aprendizado de máquina, cada um com pelo menos $100$ conjuntos de hiperparâmetros avaliados com o optuna, e um modelo baseline que prevê sempre a média do treino. Os modelos treinados neste trabalho foram:
1. KNN com normalização e PCA;
2. Árvore de decisão;
3. Floresta aleatória;
4. Regressão linear com normalização, PCA e termos polinomiais;
5. Regressão linear com normalização, seleção de atributos (RFE) e termos polinomiais.

Como materiais de uma mesma família química são muito parecidos entre si, uma divisão aleatória em trein oe teste causaria vazamento de dados. Por isso, os materiais foram agrupados com `KMeans` e a divisão treino/teste (`GroupShuffleSplit`) e a validação cruzada (`GroupKFold`) foram feitas de acordo com esses grupos. O conjunto de teste foi usado uma única vez para cada algoritmo/pipeline, depois da otimização. Por fim, o melhor modelo foi interpretado com a importância por permutação (`permutation importance`).

Os resultados e a discussão completa dos mesmos se encontram no notebook presente neste repositório.

### **Guia de arquivos no repositório**
Neste repositório, o arquivo `Tiamat.ipynb` é o notebook Jupyter com todo o desenvolvimento do trabalho (análise exploratória, modelagem, resultados, conclusões, uso de IA e referências). <br> `train.csv` é o conjunto de dados utilizado (arquivo principal do *Superconductivity Data*). <br> Os arquivos database (`.db`) referem-se ao histórico de todas as tentativas de cada otimização. Eles foram incluídos no repositório para que o notebook possa ser executado de cima para baixo sem refazer as otimizações (e sem alterar os resultados), onde ao encontrar um estudo já completo, o notebook apenas o carrega.

### **Sobre o dataset**
O Superconductivity Data reúne $21263$ materiais supercondutores descritos por $81$ atributos extraídos da composição química (estatísticas de $8$ propriedades atômicas dos elementos do material, além do número de elementos) e pela temperatura crítica. Após remover $66$ linhas duplicadas, restaram $21197$ materiais. Foi utilizado apenas o arquivo principal (train.csv).
<br> Fonte original: Hamidieh, K. (2018). **Superconductivty Data [Dataset].** UCI Machine Learning Repository. https://doi.org/10.24432/C53P47 (https://archive.ics.uci.edu/dataset/464/superconductivty+data).

### **Uso de IA**
Este trabalho contou com o apoio de ferramentas de IA (Claude, da Anthropic, e respostas do Gemini, do Google) em diferentes etapas do processo. Detalhes completos estão descritos na seção "Descrição do uso de IA neste trabalho", dentro do notebook, com o link da conversa.
