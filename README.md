# 🚗 Sistema de Aluguel de Carros

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-4.1-green.svg)](https://www.djangoproject.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-12+-blue.svg)](https://www.postgresql.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Sistema completo de gerenciamento de locação de veículos desenvolvido em Django, com interface administrativa customizada e controle de disponibilidade em tempo real.

## 📋 Sobre o Projeto

Sistema web para gerenciar locações de veículos com controle automático de disponibilidade, registro de clientes e histórico completo de locações. O sistema utiliza o Django Admin Interface customizado para proporcionar uma experiência de usuário moderna e intuitiva.

### 🎯 Funcionalidades Principais

- ✅ **Gestão de Veículos**
  - Cadastro completo de carros (marca, modelo, placa, chassi, renavam)
  - Controle automático de status (Livre/Ocupado)
  - Registro de características (ano, cor, portas, combustível, hodômetro)
  - Validação de unicidade (placa, chassi, renavam)

- ✅ **Gestão de Clientes**
  - Cadastro de clientes (pessoa física ou jurídica)
  - Registro de CPF/CNPJ, endereço e telefone
  - Histórico de locações por cliente

- ✅ **Gestão de Locações**
  - Registro de data de retirada e previsão de entrega
  - Controle de status (Pago/Aberto/Cancelado)
  - Validação automática de disponibilidade
  - Registro de CNH e intenção de uso
  - Atualização automática do status do veículo

- ✅ **Interface Administrativa**
  - Django Admin Interface customizado com tema moderno
  - Busca e filtros avançados
  - Autocomplete para seleção de clientes e carros
  - Visualização organizada de dados

## 🏗️ Arquitetura do Sistema

### Modelos de Dados

```
┌─────────────┐
│   Marca     │
└──────┬──────┘
       │
       ▼
┌─────────────┐     ┌─────────────┐
│   Modelo    │◄────┤   Carro     │
└─────────────┘     └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │   Locacao   │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │   Cliente   │
                    └─────────────┘
```

### Estrutura do Projeto

```
aluguel_carros-main/
├── aluguel_carros/          # Configurações do projeto Django
│   ├── __init__.py
│   ├── asgi.py
│   ├── backends.py          # Backends customizados
│   ├── settings.py          # Configurações principais
│   ├── urls.py              # Rotas do projeto
│   └── wsgi.py
├── Carros/                  # App de gerenciamento de carros
│   ├── models.py            # Modelos: Marca, Modelo, Carro
│   ├── admin.py
│   ├── views.py
│   └── migrations/
├── Clientes/                # App de gerenciamento de clientes
│   ├── models.py            # Modelo: Cliente
│   ├── admin.py
│   └── migrations/
├── Locacao/                 # App de gerenciamento de locações
│   ├── models.py            # Modelo: Locacao (com validações)
│   ├── admin.py             # Admin customizado com filtros
│   └── migrations/
├── admin-interface/         # Assets customizados do admin
│   ├── favicon/
│   └── logo/
├── templates/               # Templates HTML
│   ├── index.html
│   └── car-list.html
├── manage.py                # Gerenciador do Django
└── db.sqlite3               # Banco de dados (desenvolvimento)
```

## 🚀 Instalação e Configuração

### Pré-requisitos

- Python 3.9 ou superior
- PostgreSQL 12 ou superior
- pip (gerenciador de pacotes Python)
- virtualenv (recomendado)

### 1. Clone o Repositório

```bash
git clone https://github.com/seu-usuario/aluguel_carros.git
cd aluguel_carros-main
```

### 2. Crie um Ambiente Virtual

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

### 3. Instale as Dependências

```bash
pip install django==4.1
pip install psycopg2-binary
pip install django-admin-interface
pip install django-colorfield
```

**Ou crie um arquivo `requirements.txt`:**

```txt
Django==4.1
psycopg2-binary==2.9.5
django-admin-interface==0.21.3
django-colorfield==0.8.0
Pillow==10.0.0
```

```bash
pip install -r requirements.txt
```

### 4. Configure o Banco de Dados

#### Opção A: PostgreSQL (Recomendado para Produção)

```bash
# Criar banco de dados PostgreSQL
sudo -u postgres psql
CREATE DATABASE aluguel_carros;
CREATE USER aluguel_carros WITH PASSWORD 'admin123';
ALTER ROLE aluguel_carros SET client_encoding TO 'utf8';
ALTER ROLE aluguel_carros SET default_transaction_isolation TO 'read committed';
ALTER ROLE aluguel_carros SET timezone TO 'America/Sao_Paulo';
GRANT ALL PRIVILEGES ON DATABASE aluguel_carros TO aluguel_carros;
\q
```

**No `settings.py`:**

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'aluguel_carros',
        'USER': 'aluguel_carros',
        'PASSWORD': 'admin123',
        'HOST': 'localhost',
        'PORT': 5432,
    }
}
```

#### Opção B: SQLite (Desenvolvimento)

**No `settings.py`:**

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

### 5. Execute as Migrações

```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Crie um Superusuário

