# 🚀 Introdução ao FastAPI

## 📌 O que é FastAPI?

FastAPI é um **framework Python moderno** para criação de APIs rápidas, simples e com documentação automática.

### Exemplos de uso:

* Front-end → pede usuários → API responde
* App mobile → pede login → API responde

A comunicação acontece por **requisições HTTP**:

* **GET** → buscar dados
* **POST** → enviar dados
* **PUT** → atualizar dados
* **DELETE** → apagar dados

---

## 🛠️ Preparando o ambiente

### 1️⃣ Criar um ambiente virtual (opcional, mas recomendado)

No terminal (CMD ou PowerShell):

```bash
python -m venv venv
```

Ativar o ambiente virtual:

```bash
venv\Scripts\activate
```

---

### 2️⃣ Instalar FastAPI e o servidor

```bash
pip install fastapi uvicorn
```

* **FastAPI** → framework da API
* **Uvicorn** → servidor que roda a API

---

## 📄 Criando sua primeira API

Crie um arquivo chamado **`main.py`** e coloque o código abaixo:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"mensagem": "Minha primeira API FastAPI 🚀"}
```

### O que está acontecendo aqui?

* `FastAPI()` → cria a aplicação
* `@app.get("/")` → define uma rota GET na URL principal
* `return` → resposta em formato JSON

---

## ▶️ Rodando a API

No terminal, dentro da pasta do projeto:

```bash
uvicorn main:app --reload
```

Se aparecer algo como:

```text
Uvicorn running on http://127.0.0.1:8000
```

👉 Sua API está viva 🎉

Acesse no navegador:

```
http://127.0.0.1:8000
```

---

## 📚 Documentação automática

FastAPI cria a documentação automaticamente.

### Swagger (principal):

```
http://127.0.0.1:8000/docs
```

### Redoc (alternativa):

```
http://127.0.0.1:8000/redoc
```

---

## 🔗 Criando rotas de verdade

### 📥 Rota GET com parâmetro

```python
@app.get("/usuarios/{id}")
def buscar_usuario(id: int):
    return {"usuario_id": id}
```

Exemplo de acesso:

```
http://127.0.0.1:8000/usuarios/10
```

---

### 📤 Rota POST (enviar dados)

```python
from pydantic import BaseModel

class Usuario(BaseModel):
    nome: str
    idade: int

@app.post("/usuarios")
def criar_usuario(usuario: Usuario):
    return {
        "mensagem": "Usuário criado com sucesso",
        "dados": usuario
    }
```

---

## ✅ Como saber se o POST funcionou?

### 🥇 Testando pelo Swagger

1. Com a API rodando, acesse:

```
http://127.0.0.1:8000/docs
```

2. Encontre **POST /usuarios**
3. Clique em **Try it out**
4. No corpo (body), insira:

```json
{
  "nome": "Matheus",
  "idade": 19
}
```

5. Clique em **Execute**

### ✔️ Resultado esperado:

* **Status Code:** `200` ou `201`
* **Response body:**

```json
{
  "mensagem": "Usuário criado com sucesso",
  "dados": {
    "nome": "Matheus",
    "idade": 19
  }
}
```

Isso confirma que o **POST funcionou corretamente**.

---

## ⚠️ Importante

A FastAPI **só funciona se o terminal estiver aberto e rodando** o comando abaixo:

```bash
uvicorn main:app --reload
```

Se o terminal for fechado, a API para de funcionar.

---

## 🎯 Conclusão

Este projeto cobre:

* Conceito de API
* Criação de rotas GET e POST
* Uso do FastAPI
* Testes via Swagger

Ótimo ponto de partida para backend, QA e APIs modernas 🚀
