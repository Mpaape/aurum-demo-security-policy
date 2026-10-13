---
name: seguranca
version: 1
paths: ["**"]
---
Regras do time de seguranca para todo servico. Cada `## ` abaixo e uma regra
citavel pelo AurumCode (`seguranca#<slug>`); `severity: error` reprova o merge,
`warning` recomenda sem bloquear.

## SEC-001 Segredo nunca fica no codigo
severity: error
Chave de API, senha, token ou certificado privado nao aparece em codigo, teste,
fixture ou configuracao versionada. O valor vem do ambiente ou do cofre de
secrets do CI; se um segredo vazou num commit, e revogado, nao so removido.

Violacao: `API_KEY = "sk-live-..."`

Correcao: `API_KEY = os.environ["API_KEY"]`

## SEC-002 Consulta SQL nunca e montada por concatenacao
severity: error
Toda consulta usa parametros (`?`, `%s`, `:nome`) ou um query builder; valor que
vem de usuario, arquivo ou rede nunca entra na string da consulta.

Violacao: `db.execute("select * from pedidos where cliente = " + cliente_id)`

Correcao: `db.execute("select * from pedidos where cliente = ?", (cliente_id,))`

## SEC-003 Verificacao de certificado nunca e desligada
severity: error
Chamada HTTPS nao usa `verify=False`, `CERT_NONE` nem desativa a validacao de
certificado; ambiente de teste usa um certificado proprio confiavel.

## SEC-004 Entrada externa nunca vira comando
severity: error
Texto vindo de usuario, arquivo, rede ou modelo de IA nao passa por `eval`,
`exec`, `os.system`, `subprocess` com `shell=True` nem e concatenado em linha
de comando.

## SEC-005 Dependencia tem versao fixada
severity: warning
Toda dependencia declarada tem versao exata (`==`) ou lock; sem fixacao, um
build amanha nao e o build de hoje.

## SEC-006 Log nao contem segredo nem dado pessoal
severity: warning
Mensagens de log e de erro nao imprimem token, senha, cabecalho `Authorization`
nem dado pessoal (CPF, e-mail, telefone) em texto claro.
