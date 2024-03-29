# COMANDOS - GUIA

**Comandos importantes!**

* `pip install -r requirements.txt` (instalar as dependências do projeto)
* `python manage.py runserver`
* Serve para rodar o servidor local e é interessante sempre usar para testar se sua aplicação está funcionando corretamente

1. Criar um ambiente virtual (venv) e ativá-lo&#x20;

* `python -m venv nomeVenv`
* `nomeVenv\Scripts\activate`
* `deactivate` (desativa a venv)

2. Instalação Django

* `pip install django`

3. Criar o arquivo onde ficará as dependências do projeto

* `pip freeze > requirements.txt`

4. Criar arquivo onde irá listar os arquivos que deseja ignorar&#x20;

* `.gitignore`
* `Exemplo:`

<figure><img src=".gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

5. Criar projeto Django

* `django-admin startproject nomeProjeto .`&#x20;
* (" . " serve para não criar outra subpasta)

6. Criar app Django (onde estará os modelos, views...)

* `django-admin startapp nomeApp`
* Definir o nome desse app em `settings.py` no `INSTALED_APPS` ('app'):

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* Ainda em `settings.py`:
* Dê um `import os`

<figure><img src=".gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Trocar o idioma e horário

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Em `STATIC_URL` acrescentar embaixo:

<figure><img src=".gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

_Django Rest Framework_

7. Instalação e Configuração

`pip install djangorestframework`

`pip install markdown`

* É utilizado pelo Django Rest Framework para fazer a página de documentação das APIs

`pip install django-filter`

* Facilita a utilização de filtros

<mark style="color:red;">Lembrete!</mark>

* Sempre que instalar algo não esqueça de adicionar aos requirements

<mark style="color:red;">`pip freeze > requirements.txt`</mark>

8. Registrar

* Vá em `INSTALED APPS` no arquivo `settings.py` para registrar as instalações:

<figure><img src=".gitbook/assets/image (4).png" alt="" width="359"><figcaption></figcaption></figure>

* Configurações relaionadas ao Django Rest Framework:
* `settings.py`

<figure><img src=".gitbook/assets/image (11).png" alt="" width="563"><figcaption></figcaption></figure>

9. Criar Banco de Dados:

* `python manage.py migrate`

10. Criar superuser

* `python manage.py  createsuperuser`&#x20;
* `python manage.py createsuperuser --username admin --email admin@example.com`

_Models_

* Em seu app vá até o arquivo `models.py` (serão os modelos necessários)
* Um modelo é uma fonte de dados sobre os seus dados, Ele contém os campos e comportamentos essenciais dos dados que você está armazenando. Em geral, cada modelo mapeia para uma única tabela no seu banco de dados.
* Ficará assim:

<figure><img src=".gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

* _Este é um exemplo de um model, após isso é preciso registrá-lo em **admin:**_

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* Após isso, use esse comando para registrar também:
* `python manage.py makemigrations`

11. Adicionar URL

* `urls.py`

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* **Testar:**
* `python manage.py runserver`

<figure><img src=".gitbook/assets/image (15).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (16).png" alt="" width="375"><figcaption><p>Redirect padrão do Django</p></figcaption></figure>

* Mesma coisa para logout
* _**Atualizando a url**_

<figure><img src=".gitbook/assets/image (17).png" alt="" width="506"><figcaption></figcaption></figure>

_Model Serializers_

* Irá "mapear" os models
* Python -> JSON&#x20;
* JSON -> Python

Criar arquivo `serializers.py`:

<figure><img src=".gitbook/assets/image (3).png" alt="" width="437"><figcaption></figcaption></figure>

* Para ver se está funcionando:

<figure><img src=".gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

\-> Importamos o que será necessário, além de buscar o último curso cadastrado e depois ver o que está no serializer em relação a cursos



_**APIView  -  HTTP GET**_

* `views.py`

<figure><img src=".gitbook/assets/image.png" alt="" width="563"><figcaption></figcaption></figure>

* Para as rotas vamos precisar criar um novo arquivo no nosso app
* `urls.py`

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* Nossos **endpoints**:

<figure><img src=".gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>
