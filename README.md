# Grudes Web Client

 Projeto de avaliação da sprint "Qualidade de Software, Segurança e Sistemas Inteligentes" do curso de Pós-graduação da PUC-Rio em Engenharia de Software.

---
## Download do repo
 ### Para inicializar corretamente os submódulos, clone usando o comando a seguir:
```sh
git clone --recurse-submodules https://github.com/hugocm93/grudes.git
```
 ### Ou se o clone já foi feito sem o parâmetro:
```sh
git submodule update --init
```

---
## Requisitos 
 * Sistema Operacional Unix.
 * Docker Compose >= 2.5.0 instalado.
 * Git >= 2.13 instalado.
 * Permissão de execução do docker como superusuário.

---
## Execução
 Na raiz deste repositório, executar:
```sh
sudo docker compose up --build 
```
 Ou para modo desenvolvimento:
```sh
sudo docker compose -f docker-compose.yml -f dev.yml up --build 
```
 Abra o navegador no endereço http://localhost:3000/ para entrar no site.

---
## Documentação
 O site apresenta um menu lateral com 4 itens de Menu: Busca, Receitas, Ingredientes e Explorar.
 * Busca: É possível buscar receita por nome ou por ingredientes (ou substitutos). Ao buscar sem informar nome nem ingrediente, todas as receitas são retornadas. Para buscar por nome, basta informar o nome na caixa de texto e apertar o botão de lupa. Para buscar por ingrediente, clicar no botão de + e digitar o nome do ingrediente. A busca é sensível a caixa e busca palavras exatas. Para visualizar uma receita dentre as receitas encontradas, basta clicar em cima do nome dela na lista de receitas. É possível remover a receita diretamente da área de busca, clicando no botão - ao lado da receita.
 * Receitas: Área de cadastro de novas receitas e edição de receitas já cadastradas. Para cadastrar uma nova receita, preencher o formulário e clicar no botão cadastrar. Para editar uma receita, selecioná-la na lista, alterar os campos e clicar em Cadastrar.
 * Ingredientes: Área de cadastro de ingredientes e ingredientes substitutos. Para cadastrar um novo ingrediente, preencher o formulário e clicar em Cadastrar. Para editar um ingrediente, selecionar um ingrediente da lista, alterar os campos e clicar em Cadastrar.
 * Explorar: Área de busca de novas receitas na internet. Nesta área, a busca é efetuada em provedor de receitas. A busca pode ser feita por nome ou por ingrediente principal. Ao encontrar uma receita desejada, é possível salvá-la na sua lista de receitas pessoais clicando no botão Salvar.
 * **Predição de origem gastronômica**: esta funcionalidade utiliza um sistema inteligente para inferir a gastronomia de uma receita baseada na sua lista de ingredientes. Para verificar a predição, basta buscar uma receita tanto pela aba Busca quanto pela aba Explorar. A gastronomia será informada abaixo do título.

---
## Sistema inteligente
 O sistema inteligente desenvolvido utiliza um modelo de _machine learning_ (ML) supervisionado para fazer predições (classificação) sobre a origem gastronômica de uma receita baseadas em seus ingredientes. 
 O _data set_ utilizado foi o [Recipe Ingredients Dataset](https://www.kaggle.com/datasets/kaggle/recipe-ingredients-dataset/data?select=train.json) obtido do site [Kaggle](https://www.kaggle.com).
 Para informação de como usar a funcionalidade, leia a parte de Documentação acima.

 ### Notebook 
  Foi utilizado um notebook do Google Colab para a criação do modelo de ML que está localizado em ./RecipeOriginClassifier.ipynb.

 ### Testes automatizados
  Testam o modelo de ML quanto aos requisitos de desempenho desejado para o projeto. 
  Para executá-los:
```sh
sudo docker compose -f test.yml up --build
```

---
## Serviços utilizados:
 * [Grudes API](https://github.com/hugocm93/grudes_api) para gerenciamento da lista de receitas pessoais. Foi implementada por mim para o curso de Pós-graduação da PUC-Rio em Engenharia de Software.
 * [Grudes Web Client](https://github.com/hugocm93/grudes_web_client) como front-end. Foi implementada por mim para o curso de Pós-graduação da PUC-Rio em Engenharia de Software.
 * [TheMealBD](https://www.themealdb.com/api.php) para procurar novas receitas. Esta API é gratuita para fins educacionais. Nenhuma autenticação é necessária pois só foram usadas rotas presentes na versão gratuita. Rotas utilizadas: www.themealdb.com/api/json/v1/1/search.php, www.themealdb.com/api/json/v1/1/lookup.php, www.themealdb.com/api/json/v1/1/filter.php.
