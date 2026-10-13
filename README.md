# security-policy — política de segurança (mantida pelo time de segurança)

Todo serviço que aponta para este repositório (`policy_repository` no workflow do
AurumCode) herda o que está aqui e **não consegue afrouxar nada**: um `gate:` ou
`ignore:` escrito no serviço é ignorado com aviso.

| Arquivo | O que decide |
|---|---|
| `ANALISE-DE-SEGURANCA.md` | o documento de análise de segurança curado pelo time: papel do revisor, o que verificar (9 áreas), como escrever o parecer e quem aprova exceção |
| `.aurumcode/config.yml` | o gate (`fail_on: [error]`, `inconclusive: block`), o `ignore` e o idioma do parecer; exceções aprovadas (com dono e validade) moram aqui |
| `.aurumcode/skills/seguranca/SKILL.md` | **SEC-001** segredo nunca no código (`error`), **SEC-002** SQL sem concatenação (`error`), **SEC-003** certificado nunca desligado (`error`), **SEC-004** entrada externa nunca vira comando (`error`), **SEC-005** dependência com versão fixada (`warning`), **SEC-006** log sem segredo nem dado pessoal (`warning`) |
| `.aurumcode/skills/ia/SKILL.md` | **IA-001** resposta do modelo nunca é executada (`error`), **IA-002** chamada ao modelo com timeout (`warning`) |

As regras de catálogo (segredo no código, SQL injection, XSS, injeção de comando) vêm do
próprio AurumCode; o gate daqui é o que transforma qualquer `error` em bloqueio do merge.
