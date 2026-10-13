# security-policy — política de segurança (mantida pelo time de segurança)

Todo serviço que aponta para este repositório (`policy_repository` no workflow do
AurumCode) herda o que está aqui e **não consegue afrouxar nada**: um `gate:` ou
`ignore:` escrito no serviço é ignorado com aviso.

| Arquivo | O que decide |
|---|---|
| `.aurumcode/config.yml` | o gate (`fail_on: [error]`, `inconclusive: block`), o `ignore` e o idioma do parecer; exceções aprovadas (com dono e validade) moram aqui |
| `.aurumcode/skills/ia/SKILL.md` | as regras do time: **IA-001** resposta do modelo nunca é executada (`error`), **IA-002** chamada ao modelo com timeout (`warning`) |

As regras de catálogo (segredo no código, SQL injection, XSS, injeção de comando) vêm do
próprio AurumCode; o gate daqui é o que transforma qualquer `error` em bloqueio do merge.
