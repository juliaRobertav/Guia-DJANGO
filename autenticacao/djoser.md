# Djoser

{% embed url="https://djoser.readthedocs.io/en/latest/jwt_endpoints.html" %}

{% embed url="https://medium.com/@hellenwain_54279/securing-django-rest-user-apis-with-djoser-273275921343" %}

#### <mark style="background-color:green;">JWT & Djoser</mark>

Djoser já possui URLs embutidas para gerenciar a aunteticação JWT, como esses:

```
/jwt/create/: retorna access_tokens e refresh_tokens quando você passa credenciais de login.

/jwt/refresh/: Use este endpoint para atualizar o JWT.

/jwt/verify/: Use este endpoint para verificar o JWT.

/auth/token/login/

/users/reset_password/

/users/reset_password_confirm/
```

O JWT cuida de toda a lógica



<mark style="background-color:green;">**Configurações adicionais do Djoser**</mark>

1. **`USER_CREATE_PASSWORD_RETYPE`**:
   * **Para que serve:** Esta configuração determina se o endpoint de criação de usuário requer que o usuário digite a senha duas vezes para evitar erros de digitação.
   * **Como usar:** Você pode configurá-lo como `True` para ativar a verificação de senha dupla ou `False` para desativá-la. Por padrão, é `False`.
2. **`SEND_ACTIVATION_EMAIL`**:
   * **Para que serve:** Esta configuração determina se o Djoser deve enviar um email de ativação após o registro do usuário.
   * **Como usar:** Configure como `True` para ativar o envio de email de ativação ou `False` para desativá-lo. Por padrão, é `False`.
3. **`ACTIVATION_URL`**:
   * **Para que serve:** Esta configuração permite especificar o URL que será incluído no email de ativação enviado aos usuários.
   * **Como usar:** Defina o URL desejado para o email de ativação. Por padrão, é `'auth/users/activation/{uid}/{token}'`.
4. **`SEND_CONFIRMATION_EMAIL`**:
   * **Para que serve:** Esta configuração determina se o Djoser deve enviar um email de confirmação após a alteração do endereço de email do usuário.
   * **Como usar:** Configure como `True` para ativar o envio de email de confirmação ou `False` para desativá-lo. Por padrão, é `False`.
5. **`SET_USERNAME_RETYPE`**:
   * **Para que serve:** Esta configuração determina se o endpoint de alteração de nome de usuário requer que o usuário digite o nome de usuário atual para confirmação.
   * **Como usar:** Configure como `True` para ativar a verificação de nome de usuário duplo ou `False` para desativá-la. Por padrão, é `False`.
6. **`PASSWORD_RESET_CONFIRM_URL`**:
   * **Para que serve:** Esta configuração permite especificar o URL que será incluído no email de redefinição de senha enviado aos usuários.
   * **Como usar:** Defina o URL desejado para o email de redefinição de senha. Por padrão, é `'password/reset/confirm/{uid}/{token}'`.
