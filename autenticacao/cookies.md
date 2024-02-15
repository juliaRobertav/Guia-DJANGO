# Cookies

Para armazenar o token JWT de forma segura no lado do cliente usando cookies e validar o token JWT em suas views do Django, você pode seguir os passos abaixo:

1. **Instale a biblioteca python-jose**:

Você pode instalar a biblioteca python-jose usando o pip:

```bash
pip install python-jose
```

2. **Armazene o token JWT em um cookie seguro**:

Depois de obter o token JWT após o processo de login, você pode armazená-lo em um cookie seguro no lado do cliente. Aqui está um exemplo de como você pode fazer isso em uma view do Django:

```python
from django.http import JsonResponse
from django.views.decorators.csrf import ensure_csrf_cookie

@ensure_csrf_cookie
def login_view(request):
    # Obter o token JWT após o login
    token = "seu_token_jwt_aqui"

    # Definir um cookie seguro com o token JWT
    response = JsonResponse({'message': 'Login successful'})
    response.set_cookie('jwt_token', token, httponly=True, secure=True)  # Defina secure=True para cookies seguros
    return response
```

Neste exemplo, `set_cookie` é usado para definir um cookie seguro chamado `'jwt_token'` com o valor do token JWT. O parâmetro `httponly=True` garante que o cookie só será acessível via HTTP e não será acessível através de scripts do lado do cliente, o que melhora a segurança.

3. **Validar o token JWT em suas views do Django**:

Depois de armazenar o token JWT em um cookie seguro, você pode validar o token JWT em suas views do Django para garantir a autenticidade e integridade dos dados. Aqui está um exemplo de como você pode fazer isso:

```python
from jose import jwt
from django.http import JsonResponse

def minha_view_protegida(request):
    # Obter o token JWT do cookie seguro
    token = request.COOKIES.get('jwt_token')

    if token:
        try:
            # Validar e decodificar o token JWT
            payload = jwt.decode(token, 'seu_segredo_aqui', algorithms=['HS256'])

            # Extraia os dados do payload, se necessário
            user_id = payload['user_id']

            # Faça alguma coisa com os dados do usuário
            return JsonResponse({'message': f'Usuário autenticado com ID: {user_id}'})
        except jwt.ExpiredSignatureError:
            return JsonResponse({'error': 'Token JWT expirado'}, status=401)
        except jwt.JWTError:
            return JsonResponse({'error': 'Token JWT inválido'}, status=401)
    else:
        return JsonResponse({'error': 'Token JWT não encontrado'}, status=401)
```

Neste exemplo, `jwt.decode` é usado para decodificar e validar o token JWT usando uma chave secreta. Se o token JWT for válido, você pode extrair os dados do payload, como o ID do usuário, e realizar as operações necessárias.

Lembre-se de substituir `'seu_segredo_aqui'` com a chave secreta que você usa para assinar e validar seus tokens JWT. Certifique-se de manter essa chave secreta em um local seguro e não compartilhá-la publicamente.

Estes são os passos básicos para armazenar e validar um token JWT em um cookie seguro no lado do cliente e usar o token JWT em suas views do Django para autenticar e autorizar os usuários. Certifique-se de adaptar e expandir este código de acordo com os requisitos específicos do seu projeto.
