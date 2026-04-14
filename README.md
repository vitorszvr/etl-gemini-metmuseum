# Desafio ETL - Arte & IA (MetMuseum + Google Gemini)

Este projeto consiste em um mini-pipeline de ETL (Extração, Transformação e Carga) desenvolvido em Python no Jupyter Notebook. Ele utiliza a API pública do **Metropolitan Museum of Art (The Met)** em conjunto com a Inteligência Artificial do **Google Gemini** para descrever automaticamente dados sobre obras de arte.

## 🚀 Como funciona o Pipeline (ETL)

1. **Extract (Extração):** O projeto se conecta à Collection API do The Met (`https://collectionapi.metmuseum.org/public/collection/v1/`) para buscar uma lista de IDs das obras em catálogo. A partir dessa lista, escolhe uma obra aleatória e obtém o link da imagem original (`primaryImage`).
2. **Transform (Transformação):** A imagem obtida na fase anterior é baixada em memória e enviada para o modelo de visão da API do Google Gemini (utilizando o modelo `gemini-3-flash-preview` via pacote `google-genai`). A Inteligência Artificial então descreve a obra de arte a partir da instrução: *"O que você vê nessa imagem?"*.
3. **Load (Carga):** As informações consolidadas (ID da obra no museu, o link da imagem e a descrição gerada pelo modelo) são transformadas em um dicionário de dados e inseridas/anexadas em um banco de dados local com formato JSON (`data.json`).

## 🛠️ Tecnologias Utilizadas

- **Python** e **Jupyter Notebook** (`main.ipynb`)
- **Requests:** Para realização de requisições HTTP e consumo da API do museu.
- **Google GenAI SDK:** Biblioteca do Google (`google-genai`) para interagir com a inteligência artificial Gemini e processar as imagens das obras.

## ⚙️ Como rodar o projeto localmente

Para rodar este script, siga os passos:

1. **Prepare o ambiente virtual e dependências:**
   O ambiente virtual `.venv` já está na estrutura do projeto. Certifique-se de ativá-lo e de que os pacotes necessários estão instalados.
   As dependências podem ser instaladas diretamente pela primeira célula do notebook ou no terminal:
   ```bash
   pip install requests google-genai
   ```

2. **Gere a sua API Key do Google Gemini:**
   Este projeto exige uma chave do Google Gemini para realizar a etapa de `Transform`.
   Crie um arquivo chamado `config.py` na raiz do projeto e crie uma variável apontando ou contendo a sua string da chave de API:
   ```python
   GEMINI_API_KEY = 'SUA_CHAVE_AQUI'
   ```

3. **Execute o arquivo principal:**
   - Entre no arquivo `main.ipynb` e execute as células sequencialmente. 
   - Ao rodar a última célula adequadamente, o arquivo `data.json` deverá ser criado e/ou atualizado com a obra aleatória escolhida na etapa de Extração!
