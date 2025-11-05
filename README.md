# Sistema de Gerenciamento de Expedições

API RESTful desenvolvida em Flask para gerenciamento de expedições. Este projeto fornece endpoints para criar, listar, atualizar e deletar expedições, com armazenamento de dados em banco SQLite.

## 🚀 Tecnologias

- **Flask** 3.0.3 - Framework web Python
- **Flask-RESTful** 0.3.10 - Extensão para criação de APIs REST
- **SQLAlchemy** 2.0.30 - ORM para gerenciamento de banco de dados
- **Flask-CORS** - Suporte para Cross-Origin Resource Sharing
- **SQLite** - Banco de dados relacional

## 📋 Pré-requisitos

- Python 3.7 ou superior
- pip (gerenciador de pacotes Python)

## 🔧 Instalação

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/trabalhoFlask.git
cd trabalhoFlask
```

2. Crie um ambiente virtual (recomendado):

```bash
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate
```

3. Instale as dependências:

```bash
pip install -r requeriments.txt
```

## ▶️ Como executar

Execute o arquivo principal:

```bash
python app.py
```

A API estará disponível em `http://127.0.0.1:2000`

## 📚 Estrutura do Projeto

```
trabalhoFlask/
├── app/
│   ├── __init__.py          # Configuração do Flask e inicialização da aplicação
│   ├── models/
│   │   └── expedicoes.py    # Modelo de dados Expedicoes
│   └── view/
│       └── reso_expedicoes.py  # Recursos RESTful (endpoints)
├── app.py                   # Arquivo principal para executar a aplicação
├── requeriments.txt         # Dependências do projeto
└── README.md               # Este arquivo
```

## 🔌 Endpoints da API

### GET `/`

Retorna uma mensagem de boas-vindas.

**Resposta:**

```json
"Bem vindo à aplicação Flask"
```

### POST `/criar`

Cria uma nova expedição.

**Body (JSON):**

```json
{
  "nome": "Expedição Espacial X",
  "data": "2024-01-15",
  "destino": "Marte",
  "estado": "Planejada",
  "tripulacao": "João Silva, Maria Santos",
  "carga": "Equipamentos científicos",
  "duracao": "2024-06-15",
  "custo": 5000000,
  "status": "Ativa"
}
```

**Resposta:**

```json
{
  "message": "Expedição criada com sucesso!"
}
```

### GET `/expedicoes`

Lista todas as expedições ou busca uma expedição específica por ID.

**Query Parameters:**

- `id` (opcional): ID da expedição desejada

**Exemplo sem ID:**

```bash
GET /expedicoes
```

**Exemplo com ID:**

```bash
GET /expedicoes?id=1
```

**Resposta (lista completa):**

```json
[
  {
    "id": 1,
    "nome": "Expedição Espacial X",
    "data": "2024-01-15",
    "destino": "Marte",
    "estado": "Planejada",
    "tripulacao": "João Silva, Maria Santos",
    "carga": "Equipamentos científicos",
    "duracao": "2024-06-15",
    "custo": 5000000,
    "status": "Ativa"
  }
]
```

### PUT `/atualizar`

Atualiza uma expedição existente.

**Body (JSON):**

```json
{
  "id": 1,
  "nome": "Expedição Espacial X (Atualizada)",
  "data": "2024-01-20",
  "destino": "Marte",
  "estado": "Em andamento",
  "tripulacao": "João Silva, Maria Santos, Pedro Costa",
  "carga": "Equipamentos científicos e suprimentos",
  "duracao": "2024-07-15",
  "custo": 5500000,
  "status": "Ativa"
}
```

**Resposta:**

```json
{
  "message": "Expedição atualizada com sucesso!"
}
```

### DELETE `/deletar`

Deleta uma expedição.

**Body (JSON):**

```json
{
  "id": 1
}
```

**Resposta:**

```json
{
  "message": "Expedição deletada com sucesso!"
}
```

## 📊 Modelo de Dados

### Expedicoes

| Campo      | Tipo    | Descrição                                       |
| ---------- | ------- | ----------------------------------------------- |
| id         | Integer | ID único (chave primária, auto-incremento)      |
| nome       | String  | Nome da expedição                               |
| data       | Date    | Data da expedição (formato: YYYY-MM-DD)         |
| destino    | String  | Destino da expedição                            |
| estado     | String  | Estado atual da expedição                       |
| tripulacao | String  | Membros da tripulação                           |
| carga      | String  | Descrição da carga                              |
| duracao    | Date    | Data de duração/conclusão (formato: YYYY-MM-DD) |
| custo      | Integer | Custo da expedição                              |
| status     | String  | Status da expedição                             |

## 🗄️ Banco de Dados

O projeto utiliza SQLite como banco de dados. O arquivo `expedicoes.db` é criado automaticamente na primeira execução da aplicação.

## 🔒 CORS

O projeto está configurado com CORS habilitado, permitindo requisições de diferentes origens.

## 📝 Exemplos de Uso

### Criar uma expedição com cURL:

```bash
curl -X POST http://127.0.0.1:2000/criar \
  -H "Content-Type: application/json" \
  -d '{
    "nome": "Expedição Lua",
    "data": "2024-03-01",
    "destino": "Lua",
    "estado": "Planejada",
    "tripulacao": "Ana Costa",
    "carga": "Rover lunar",
    "duracao": "2024-03-15",
    "custo": 2000000,
    "status": "Ativa"
  }'
```

### Listar todas as expedições:

```bash
curl http://127.0.0.1:2000/expedicoes
```

### Buscar expedição por ID:

```bash
curl "http://127.0.0.1:2000/expedicoes?id=1"
```

### Atualizar uma expedição:

```bash
curl -X PUT http://127.0.0.1:2000/atualizar \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "nome": "Expedição Lua (Atualizada)",
    "data": "2024-03-05",
    "destino": "Lua",
    "estado": "Em andamento",
    "tripulacao": "Ana Costa, Carlos Mendes",
    "carga": "Rover lunar e equipamentos",
    "duracao": "2024-03-20",
    "custo": 2200000,
    "status": "Ativa"
  }'
```

### Deletar uma expedição:

```bash
curl -X DELETE http://127.0.0.1:2000/deletar \
  -H "Content-Type: application/json" \
  -d '{"id": 1}'
```

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para abrir uma issue ou enviar um pull request.

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 👥 Integrantes do Projeto

- [**Lucas da Silva Duarte**](https://github.com/lucasduartexyz/)

- [**Gabriel Mendes Rodrigues**](https://github.com/GabrielSteins/)

- [**Lara Stefanny Andrade da Silva**](https://github.com/Lara-AS)

- [**João Marcos Silva de Melo**](https://github.com/JOAOMARCOS405)
