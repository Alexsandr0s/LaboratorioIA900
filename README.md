# LaboratorioIA900
Repositório para o projeto de previsão desenvolvido com Azure ML

Introdução
Este projeto tem como objetivo demonstrar o uso do Azure Machine Learning para criar um modelo de previsão baseado em aprendizado de máquina. A partir de um conjunto de dados fornecido pela Microsoft, utilizamos o serviço de Automated Machine Learning (AutoML) para treinar e implementar um modelo que prediz valores com base nos dados de entrada. O modelo é configurado com pontos de extremidade (endpoints), permitindo seu uso em aplicações externas para gerar previsões em tempo real.

Ferramentas Utilizadas
  * Azure Machine Learning Studio: Plataforma usada para treinar e implementar o modelo.
  * Automated Machine Learning (AutoML): Ferramenta que automatiza o processo de treinamento e seleção do melhor modelo.
  * Python: Linguagem usada para manipular dados e interagir com os endpoints.
  * Conjunto de Dados: [Bank Marketing Dataset.]([https://www.linkedin.com/in/thiago-valentim-correia-5331691b5/](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html))

Passo a Passo
Carregar os Dados

  * Acesse o link do conjunto de dados [Bank Marketing Dataset.]([https://www.linkedin.com/in/thiago-valentim-correia-5331691b5/](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html))
  * Faça o download do arquivo bank-marketing.csv.
    
Configurar o Workspace no Azure Machine Learning
  * Entre no Azure Machine Learning Studio.
  * Crie um novo workspace, se necessário.
  * Faça o upload do arquivo bank-marketing.csv para o workspace na seção Datasets.

    
Criar o Experimento AutoML
  * Vá até a seção Automated ML e inicie um novo experimento.
  * Escolha o dataset bank-marketing.csv como fonte de dados.
  * Configure o campo de previsão: deposit (sim/não).
  * Selecione a métrica de avaliação, como AUC_weighted.
  * Inicie o treinamento do AutoML.
  * 
Implantar o Modelo (Deploy)
  * Após o treinamento, selecione o melhor modelo identificado pelo AutoML.
  * Clique em Deploy para criar um ponto de extremidade.
  * Configure o tipo de serviço como Azure Container Instance (ACI).
  * Aguarde a conclusão da implantação e anote o Endpoint URL gerado.

Salvar os Dados do Endpoint
  * Copie os detalhes do endpoint, incluindo a URL e a chave de autenticação.
  * Salve essas informações em um arquivo JSON no seguinte formato:
    
    {
  "endpoint": "https://<seu-endpoint>.azurewebsites.net/score",
  "key": "sua-chave-de-autenticacao"
}

Como Testar
Instale as Dependências
Certifique-se de ter o Python instalado e execute:

pip install requests

Envie uma Requisição para o Endpoint
Crie um arquivo Python com o seguinte código para testar o modelo:

import requests

# Configurações do endpoint
url = "https://<seu-endpoint>.azurewebsites.net/score"
headers = {"Content-Type": "application/json", "Authorization": "Bearer sua-chave-de-autenticacao"}

# Dados de exemplo para teste
data = {
    "age": 35,
    "job": "management",
    "marital": "married",
    "education": "tertiary",
    "default": "no",
    "balance": 1200,
    "housing": "yes",
    "loan": "no",
    "contact": "cellular",
    "day": 5,
    "month": "may",
    "duration": 250,
    "campaign": 1,
    "pdays": -1,
    "previous": 0,
    "poutcome": "unknown"
}

# Enviando a requisição
response = requests.post(url, headers=headers, json=data)

# Exibindo o resultado
print(f"Resposta do modelo: {response.json()}")

Validar a Resposta
O modelo deve retornar uma previsão indicando se o cliente irá ou não realizar o depósito.









