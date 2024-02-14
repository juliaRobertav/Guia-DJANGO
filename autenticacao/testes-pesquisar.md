# Testes/Pesquisar

```python
"""
 Consumindo a API
"""

from pprint import pprint
from typing import Dict
import click
import requests
from requests.auth import HTTPBasicAuth


BASE_URL = 'http://localhost:8000/api/v1/'



def fetch_token(session, endpoint, username, password):

    data = {
        'usuario' : username,
        'senha' : password,
    }
    with session.post(
        endpoint,
        auth=HTTPBasicAuth(username, password),
        data=data
    ) as response:
        return response.json()

        
def get_token(usuario: str, senha: str) -> Dict[str, str]:

    with requests.Session() as session:
        endpoint = f'{BASE_URL}authjwt/'
        response = fetch_token(session, endpoint, usuario, senha)
        data = {
            'access_token' : response['access'],
        }
        return data


def fetch(session, endpoint, access_token):
    headers = {'Authorization' : f'Bearer {access_token}'}
    with session.get(endpoint, headers=headers) as response:
        return response.json()


@click.command()
@click.option('--usuario', '-u', prompt='usuario', help='Digite seu usuario.')
@click.option('--senha', '-s', prompt='senha', help='Digite sua senha.')


def main(usuario, senha):

    token = get_token(usuario, senha)
    access_token = token['access_token']
    with requests.Session() as session:
        endpoint = 'http://127.0.0.1:8000/api/v1/aprendiz'
        pprint(response)


if __name__ == '__main__':
    main ()




from django.http import JsonResponse
import requests 


def obter_token(request):
    if request.method == 'POST':
        url = 'http://127.0.0.1:8000/api/v1'
        credentials = {
            'usuario' : request.POST['usuario'],
            'senha' : request.POST['senha'],
        }
        response = requests.post(url, json=credentials)
        if response.status_code == 200:
            token = response.json()['auth_token']
            return JsonResponse({'token' : token})

        elif response.status_code == 400:
            return JsonResponse({'error' : 'Erro ao obter token de autenticação'})
            
        else:
            return JsonResponse({'error' : 'Método não permitido'}, status=405)





class CustomUserManager(BaseUserManager):

    def create_user(self, email, nome, usuario, senha=None):
        if not email:
            raise ValueError('O usuário precisa cadastrar um email')
        email = self.normalize_email(email)
        usuario = self.model(email=email, nome=nome)
        usuario.set_password(senha)
        usuario.save(using=self._db)
        return usuario



# Abstract User

from django.contrib.auth.models import AbstractBaseUser, PermissionsMixin, BaseUserManager

def create_superuser(self, email, senha=None, **extra_fields):
    extra_fields.setdefault('is_staff', True)
    extra_fields.setdefault('is_superuser', True)
        

class CustomUser(AbstractBaseUser, PermissionsMixin):
    nome = models.CharField(max_length=120, null=False)
    usuario = models.CharField(max_length=10, null=False, unique=True)
    senha = models.CharField(max_length=20, null=False)
    email = models.EmailField(max_length=254, null=False)
    ativo = models.BooleanField(default=True)

    objects = CustomUserManager()

    USERNAME_FIELD = 'usuario'
    REQUIRED_FIELDS = ['nome', 'email', 'senha']

    def get_full_name(self):
        return self.nome

    def get_short_name(self):
        return self.nome

    def __str__(self):
        return self.nome



# serializer :

from djoser.serializers import UserCreateSerializer

Usuario = get_user_model()


class CustomUserSerializer(UserCreateSerializer):
    class Meta(UserCreateSerializer.Meta):
        model = Usuario
        fields = ('id', 'nome', 'usuario', 'email', 'senha')
```







<pre class="language-python"><code class="lang-python"><strong># testes para autenticação
</strong>

from rest_framework.permissions import BasePermission
from djoser.views import UserCreateView
from api.permissions import AllowUnauthenticatedCreate

class AllowUnauthenticatedCreate(BasePermission):
    def has_permission(self, request, view):
        if view.action == 'create':
            return True
        return request.user and request.user.is_authenticated

class CustomUserCreateView(UserCreateView):
    permission_classes = [AllowUnauthenticatedCreate]




from django.shortcuts import render
from rest_framework.response import Response
from rest_framework.views import APIView
from rest_framework_simplejwt.tokens import RefreshToken
from django.contrib.auth import authenticate

class CustomTokenObtainPairView(APIView):
    def post(self, request, *args, **kwargs):

        usuario = request.data.get('usuario')
        senha = request.data.get('senha')
        user = authenticate(usuario=usuario, senha=senha)
        if user:
            refresh = RefreshToken.for_user(user)
            return Response({'refresh' : str(refresh), 'access' : str(refresh.access_token), })
        else:
            return Response({'error' : 'credenciais inválidas'}, status=400)

</code></pre>
