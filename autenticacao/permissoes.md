# Permissoes

{% embed url="https://www.django-rest-framework.org/api-guide/permissions/" %}

{% embed url="https://medium.com/@verasleonardo210/como-utilizar-django-role-permissions-no-seu-projeto-b3461aa263f0" %}

{% embed url="https://medium.com/@jamil.pyhidrodev/permiss%C3%B5es-e-autentica%C3%A7%C3%A3o-em-django-rest-framework-74b20a3c9981" %}

Claro! Vou explicar de uma forma mais detalhada como usar permissões em um exemplo prático com Django, utilizando os modelos de turmas, salas, professores, alunos e diretores que você mencionou.

#### 1. Definir Modelos de Usuário Personalizados:

Primeiro, vamos definir os modelos de usuário personalizados para professor, aluno e diretor, estendendo o modelo de usuário padrão do Django.

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class Professor(AbstractUser):
    # Campos específicos do professor

class Aluno(AbstractUser):
    # Campos específicos do aluno

class Diretor(AbstractUser):
    # Campos específicos do diretor
```

#### 2. Definir Modelos para Turmas, Salas e Materiais:

Agora, vamos definir os modelos para turmas, salas e materiais, e relacioná-los com os modelos de usuário personalizados.

```python
class Turma(models.Model):
    professor = models.ForeignKey(Professor, on_delete=models.CASCADE)
    sala = models.ForeignKey(Sala, on_delete=models.CASCADE)
    # Outros campos da turma

class Sala(models.Model):
    nome = models.CharField(max_length=100)
    # Outros campos da sala

class Materia(models.Model):
    turma = models.ForeignKey(Turma, on_delete=models.CASCADE)
    nome = models.CharField(max_length=100)
    # Outros campos da matéria
```

#### 3. Definir Permissões Personalizadas:

Agora, vamos definir permissões personalizadas para cada tipo de usuário e atribuí-las aos grupos correspondentes.

```python
from django.contrib.auth.models import Group, Permission

# Criar permissões personalizadas
can_view_grade = Permission.objects.create(codename='can_view_grade', name='Can view grade')

# Criar grupos
professor_group = Group.objects.create(name='Professor')
aluno_group = Group.objects.create(name='Aluno')
diretor_group = Group.objects.create(name='Diretor')

# Atribuir permissões aos grupos
professor_group.permissions.add(can_view_grade)
diretor_group.permissions.add(can_view_grade)
```

#### 4. Implementar Lógica de Visualização de Notas:

Finalmente, implementaremos a lógica de visualização de notas com base nas permissões atribuídas aos grupos.

```python
from django.contrib.auth.decorators import user_passes_test
from django.shortcuts import render

def can_view_grade(user):
    return user.groups.filter(name__in=['Professor', 'Diretor']).exists()

@user_passes_test(can_view_grade)
def view_grade(request):
    # Lógica para exibir as notas
    # Exemplo: obter notas dos alunos da turma do professor logado
    professor = Professor.objects.get(username=request.user.username)
    turma_do_professor = Turma.objects.filter(professor=professor).first()
    alunos_na_turma = Aluno.objects.filter(turma=turma_do_professor)
    notas = []
    for aluno in alunos_na_turma:
        notas.append({
            'aluno': aluno,
            'nota': aluno.nota_set.get(materia__turma=turma_do_professor).valor
        })
    return render(request, 'grade.html', {'notas': notas})
```

Neste exemplo, o view `view_grade` só permite o acesso a professores e diretores, pois apenas eles têm permissão para visualizar as notas dos alunos.

Espero que isso ajude a esclarecer como usar permissões em um exemplo prático com Django! Se tiver mais alguma dúvida, estou à disposição para ajudar.
