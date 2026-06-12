# Algoritmo_Corrigido.md — Versão Corrigida (com justificativas)

## Código Corrigido

```python
alunos = ["Ana", "Bruno", "Carlos", "Daniela", "Eduardo"]
notas = [8.5, 7.0, 9.0, 6.5, 8.0]

NOTA_MAXIMA = 10.0
NOTA_MINIMA = 0.0


def media_turma(notas):
    """Calcula a média aritmética simples das notas da turma."""
    if not notas:                       # Ação defensiva: lista vazia
        return 0.0
    soma = 0
    for n in notas:
        soma = soma + n
    media = soma / len(notas)           # Correção 2: sem subtração indevida
    return media


def buscar_aluno(posicao):
    """Retorna o aluno em uma posição válida da lista de chamada."""
    if posicao < 0 or posicao >= len(alunos):   # Correção 3: validação de índice
        return None
    return alunos[posicao]


def aplicar_bonus(nota, bonus):
    """Aplica um bônus percentual à nota, respeitando a escala 0-10."""
    nota_final = nota + (bonus / 100)           # Parênteses explícitos (clareza)

    # Correção 4: filtro de validação - garante que a nota final
    # permaneça dentro da escala permitida (0 a 10).
    if nota_final > NOTA_MAXIMA:
        nota_final = NOTA_MAXIMA
    elif nota_final < NOTA_MINIMA:
        nota_final = NOTA_MINIMA

    return nota_final


# --- Execução principal ---
print("Média da turma:", media_turma(notas))

aluno = buscar_aluno(5)
if aluno is None:
    print("Posição 5 inválida: a turma possui apenas 5 alunos (índices 0 a 4).")
else:
    print("Aluno encontrado:", aluno)

print("Nota com bônus:", aplicar_bonus(8.0, 50))
```

## Justificativas das Alterações

### Correção 1 — Sintaxe (`def media_turma(notas):`)
Foi adicionado o caractere `:` ao final da declaração da função. Em Python,
toda estrutura de bloco (funções, laços, condicionais) exige dois-pontos.
Sem essa correção, o interpretador não consegue nem iniciar a execução do
programa (`SyntaxError`).

### Correção 2 — Lógica/Matemática (`media = soma / len(notas)`)
Removida a subtração de `0.5`, que não tinha nenhuma justificativa de
negócio e distorcia o resultado real da média da turma — o mesmo padrão de
"erro de parênteses" mostrado na aula, onde uma operação extra altera
silenciosamente o resultado final sem quebrar o programa.

### Correção 3 — Execução (`buscar_aluno`)
Adicionada uma **pré-condição** (`if posicao < 0 or posicao >= len(alunos)`)
que verifica se o índice solicitado existe antes de acessar a lista. Em vez
de o programa **quebrar** com `IndexError`, ele agora **retorna `None`** e
o ponto de chamada trata esse caso com uma mensagem amigável — seguindo o
princípio "sistemas interativos perguntam; sistemas transacionais desfazem":
aqui, o sistema **avisa** o usuário em vez de travar.

### Correção 4 — Lógica/Validação (`aplicar_bonus`)
- Adicionados parênteses explícitos em `(bonus / 100)` para deixar a
  precedência clara, eliminando qualquer ambiguidade de leitura.
- Implementado um **filtro de validação** que garante que a nota final nunca
  saia da escala válida (0 a 10), aplicando o conceito de "Ação Defensiva":
  prever o estado inválido e corrigi-lo antes que ele se propague pelo
  sistema.

### Correção adicional — Caso de lista vazia em `media_turma`
Foi incluída uma verificação `if not notas: return 0.0` para evitar uma
futura **divisão por zero** (`ZeroDivisionError`) caso a lista de notas
esteja vazia — aplicando o princípio de "Falha Crítica de Recurso":
cancelar a operação e retornar a um estado seguro em vez de travar o
sistema.
