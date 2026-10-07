# Alpar+ para o Claude Code

Plugin e conector MCP que ligam o Claude Code ao **Alpar+**, o sistema de gestão de escritórios contábeis da Alpar Contabilidade. Com ele, você pergunta em português e o Claude consulta o Alpar+ por você: dados de empresas, obrigações, atendimento, honorários e o manual de uso do sistema.

Este repositório contém só o plugin (instruções e configuração do conector). O software do Alpar+ não está aqui.

## Instalar em 2 comandos

Dentro do Claude Code:

```
/plugin marketplace add alparcontabilidade/alparmais-plugin
/plugin install alparmais@alparmais
```

Depois rode `/reload-plugins` (ou reinicie o Claude Code) para carregar o plugin.

### Alternativa manual (só o conector, sem o plugin)

No terminal:

```
claude mcp add --transport http alparmais https://alparmais.alparcontabilidade.com.br/mcp
```

Dá acesso às mesmas ferramentas. O plugin acrescenta as instruções de uso em português e os comandos prontos.

## Conectar a sua conta

1. Na primeira vez que o Claude usar uma ferramenta do Alpar+, o Claude Code abre o **navegador** na página de login do Alpar+. Você também pode rodar `/mcp`, escolher o servidor `alparmais` e autenticar.
2. Entre com o seu e-mail de trabalho. O Alpar+ descobre sozinho a instância do seu escritório a partir do e-mail.
3. Autorize o acesso e volte ao terminal.
4. Para testar, rode `/alparmais:alparmais-conectar`.

O login usa OAuth 2.1: você entra no navegador e o Claude Code recebe apenas uma autorização, nunca a sua senha. **Nunca digite senha no chat.**

## O que o Claude passa a fazer

- Responder perguntas sobre os seus dados do Alpar+ (empresas, carteiras, obrigações e entregas, atendimentos, honorários, cadastros).
- Explicar como cada tela e rotina do Alpar+ funciona, lendo o manual do sistema.
- Montar o resumo de uma empresa pelo código com o comando `/alparmais:alparmais-empresa A0123`.
- Citar sempre a fonte ("Alpar+") e dizer quando não encontrou algo, sem inventar dados.

Exemplos de pergunta:

- "Quais empresas do Simples Nacional temos no Alpar+?"
- "Quais obrigações vencem esta semana e ainda estão pendentes?"
- "Como funciona a baixa de uma obrigação?"

### Ferramentas do conector

Todas são de leitura.

| Ferramenta | O que faz |
|---|---|
| `resumo_do_sistema` | Resumo dos módulos, das tabelas principais e das regras de sigilo |
| `listar_tabelas` | Lista as tabelas consultáveis |
| `colunas_da_tabela` | Mostra as colunas de uma tabela |
| `consultar_dados` | Executa uma consulta `SELECT` (até 500 linhas) |
| `ler_manual` | Lê o manual do Alpar+, inteiro ou por seção |

## Privacidade

- O Claude **só vê o que a pessoa logada vê no Alpar+**. As permissões, o recorte por equipe e o sigilo de RH do sistema continuam valendo.
- O conector é **somente leitura**: não cria, não edita e não apaga nada.
- Tabelas de senha, sessão, token e certificado não são consultáveis.
- Cada consulta fica registrada no Alpar+, para auditoria.
- Nenhum dado de cliente, segredo ou chave está neste repositório.
- Como em qualquer uso do Claude, o resultado das consultas passa pela conversa com o Claude. Use em computador de trabalho e siga a política de dados do seu escritório.

## Revogar o acesso

- No Claude Code, rode `/mcp`, escolha o servidor `alparmais` e limpe a autenticação (ou remova o conector com `claude mcp remove alparmais`). Para desinstalar o plugin: `/plugin uninstall alparmais@alparmais`.
- Para encerrar a autorização também no lado do Alpar+, peça à pessoa que administra o sistema no seu escritório para revogar a sessão do conector.

## Suporte

Dúvidas e problemas: abra uma *issue* neste repositório (sem colocar dados de clientes) ou fale com o time responsável pelo Alpar+ no seu escritório.

## Licença

Veja o arquivo [LICENSE](LICENSE).
