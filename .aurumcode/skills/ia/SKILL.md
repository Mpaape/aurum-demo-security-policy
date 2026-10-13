---
name: ia
version: 1
languages: [python]
---
Regras da seguranca para software que conversa com modelos de IA. Cada `## `
abaixo e uma regra citavel pelo AurumCode; `severity: error` reprova o merge.

## IA-001 Resposta do modelo nunca e executada
severity: error
Texto devolvido por um modelo de IA e dado, nunca codigo: nao passa por
`exec`, `eval`, `compile`, `subprocess` nem shell. Para "rodar o que a IA
sugeriu", mostre o codigo e deixe a pessoa decidir.

## IA-002 Chamada ao modelo tem limite de tempo
severity: warning
Toda chamada de rede ao modelo declara `timeout`; sem ele, um servico lento
trava o programa inteiro.
