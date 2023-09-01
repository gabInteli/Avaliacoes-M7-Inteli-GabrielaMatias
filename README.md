# Avaliacoes-M7-Inteli
Avaliações do Módulo 7

Para executar o backend:

```bash
python main.py
```

Para executar o frontend:

```bash
node server.js
```

Foi desenvolvido um Dockerfile para cada camada da aplicação, sendo: 

### Frontend

FROM node:18.16.1

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000
CMD [ "node", "server.js" ]

Onde indicamos a imagem a ser utilizada `node`, a rota das dependencias do arquivo com `package.json` e a instalação das dependências, e por fim, o comando e a porta para iniciar o servidor da interface. 


### Backend 

FROM python:3.9

WORKDIR /code

COPY ./requirements.txt /code/requirements.txt

RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

COPY . /code

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

Onde indicamos a imagem a ser utilizada `python`, a rota das dependencias do arquivo com `requirements.txt` e a instalação das dependências, e por fim, o comando e a porta para iniciar o servidor do sistema de backend.

### Docker Compose

Por fim, temos nosso arquivo de compose que inicia o serviço das imagens desenvolvidas por cada um dos dockerfiles. De modo que, podemos acionar todos os serviços de forma unitária com base nas imagens criadas: 

#### Imagem Frontend: 
https://hub.docker.com/repository/docker/gabinteli/frontend-p1/general
#### Imagem Backend: 
https://hub.docker.com/repository/docker/gabinteli/backend-p1/general
 

Para acionar todos os serviços basta rodar um docker compose, e a seguir temos o passo a passo da criação de um novo usuário: 

 ![Imagem 1](imagem)