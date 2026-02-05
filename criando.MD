Fast API

Exemplo:

Front-end → pede usuários → API responde

App mobile → pede login → API responde
A comunicação acontece por requisições HTTP:
GET → buscar dados

POST → enviar dados

PUT → atualizar

DELETE → apagar

1️⃣ Criar um ambiente virtual (opcional, mas recomendado)

No terminal (CMD ou PowerShell):

python -m venv venv

Ativar:

venv\Scripts\activate

2️⃣ Instalar FastAPI e servidor
pip install fastapi uvicorn


FastAPI → framework

Uvicorn → servidor que roda a API

Aula 4 – Criando sua primeira API 
Crie um arquivo chamado:

main.py

Coloque isso dentro 👇

from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"mensagem": "Minha primeira API FastAPI 🚀"}

O que está acontecendo aqui?

FastAPI() → cria a aplicação

@app.get("/") → rota GET na URL principal

return → resposta em JSON



Rodando a API

No terminal, dentro da pasta do projeto:
uvicorn main:app --reload

Se aparecer algo como:

Uvicorn running on http://127.0.0.1:8000

Sua API está viva

Acesse no navegador:

http://127.0.0.1:8000


Documentação automática
FastAPI cria docs sozinho.

Swagger (principal):

http://127.0.0.1:8000/docs

Redoc (alternativa):

http://127.0.0.1:8000/redoc

Criando rotas de verdade

Rota GET com parâmetro
@app.get("/usuarios/{id}")
def buscar_usuario(id: int):
    return {"usuario_id": id}
Exemplo de acesso:

http://127.0.0.1:8000/usuarios/10

Rota POST (enviar dados)

from pydantic import BaseModel

class Usuario(BaseModel):
    nome: str
    idade: int

@app.post("/usuarios")
def criar_usuario(usuario: Usuario):
    return {
        "mensagem": "Usuário criado",
        "dados": usuario
    }

Como saber se o post funcinou?
Jeito 1 – Pelo Swagger
Com a API rodando, abra:

http://127.0.0.1:8000/docs
Encontre:

POST /usuarios

Clique em Try it out
No corpo (body), coloque:
{
  "nome": "Matheus",
  "idade": 19
}

Clique em Execute

Se deu code 200 ou 201 e pq deu certo

no body vai aparecer 
{
  "mensagem": "Usuário criado com sucesso",
  "dados": {
    "nome": "Matheus",
    "idade": 19
  }
}

Isso CONFIRMA que o POST funcionou.

Se NÃO RODAR
Passo 1 – Olha o TERMINAL (isso é obrigatório)

A FastAPI só funciona se o terminal estiver aberto e rodando.

Você PRECISA ter algo assim aberto:

uvicorn main:app --reload