```bash
python manage.py createsuperuser
```

Forneça:
- Username
- Email
- Password

### 7. Colete Arquivos Estáticos

```bash
python manage.py collectstatic --noinput
```

### 8. Execute o Servidor

```bash
python manage.py runserver
```

Acesse: **http://localhost:8000/**

## 🎨 Interface Administrativa

O sistema utiliza o **Django Admin Interface** para proporcionar uma experiência moderna e personalizável.

### Acesso ao Admin

```
URL: http://localhost:8000/
Usuário: [superuser criado]
Senha: [senha do superuser]
```

### Recursos da Interface

- 🎨 **Tema Customizável** - Interface moderna com cores personalizáveis
- 🔍 **Busca Avançada** - Filtre por múltiplos campos
- 📊 **Dashboard** - Visão geral do sistema
- 🚀 **Autocomplete** - Seleção rápida de clientes e carros
- 📱 **Responsivo** - Funciona em desktop, tablet e mobile

## 💾 Modelos de Dados Detalhados

### Marca

```python
campos:
  - marca: CharField (max 30 caracteres)
```

### Modelo

```python
campos:
  - marca: ForeignKey para Marca
  - modelo: CharField (max 30 caracteres)
```

### Carro

```python
campos:
  - modelo: ForeignKey para Modelo
  - placa: CharField (único, max 10)
  - cor: CharField (max 50)
  - ano: IntegerField
  - qtd_portas: CharField
  - combustivel: CharField (choices: Diesel, Etanol, Gasolina, Biodiesel, Elétrico, GNV)
  - chassi: CharField (único)
  - renavam: IntegerField (único)
  - nr_hodometro: IntegerField
  - valor_locacao: DecimalField
  - status: CharField (L=Livre, O=Ocupado)

constraints:
  - Placa única
  - Chassi único
  - Renavam único
```

### Cliente

```python
campos:
  - nome: CharField (Nome ou Razão Social)
  - cpf: IntegerField (CPF ou CNPJ)
  - endereco: CharField
  - telefone: IntegerField
```

### Locação

```python
campos:
  - cliente: ForeignKey para Cliente
  - carro: ForeignKey para Carro (validado)
  - data_retirada: DateField
  - data_entrega_prevista: DateField
  - data_entrega: DateField (nullable)
  - intencao_uso: CharField
  - cnh: IntegerField
  - status: CharField (P=Pago, A=Aberto, C=Cancelado)

validações:
  - Impede locação de carro já ocupado
  - Atualiza status do carro automaticamente
```

## 🔒 Segurança

### ⚠️ Importante para Produção

**Antes de colocar em produção, você DEVE:**

1. **Alterar SECRET_KEY**
```python
# settings.py
SECRET_KEY = 'sua-chave-secreta-aleatoria-muito-longa'
```

2. **Desabilitar DEBUG**
```python
# settings.py
DEBUG = False
ALLOWED_HOSTS = ['seu-dominio.com', 'www.seu-dominio.com']
```

3. **Configurar HTTPS**
```python
# settings.py
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
```

4. **Proteger Credenciais do Banco**
```python
# Use variáveis de ambiente
import os
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('DB_NAME'),
        'USER': os.environ.get('DB_USER'),
        'PASSWORD': os.environ.get('DB_PASSWORD'),
        'HOST': os.environ.get('DB_HOST'),
        'PORT': os.environ.get('DB_PORT', 5432),
    }
}
```

