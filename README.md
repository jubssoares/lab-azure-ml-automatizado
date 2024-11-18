<h1>Trabalhando com Machine Learning na Prática no Azure ML</h1>

<img align="right" height="200" style="border-radius:50px;" src="https://assets.dio.me/arZ5ZUZHMQWT8l4NCDy489M0KFa99ywo3ZJ5-N3wmE8/f:webp/h:120/q:80/L3RyYWNrcy8xODIzYThhMS1lZjk2LTQ4MmYtODI1Ny0yNmRkNjFiNDJiYTMucG5n">

<h3>Repositório criado para o desafio do bootcamp Microsoft - Fundamentos de IA</h3>

<h4 align="justify">Descrição do projeto</h4>

<p align="justify">
    Este projeto demonstra o processo de criação de um modelo de previsão usando o Azure Machine Learning Automated ML e a configuração de pontos de extremidade para inferências em tempo real. O repositório inclui o arquivo `README.md` com o passo a passo e o arquivo `.json` contendo as informações do ponto de extremidade configurado.
</p>


## **Passo a Passo**

### **1. Configuração Inicial**
1. Acesse o **Azure Machine Learning Studio** [aqui](https://ml.azure.com).
2. Certifique-se de ter um Workspace configurado e um **Compute Cluster** disponível para execução dos experimentos.
3. Faça upload do dataset necessário no Azure ML:
   - Navegue até **Datasets** > **Create Dataset** > **From local files** e envie o arquivo.
   - Certifique-se de que os dados estão no formato correto e que a coluna de destino (target) está definida.

---

### **2. Criar um Experimento com AutoML**
1. No menu lateral, selecione **Automated ML** e clique em **New Automated ML Run**.
2. Configure o experimento:
   - **Dataset**: Escolha o dataset carregado na etapa anterior.
   - **Target Column**: Defina a variável que será prevista.
   - **Task Type**: Escolha entre `Regression`, `Classification` ou `Forecasting`, dependendo do caso.
3. Configure o cluster de computação e o tempo máximo de execução para o treinamento.

---

### **3. Selecionar o Melhor Modelo**
1. Após a conclusão do experimento, vá até a aba **Models** dentro do experimento.
2. Escolha o modelo com o melhor desempenho (com base em métricas como AUC, R^2, ou outra métrica relevante).
3. Clique em **Register Model** para salvar o modelo no workspace.

---

### **4. Configurar o Ponto de Extremidade**
1. Após registrar o modelo, vá até a aba **Models** do Azure ML Studio.
2. Clique em **Deploy** e configure o ponto de extremidade:
   - **Deployment type**: Escolha entre **Azure Kubernetes Service (AKS)** ou **Azure Container Instance (ACI)**.
   - Defina um nome para o endpoint e ajuste as configurações de recursos conforme necessário.
3. Finalize a implantação e aguarde até que o ponto de extremidade esteja ativo.

---

### **5. Realizar Inferências**
Utilize a URL e a chave do endpoint para enviar dados e obter previsões. Aqui está um exemplo em Python:

```python
import json
import requests

# URL e chave do endpoint
url = "<sua_url_do_endpoint>"
api_key = "<sua_chave_de_acesso>"

# Dados de exemplo para predição
data = {
    "data": [
        {"coluna1": valor1, "coluna2": valor2, "coluna3": valor3}
    ]
}

# Cabeçalhos
headers = {
    "Content-Type": "application/json",
    "Authorization": f"Bearer {api_key}"
}

# Enviar requisição
response = requests.post(url, headers=headers, data=json.dumps(data))

# Exibir resultado
print(response.json())
