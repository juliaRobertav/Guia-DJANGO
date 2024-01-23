# COMANDOS - GUIA

1. Criar um ambiente virtual (venv) e ativá-lo&#x20;

* `python -m venv nomeVenv`
* `nomeVenv\Scripts\activate`

2. Instalação Django

* `pip install django`

3. Criar o arquivo onde ficará as dependências do projeto

* `requirements.txt`

4. Criar arquivo onde irá listar os arquivos que deseja ignorar&#x20;

* `.gitignore`

5. Criar projeto Django

* `django-admin startproject nomeProjeto .`&#x20;
* (" . " serve para não criar outra subpasta)

Django Rest Framework

6. Instalação

* `pip install djangorestframework`

7. Registrar

* Vá em `INSTALED APPS` no arquivo `settings.py`&#x20;
* `'rest_framework'`

8. Criar Banco de Dados

* `python manage.py migrate`



* **Comando importante**
* `python manage.py runserver`
* Serve para rodar o servidor local e é interessante sempre usar para testar se sua aplicação está funcionando corretamente