## 📊 Fluxo de Trabalho

### Criando uma Locação

```
1. Cliente se cadastra no sistema
   ↓
2. Administrador acessa painel de Locações
   ↓
3. Clica em "Adicionar Locação"
   ↓
4. Seleciona Cliente (autocomplete)
   ↓
5. Seleciona Carro disponível (apenas status "Livre")
   ↓
6. Preenche datas, CNH e intenção de uso
   ↓
7. Salva a locação
   ↓
8. Sistema atualiza status do carro para "Ocupado" automaticamente
```

### Devolvendo um Carro

```
1. Administrador acessa a locação ativa
   ↓
2. Preenche "Data de Entrega"
   ↓
3. Altera status para "Pago"
   ↓
4. Salva
   ↓
5. Sistema atualiza status do carro para "Livre" automaticamente
```

## 🛠️ Comandos Úteis do Django

```bash
# Criar migrações
python manage.py makemigrations

# Aplicar migrações
python manage.py migrate

# Criar superusuário
python manage.py createsuperuser

# Coletar arquivos estáticos
python manage.py collectstatic

# Rodar servidor de desenvolvimento
python manage.py runserver

# Rodar em IP/porta específica
python manage.py runserver 0.0.0.0:8080

# Shell interativo do Django
python manage.py shell

# Limpar sessões expiradas
python manage.py clearsessions
```

## 🐛 Solução de Problemas

### Erro de Banco de Dados

```bash
# PostgreSQL não está rodando
sudo systemctl start postgresql

# Recriar banco
python manage.py flush
python manage.py migrate
```

### Erro de Permissões

```bash
# Linux/Mac
chmod +x manage.py

# Permissões de pasta
sudo chown -R $USER:$USER .
```

### Erro de Static Files

```bash
# Recriar arquivos estáticos
python manage.py collectstatic --clear --noinput
```

## 🚀 Deploy

### Heroku

```bash
# Instalar Heroku CLI
# Adicionar ao requirements.txt:
gunicorn==20.1.0
django-heroku==0.3.1
whitenoise==6.2.0

# Criar Procfile
echo "web: gunicorn aluguel_carros.wsgi" > Procfile

# Deploy
heroku create seu-app
git push heroku main
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```

### Docker

```dockerfile
# Criar Dockerfile
FROM python:3.9
ENV PYTHONUNBUFFERED=1
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

```bash
# Build e Run
docker build -t aluguel-carros .
docker run -p 8000:8000 aluguel-carros
```

## 📈 Melhorias Futuras

- [ ] API REST com Django REST Framework
- [ ] Sistema de autenticação para clientes
- [ ] App mobile (React Native / Flutter)
- [ ] Sistema de notificações (email/SMS)
- [ ] Relatórios e dashboard analítico
- [ ] Integração com gateway de pagamento
- [ ] Sistema de multas e danos
- [ ] Reservas online
- [ ] Upload de documentos (CNH, RG)
- [ ] Histórico de manutenção dos veículos
- [ ] Sistema de avaliação de clientes

## 📝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um Fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

### Padrões de Código

- Siga a PEP 8 para código Python
- Use nomes descritivos para variáveis e funções
- Documente funções complexas
- Escreva testes para novas features

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👥 Autores

**Seu Nome**
- GitHub: [@seu-usuario](https://github.com/seu-usuario)
- Email: seu-email@exemplo.com
- LinkedIn: [seu-linkedin](https://linkedin.com/in/seu-usuario)

## 🙏 Agradecimentos

- [Django](https://www.djangoproject.com/) - Framework web Python
- [Django Admin Interface](https://github.com/fabiocaccamo/django-admin-interface) - Interface administrativa moderna
- [PostgreSQL](https://www.postgresql.org/) - Sistema de banco de dados

## 📞 Suporte

Para dúvidas, problemas ou sugestões:

- **Issues:** [GitHub Issues](https://github.com/seu-usuario/aluguel_carros/issues)
- **Email:** seu-email@exemplo.com
- **Documentação Django:** [docs.djangoproject.com](https://docs.djangoproject.com/)

---

⭐ Se este projeto foi útil para você, considere dar uma estrela no repositório!

**Feito com ❤️ e Django**
