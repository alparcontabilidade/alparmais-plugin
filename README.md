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

- Mostrar o seu dia: cards de hoje, atrasados e vencidos, e as conversas de atendimento que esperam resposta.
- Montar a lista de prioridades de um setor (`/alparmais:alparmais-prioridades fiscal`), por empresa e responsável, com a ação de cada item.
- Resumir uma empresa pelo código (`/alparmais:alparmais-empresa A0123`).
- Listar as empresas e as obrigações da sua carteira.
- Explicar como cada tela e rotina do Alpar+ funciona, lendo o manual do sistema.
- Citar sempre a fonte ("Alpar+"), repassar o recorte que o sistema aplicou e dizer quando não encontrou algo, sem inventar dados.

Exemplos de pergunta:

- "O que eu tenho para hoje?"
- "Quais cards meus estão atrasados?"
- "Monte a lista de prioridades do Fiscal."
- "Quais obrigações de setembro ainda estão abertas na minha carteira?"
- "Como funciona a baixa de uma obrigação?"

Sobre os termos: **vencido** é o que passou do prazo legal, **atrasado** é o que passou do prazo interno do escritório.

### Ferramentas do conector

Todas são de leitura e já devolvem os dados recortados pelo que a sua conta pode ver. Setores aceitos: legalização, alicerce, estruturação, fiscal, contábil, dp, atendimento, financeiro, ti, comercial e taxas.

| Ferramenta | O que faz |
|---|---|
| `resumo_do_dia` | Panorama do dia: o que pede atenção agora |
| `meus_cards` | Seus cards (abertos, vencidos, atrasados, de hoje, da semana) |
| `cards_do_setor` | Cards de um setor, agrupados por responsável |
| `pendencias_do_setor` | Pendências do setor (cards, obrigações e processos do Alicerce) com prioridade sugerida de 1 a 8 |
| `minhas_empresas` | Empresas da sua carteira |
| `empresa_resumo` | Resumo de uma empresa |
| `minhas_conversas` | Conversas de atendimento |
| `obrigacoes_da_carteira` | Obrigações da carteira, por competência |
| `ler_manual` | Manual do Alpar+, inteiro ou por seção |
| `resumo_do_sistema` | Resumo dos módulos e das regras de sigilo |

Para quem tem a chave de SQL no Alpar+, ficam disponíveis também `consultar_dados`, `listar_tabelas` e `colunas_da_tabela`, para consultas livres de leitura.

## Privacidade

- O Claude **só vê o que a pessoa logada vê no Alpar+**. As permissões, o recorte por equipe e o sigilo de RH do sistema continuam valendo.
- O conector é **somente leitura**: não cria, não edita e não apaga nada.
- As ferramentas já devolvem só o recorte que a sua conta pode ver. Nas consultas livres (só para quem tem a chave de SQL), tabelas de senha, sessão, token e certificado não são consultáveis.
- Cada consulta fica registrada no Alpar+, para auditoria.
- Nenhum dado de cliente, segredo ou chave está neste repositório.
- Como em qualquer uso do Claude, o resultado das consultas passa pela conversa com o Claude. Use em computador de trabalho e siga a política de dados do seu escritório.

## Revogar o acesso

- No Alpar+, em **Meu Espaço > Conexões com o Claude**, clique em **Revogar** na conexão desejada. O administrador do escritório também pode revogar em **Configurações**.
- No Claude Code, você pode ainda rodar `/mcp` e limpar a autenticação do servidor `alparmais`, ou remover o conector com `claude mcp remove alparmais`. Para desinstalar o plugin: `/plugin uninstall alparmais@alparmais`.

## Suporte

Fale com o administrador do Alpar+ do seu escritório. Problemas do plugin podem ser abertos nas issues deste repositório (sem colocar dados de clientes).

## Licença

Veja o arquivo [LICENSE](LICENSE).
