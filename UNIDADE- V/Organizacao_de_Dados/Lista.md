# Estrutura 1: Lista — Sequência de Chamada da Turma

Uma **lista** é uma sequência simples, linear e ordenada de elementos, onde a
posição determina a ordem de acesso. Aqui, ela representa a **lista de chamada**
dos alunos da turma, do primeiro ao último.

| Posição | Aluno     |
|:-------:|-----------|
| 0       | Ana       |
| 1       | Bruno     |
| 2       | Carlos    |
| 3       | Daniela   |
| 4       | Eduardo   |

## Representação Computacional (pseudocódigo / Python)

```python
lista_chamada = ["Ana", "Bruno", "Carlos", "Daniela", "Eduardo"]

# Acesso por posição (ordem de chamada)
for posicao, aluno in enumerate(lista_chamada):
    print(f"{posicao}: {aluno}")
```

## Por que uma Lista?

- **Simplicidade:** fácil de implementar e ler.
- **Ordem importa:** a posição na lista corresponde diretamente à ordem de
  chamada em sala de aula.
- **Uso cotidiano:** agendas, checklists e filas seguem exatamente essa mesma lógica.
