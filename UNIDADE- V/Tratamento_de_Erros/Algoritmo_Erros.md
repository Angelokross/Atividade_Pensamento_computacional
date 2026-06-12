# Algoritmo_Erros.md — Versão Original (com bugs)

## Contexto

O script `sistema_turma.py` foi criado a partir do mesmo conjunto de dados da
atividade anterior (lista de alunos da turma) para calcular a **média da
turma**, **buscar um aluno pela posição na lista** e **aplicar um desconto
sobre uma nota** (simulando uma penalidade/bônus percentual).

## Código Original (com erros)

```python
alunos = ["Ana", "Bruno", "Carlos", "Daniela", "Eduardo"]
notas = [8.5, 7.0, 9.0, 6.5, 8.0]

def media_turma(notas)
    soma = 0
    for n in notas:
        soma = soma + n
    media = soma / len(notas) - 0.5
    return media

def buscar_aluno(posicao):
    return alunos[posicao]

def aplicar_bonus(nota, bonus):
    nota_final = nota + bonus / 100
    return nota_final

print("Média da turma:", media_turma(notas))
print("Aluno representante (posição 5):", buscar_aluno(5))
print("Nota com bônus:", aplicar_bonus(8.0, 50))
```

## Erros Identificados

| # | Erro | Tipo | Onde está | Descrição |
|---|------|------|-----------|-----------|
| 1 | Falta de `:` em `def media_turma(notas)` | **Sintaxe** | Linha da definição da função `media_turma` | A declaração de função em Python exige dois-pontos (`:`) ao final. Sem ele, o interpretador gera `SyntaxError` e o programa não executa. |
| 2 | `media = soma / len(notas) - 0.5` | **Lógica (Erro Lógico-Matemático / Falha de Prioridade Operacional)** | Função `media_turma` | Por precedência de operadores, primeiro é calculada a divisão (`soma/len(notas)`) e **depois** subtraído `0.5`, deslocando a média real da turma sem nenhuma justificativa de negócio — exatamente o mesmo padrão de erro de parênteses/precedência mostrado na aula (`preco - desconto / 100`). |
| 3 | `buscar_aluno(5)` em uma lista de 5 elementos (índices 0 a 4) | **Execução (Erro de Execução / IndexError)** | Chamada da função `buscar_aluno` | A lista `alunos` possui posições válidas de `0` a `4`. Chamar `buscar_aluno(5)` provoca um `IndexError: list index out of range`, interrompendo o programa em tempo de execução. |
| 4 | `aplicar_bonus` não valida o valor de `bonus` | **Lógica (Falha de Validação / Ação Defensiva ausente)** | Função `aplicar_bonus` | A função aceita qualquer valor numérico sem verificar limites (ex: `bonus = 50` soma 0.5 ponto a uma nota que já é 8.0, podendo gerar nota final acima da escala máxima permitida, 10.0). Não há "filtro de validação" antes do processamento, conforme o diagrama Usuário/Sistema da aula. |

## Regra de Ouro aplicada

> "Quanto mais cedo o erro humano é descoberto, menor a chance de ele se
> transformar em um bug letal no sistema."

Os erros 1 e 3 seriam descobertos imediatamente ao tentar **executar** o
programa (teste estático/dinâmico). O erro 2 e o erro 4, porém, são
**silenciosos**: o programa roda normalmente e retorna resultados
*matematicamente ou logicamente incorretos*, sem nenhum aviso — por isso são
os mais perigosos.
